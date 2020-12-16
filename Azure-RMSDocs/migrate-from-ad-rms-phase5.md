---
title: Migrer un déploiement AD RMS vers Azure Information Protection - Phase 5
description: Phase 5 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 10 à 12 de la migration d’AD RMS vers Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: f4ae6c5addbea7293192b085bade9f17b798c23c
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583589"
---
# <a name="migration-phase-5---post-migration-tasks"></a>Phase de migration 5 : Tâches de post-migration

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Utilisez les informations suivantes pour la Phase 5 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 10 à 12 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-10-deprovision-ad-rms"></a>Étape 10. Déprovisionner AD RMS

supprimez le point de connexion de service d'Active Directory pour empêcher des ordinateurs de découvrir votre infrastructure Rights Management locale. Ceci est facultatif pour les clients existants que vous migrez en raison de la redirection que vous avez configurée dans le Registre (par exemple en exécutant le script de migration). Cependant, la suppression du point de connexion de service empêche les nouveaux clients, et potentiellement les outils et les services RMS, de trouver le point de connexion de service quand la migration est terminée. À ce stade, toutes les connexions doivent accéder au service Azure Rights Management.

Pour supprimer le point de connexion de service, assurez-vous que vous êtes connecté en tant qu’administrateur d’entreprise de domaine, puis procédez comme suit :

1. Dans la console Active Directory Rights Management Services, cliquez sur le cluster AD RMS, puis cliquez sur **Propriétés**.

2. Cliquez sur l'onglet **Point de connexion de service**.

3. Cochez la case **Modifier le point de connexion de service**.

4. Sélectionnez **Supprimer le point de connexion de service actuel**, puis cliquez sur **OK**.

Surveillez à présent l’activité de vos serveurs AD RMS. Par exemple, vérifiez [les demandes dans le rapport sur l’intégrité du système](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee221012(v=ws.10)), [la table ServiceRequest](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772686(v=ws.10)) ou [l’audit de l’accès utilisateur au contenu protégé](https://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx).

Après avoir confirmé que les clients RMS ne communiquent plus avec ces serveurs et que les clients utilisent avec succès Azure Information Protection, vous pouvez supprimer le rôle serveur AD RMS de ces serveurs. Si vous utilisez des serveurs dédiés, vous préférerez peut-être la première étape de l’arrêt des serveurs pendant un certain temps. Cela vous donne le temps de confirmer l’absence de problèmes qui pourraient vous obliger à redémarrer ces serveurs pour garantir la continuité de service pendant que vous étudiez la raison pour laquelle les clients n’utilisent pas Azure Information Protection.

Une fois que yo a désapprovisionné vos serveurs AD RMS, vous pouvez choisir de passer en revue votre modèle et vos étiquettes. Par exemple, convertissez les modèles en étiquettes, consolidez-les afin que les utilisateurs aient moins de choix, ou reconfigurez-les. Il s’agit également d’un bon moment pour publier les modèles par défaut.

Pour les étiquettes de sensibilité et le client d’étiquetage unifié, utilisez le centre d’administration d’étiquetage, y compris le centre de sécurité Microsoft 365, le centre de conformité Microsoft 365, ou le centre de conformité Microsoft 365 Security &. Pour plus d’informations, consultez la documentation Microsoft 365.

Si vous utilisez le client classique, utilisez la Portail Azure. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](./configure-policy-templates.md).

>[!IMPORTANT]
> À la fin de cette migration, votre cluster AD RMS ne peut pas être utilisé avec Azure Information Protection et l’option conserver votre propre clé ([hyok](configure-adrms-restrictions.md)). Si vous utilisez le client classique avec HYOK, en raison des redirections qui sont maintenant en place, le cluster AD RMS que vous utilisez doit avoir des URL de licence différentes de celles des clusters que vous avez migrés.

### <a name="additional-configuration-for-computers-that-run-office-2010"></a>Configuration supplémentaire pour les ordinateurs qui exécutent Office 2010

Si les clients migrés exécutent Office 2010, les utilisateurs peuvent rencontrer des retards lors de l’ouverture de contenu protégé après l’annulation de l’approvisionnement de nos serveurs de AD RMS. Les utilisateurs peuvent également voir des messages indiquant qu’ils n’ont pas d’informations d’identification pour ouvrir du contenu protégé. Pour résoudre ces problèmes, créez une redirection réseau pour ces ordinateurs, qui redirige le AD RMS nom de domaine complet de l’URL vers l’adresse IP locale de l’ordinateur (127.0.0.1). Pour ce faire, vous pouvez configurer le fichier des hôtes locaux sur chaque ordinateur ou à l’aide de DNS.

Redirection par le biais du fichier d’hôte local :

- Ajoutez la ligne suivante dans le fichier local hosts, en remplaçant `<AD RMS URL FQDN>` par la valeur de votre cluster AD RMS, sans préfixes ni pages Web :

    ```sh
    127.0.0.1 <AD RMS URL FQDN>
    ```

Redirection via DNS :

- Créez un nouvel enregistrement d’hôte (A) pour votre AD RMS nom de domaine complet de l’URL, dont l’adresse IP est 127.0.0.1.

Pour plus d’informations sur AIP et Office 2010, consultez [AIP pour Windows et versions d’Office dans support étendu](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).
## <a name="step-11-complete-client-migration-tasks"></a>Étape 11. Effectuer les tâches de migration des clients

Pour les clients d’appareils mobiles et les ordinateurs Mac : Supprimez les enregistrements SRV DNS que vous avez créés lors du déploiement de l’[extension d’appareil mobile AD RMS](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11)).

Une fois ces modifications DNS propagées, ces clients découvrent et commencent automatiquement à utiliser le service Azure Rights Management. Toutefois, les ordinateurs Mac qui exécutent Office Mac mettent en cache les informations d’AD RMS. Pour ces ordinateurs, ce processus peut prendre jusqu’à 30 jours.

Pour forcer les ordinateurs Mac à exécuter immédiatement le processus de découverte, dans le trousseau, recherchez « adal » et supprimez toutes les entrées ADAL. Ensuite, exécutez les commandes suivantes sur ces ordinateurs :

````sh

rm -r ~/Library/Cache/MSRightsManagement

rm -r ~/Library/Caches/com.microsoft.RMS-XPCService

rm -r ~/Library/Caches/Microsoft\ Rights\ Management\ Services

rm -r ~/Library/Containers/com.microsoft.RMS-XPCService

rm -r ~/Library/Containers/com.microsoft.RMSTestApp

rm ~/Library/Group\ Containers/UBF8T346G9.Office/DRM.plist

killall cfprefsd

````

Quand tous vos ordinateurs Windows existants ont migré vers Azure Information Protection, il n’y a aucune raison de continuer à utiliser les contrôles d’intégration et à conserver le groupe **AIPMigrated** que vous avez créé pour le processus de migration.

Supprimez d’abord les contrôles d’intégration, puis éventuellement le groupe **AIPMigrated** et toute méthode de déploiement de logiciels que vous avez créée pour déployer les scripts de migration.

Pour supprimer les contrôles d’intégration :

1. Dans une session PowerShell, connectez-vous au service Azure Rights Management et indiquez vos informations d’identification d’administrateur général quand vous y êtes invité :

    ```PowerShell
    Connect-AipService

2. Run the following command, and enter **Y** to confirm:

    ```PowerShell
    Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
    ```

    Notez que cette commande supprime toute application de licence pour le service de protection Azure Rights Management, et ce pour que tous les ordinateurs puissent protéger les documents et les e-mails.

3. Vérifiez que les contrôles d’intégration ne sont plus définis :

    ```PowerShell    
    Get-AipServiceOnboardingControlPolicy
    ```

    Dans la sortie, **Licence** doit indiquer **False** et aucun GUID n’est affiché pour **SecurityGroupOjbectId**

Enfin, si vous utilisez Office 2010 et que vous avez activé la tâche de **gestion des modèles de stratégie de droits AD RMS (automatique)** dans la bibliothèque du Planificateur de tâches Windows, désactivez cette tâche parce qu’elle n’est pas utilisée par le client Azure Information Protection. 

Cette tâche est généralement activée par l’utilisation d’une stratégie de groupe et prend en charge un déploiement AD RMS. Cette tâche se trouve à l’emplacement suivant : **Microsoft**  >  **Windows**  >  **services AD RMS (Active Directory Rights Management Services) client**. 

Pour plus d’informations, consultez [AIP pour Windows et les versions d’Office dans support étendu](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>Étape 12. Renouveler votre clé de locataire Azure Information Protection

Cette étape est requise une fois la migration terminée si votre déploiement de AD RMS utilise le mode de chiffrement RMS 1, car ce mode utilise une clé 1024 bits et SHA-1. Cette configuration est considérée comme offrant un niveau de protection inadéquat. Microsoft n’approuve pas l’utilisation de longueurs de clé inférieures telles que les clés RSA 1024 bits et l’utilisation associée de protocoles qui offrent des niveaux de protection inadéquats, tels que SHA-1.

La régénération de clés entraîne une protection qui utilise le mode de chiffrement RMS 2, qui génère une clé 2048 bits et SHA-256.

Même si votre déploiement AD RMS utilisait le mode de chiffrement 2, nous vous recommandons d’effectuer cette étape dans la mesure où une nouvelle clé contribue à protéger votre locataire contre d’éventuelles infractions à la sécurité de votre clé AD RMS.

Quand vous renouvelez votre clé de locataire Azure Information Protection (opération également appelée « déploiement de votre clé »), la clé active est archivée et Azure Information Protection commence à utiliser une autre clé que vous spécifiez. Cette autre clé peut être une nouvelle clé que vous créez dans Azure Key Vault ou la clé par défaut qui a été automatiquement créée pour votre locataire.

Le passage d’une clé à l’autre ne se produit pas immédiatement mais sur plusieurs semaines. Pour cette raison, n’attendez pas de soupçonner une violation de votre clé d’origine, mais effectuez cette étape dès la fin de la migration.

Pour renouveler votre clé de locataire Azure Information Protection :

- **Si votre clé de locataire est gérée par Microsoft**: exécutez l’applet de commande PowerShell [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) et spécifiez l’identificateur de clé pour la clé qui a été créée automatiquement pour votre locataire. Vous pouvez identifier la valeur à spécifier en exécutant l’applet de commande [AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) . La clé créée automatiquement pour votre locataire a la date de création la plus ancienne. Vous pouvez donc l’identifier à l’aide de la commande suivante :

        
    ```PowerShell
    (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1
    ```

- **Si votre clé de locataire est gérée par vous (BYOK)**: dans Azure Key Vault, répétez votre processus de création de clé pour votre locataire Azure information protection, puis exécutez à nouveau l’applet de commande [use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) pour spécifier l’URI de cette nouvelle clé.

Pour plus d’informations sur la gestion de votre clé de locataire Azure Information Protection, consultez [Opérations pour votre clé de locataire Azure Information Protection](./operations-tenant-key.md).


## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez terminé la migration, consultez la feuille [de route pour le déploiement d’AIP pour la classification, l’étiquetage et la protection](deployment-roadmap-classify-label-protect.md) afin d’identifier les autres tâches de déploiement que vous devrez peut-être faire.
