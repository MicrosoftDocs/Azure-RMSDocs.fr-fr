---
title: "Migrer un déploiement AD RMS vers Azure Information Protection - Phase 5"
description: "Phase 5 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 10 à 12 de la migration d’AD RMS vers Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e07e9252837fe17c84ce17c3b1fc8e20734190fd
ms.sourcegitcommit: 237ce3a0cc4921da5a08ed5753e6491403298194
translationtype: HT
---
# <a name="migration-phase-5---post-migration-tasks"></a>Phase de migration 5 : Tâches de post-migration

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*


Utilisez les informations suivantes pour la Phase 5 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 10 à 12 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-10-deprovison-ad-rms"></a>Étape 10. Annuler l’approvisionnement d’AD RMS

Supprimez le point de connexion de service d'Active Directory pour empêcher des ordinateurs de découvrir votre infrastructure Rights Management locale. Ceci est facultatif pour les clients existants que vous migrez en raison de la redirection que vous avez configurée dans le Registre (par exemple en exécutant le script de migration). Cependant, la suppression du point de connexion de service empêche les nouveaux clients, et potentiellement les outils et les services RMS, de trouver le point de connexion de service quand la migration est terminée et que toutes les connexions doivent accéder au service Azure Rights Management. 

Pour supprimer le point de connexion de service, assurez-vous que vous êtes connecté en tant qu’administrateur d’entreprise de domaine, puis procédez comme suit :

1. Dans la console Active Directory Rights Management Services, cliquez sur le cluster AD RMS, puis cliquez sur **Propriétés**.

2. Cliquez sur l'onglet **SCP** .

3. Activez la case à cocher **Modifier le point de connexion de service** .

4. Sélectionnez **Supprimer le point de connexion de service actuel**, puis cliquez sur **OK**.

Surveillez maintenant l’activité de vos serveurs AD RMS, par exemple en vérifiant les [demandes dans le rapport d’intégrité système](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [table ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) ou [l’audit de l’accès utilisateur au contenu protégé](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). 

Après avoir confirmé que les clients RMS ne communiquent plus avec ces serveurs, et que les clients utilisent avec succès Azure Information Protection, vous pouvez supprimer le rôle serveur AD RMS de ces serveurs. Si vous utilisez des serveurs dédiés, vous pouvez prendre la précaution de les arrêter pendant un certain temps pour vous assurer qu’aucun problème n’est signalé, qui pourrait nécessiter un redémarrage de ces serveurs pour garantir la continuité de service pendant que vous étudiez la raison pour laquelle les clients n’utilisent pas Azure Information Protection.

Après avoir annulé l’approvisionnement de vos serveurs AD RMS, vous pouvez réviser vos modèles dans le portail Azure Classic et les consolider afin que les utilisateurs aient moins de choix, reconfigurer ces modèles ou même ajouter de nouveaux modèles. Il serait également judicieux de publier les modèles par défaut. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md).

>[!IMPORTANT]
> À la fin de cette migration, vous ne pouvez pas utiliser votre cluster AD RMS avec Azure Information Protection et l’option HYOK (Hold Your Own Key). Si vous décidez d’utiliser HYOK pour une étiquette Azure Information Protection en raison des redirections maintenant en place, le cluster AD RMS que vous utilisez doit avoir des URL de licences différentes de celles des clusters que vous avez migrés.

## <a name="step-11-remove-onboarding-controls"></a>Étape 11. Supprimer les contrôles d’intégration

Quand tous vos clients existants ont migré vers Azure Information Protection, il n’existe aucune raison de continuer à utiliser les contrôles d’intégration et gérer le groupe **AIPMigrated** que vous avez créé pour le processus de migration. 

Supprimez d’abord les contrôles d’intégration, puis vous pouvez supprimer le groupe **AIPMigrated** et toute tâche de déploiement de logiciel que vous avez créée pour déployer les redirections.

Pour supprimer les contrôles d’intégration :

1. Dans une session PowerShell, connectez-vous au service Azure Rights Management et indiquez vos informations d’identification d’administrateur général quand vous y êtes invité :

        Connect-Aadrmservice

2. Exécutez la commande suivante, puis entrez **O** pour confirmer :

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False

3. Vérifiez que les contrôles d’intégration ne sont plus définis :

        Get-AadrmOnboardingControlPolicy

    Dans la sortie, **Licence** doit indiquer **False** et aucun GUID n’est affiché pour **SecurityGroupOjbectId**

## <a name="step-12-re-key-your-azure-information-protection-tenant-key"></a>Étape 12. Renouvellement de votre clé de locataire Azure Information Protection
Cette étape est obligatoire une fois la migration terminée si votre déploiement AD RMS utilisait le mode de chiffrement RMS 1, car le renouvellement de clé crée une clé de locataire qui utilise le mode de chiffrement RMS 2. L'utilisation d'Azure RMS avec le mode de chiffrement 1 est prise en charge uniquement pendant le processus de migration.

Cette étape est facultative. Toutefois, nous la recommandons une fois la migration terminée, même si vous utilisiez le mode de chiffrement 2 RMS. Dans ce scénario, le renouvellement de clé permet de protéger votre clé de locataire Azure Information Protection contre des failles de sécurité potentielles de votre clé AD RMS.

Quand vous renouvelez votre clé de locataire Azure Information Protection (opération également appelée « déploiement de votre clé »), une nouvelle clé est créée et la clé d’origine est archivée. Toutefois, étant donné que le basculement d’une clé à l’autre ne se produit pas immédiatement mais sur plusieurs semaines, n’attendez pas de soupçonner une violation de votre clé d’origine, mais renouvelez votre clé de locataire Azure Information Protection dès la fin de la migration.

Pour renouveler votre clé de locataire Azure Information Protection :

- Si votre clé de locataire est gérée par Microsoft : contactez le [support Microsoft](../get-started/information-support.md#to-contact-microsoft-support) et ouvrez un **dossier de support Azure Information Protection dans lequel vous demandez le renouvellement de votre clé Azure Information Protection après une migration à partir d’AD RMS**. Vous devez prouver que vous êtes administrateur de votre locataire Azure Information Protection et comprendre que la confirmation de ce processus prend plusieurs jours. Des frais de prise en charge standard s’appliquent. Le renouvellement de votre clé de locataire n’est pas un service de support gratuit.

- Si vous gérez vous-même votre clé de locataire (BYOK) : dans Azure Key Vault, renouvelez la clé que vous utilisez pour votre locataire Azure Information Protection, puis réexécutez l’applet de commande [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) pour spécifier l’URL de nouvelle clé. 

Pour plus d’informations sur la gestion de votre clé de locataire Azure Information Protection, consultez [Opérations pour votre clé de locataire Azure Rights Management](../deploy-use/operations-tenant-key.md).

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez terminé la migration, passez en revue la [feuille de route de déploiement](deployment-roadmap.md) pour identifier les autres tâches de déploiement éventuellement nécessaires.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]