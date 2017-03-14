---
title: "Migrer un déploiement AD RMS vers Azure Information Protection - Phase 4"
description: "Phase 4 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 8 et 9 de la migration d’AD RMS vers Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d36f47e586ac1295dcc79e43a9e061b4c7c7fe1e
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="migration-phase-4---post-migration-tasks"></a>Phase de migration 4 - Tâches de post-migration

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*


Utilisez les informations suivantes pour la Phase 4 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 8 et 9 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-8-decommission-ad-rms"></a>Étape 8. Désaffecter AD RMS

Supprimez le point de connexion de service d'Active Directory pour empêcher des ordinateurs de découvrir votre infrastructure Rights Management locale. Ceci est facultatif pour les clients existants que vous migrez en raison de la redirection que vous avez configurée dans le Registre (par exemple en exécutant le script de migration). Cependant, la suppression du point de connexion de service empêche les nouveaux clients, et potentiellement les outils et les services RMS, de trouver le point de connexion de service quand la migration est terminée et que toutes les connexions doivent accéder au service Azure Rights Management. 

Pour supprimer le point de connexion de service, assurez-vous que vous êtes connecté en tant qu’administrateur d’entreprise de domaine, puis procédez comme suit :

1. Dans la console Active Directory Rights Management Services, cliquez sur le cluster AD RMS, puis cliquez sur **Propriétés**.

2. Cliquez sur l'onglet **SCP** .

3. Activez la case à cocher **Modifier le point de connexion de service** .

4. Sélectionnez **Supprimer le point de connexion de service actuel**, puis cliquez sur **OK**.

Surveillez l’activité de vos serveurs AD RMS, par exemple, en vérifiant [les demandes dans le rapport d’intégrité système](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [Table ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) ou [l’audit de l’accès utilisateur au contenu protégé](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Après avoir confirmé que les clients RMS ne communiquent plus avec ces serveurs, et que les clients utilisent avec succès Azure Information Protection, vous pouvez supprimer le rôle serveur AD RMS de ces serveurs. Si vous utilisez des serveurs dédiés, vous pouvez prendre la précaution de les arrêter pendant un certain temps pour vous assurer qu’aucun problème n’est signalé, qui pourrait nécessiter un redémarrage de ces serveurs pour garantir la continuité de service pendant que vous étudiez la raison pour laquelle les clients n’utilisent pas Azure Information Protection.

Après la désaffectation de vos serveurs AD RMS, vous pouvez réviser vos modèles dans le portail Azure Classic et les consolider afin que les utilisateurs aient moins de choix, les reconfigurer ou même ajouter de nouveaux modèles. Il serait également judicieux de publier les modèles par défaut. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md).

## <a name="step-9-re-key-your-azure-information-protection-tenant-key"></a>Étape 9. Renouvellement de votre clé de locataire Azure Information Protection
Cette étape est obligatoire une fois la migration terminée si votre déploiement AD RMS utilisait le mode de chiffrement RMS 1, car le renouvellement de clé crée une clé de locataire qui utilise le mode de chiffrement RMS 2. L'utilisation d'Azure RMS avec le mode de chiffrement 1 est prise en charge uniquement pendant le processus de migration.

Cette étape est facultative. Toutefois, nous la recommandons une fois la migration terminée, même si vous utilisiez le mode de chiffrement 2 RMS. Dans ce scénario, le renouvellement de clé permet de protéger votre clé de locataire Azure Information Protection contre des failles de sécurité potentielles de votre clé AD RMS.

Quand vous renouvelez votre clé de locataire Azure Information Protection (opération également appelée « déploiement de votre clé »), une nouvelle clé est créée et la clé d’origine est archivée. Toutefois, étant donné que le basculement d’une clé à l’autre ne se produit pas immédiatement mais sur plusieurs semaines, n’attendez pas de soupçonner une violation de votre clé d’origine, mais renouvelez votre clé de locataire Azure Information Protection dès la fin de la migration.

Pour renouveler votre clé de locataire Azure Information Protection :

- Si votre clé de locataire est gérée par Microsoft : contactez le [support Microsoft](../get-started/information-support.md#to-contact-microsoft-support) et ouvrez un **dossier de support Azure Information Protection dans lequel vous demandez le renouvellement de votre clé Azure Information Protection après une migration à partir d’AD RMS**. Vous devez prouver que vous êtes administrateur de votre locataire Azure Information Protection et comprendre que la confirmation de ce processus prend plusieurs jours. Des frais de prise en charge standard s’appliquent. Le renouvellement de votre clé de locataire n’est pas un service de support gratuit.

- Si vous gérez vous-même votre clé de locataire (BYOK) : dans Azure Key Vault, renouvelez la clé que vous utilisez pour votre locataire Azure Information Protection, puis réexécutez la cmdlet [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) pour spécifier l’URL de nouvelle clé. 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la gestion de votre clé de locataire Azure Information Protection, consultez [Opérations pour votre clé de locataire Azure Rights Management](../deploy-use/operations-tenant-key.md).

Maintenant que vous avez terminé la migration, passez en revue la [feuille de route de déploiement](deployment-roadmap.md) pour identifier les autres tâches de déploiement éventuellement nécessaires.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
