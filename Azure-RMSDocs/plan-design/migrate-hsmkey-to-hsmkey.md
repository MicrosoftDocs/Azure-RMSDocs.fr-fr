---
# required metadata

title: Étape 2 : Migration de clé protégée par HSM à clé protégée par HSM | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Étape 2 : Migration de clé protégée par HSM à clé protégée par HSM

Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), et s’appliquent uniquement si votre clé AD RMS est protégée par HSM et que vous souhaitez procéder à la migration vers Azure Rights Management avec une clé de locataire protégée par HSM. 

Si ce n’est pas votre scénario de configuration choisi, revenez à l’[Étape 2. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) et choisissez une configuration différente.

> [!NOTE]
> Ces instructions supposent que votre clé AD RMS est protégée par module. C’est le cas habituel. Si votre clé AD RMS est protégée par OCS, contactez [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key) avant de suivre ces instructions.

Cette procédure en deux parties permet d'importer votre clé HSM et la configuration d'AD RMS dans Azure RMS pour que votre clé de client Azure RMS soit gérée par vous (scénario BYOK).

Vous devez d'abord empaqueter votre clé HSM pour la préparer au transfert vers Azure RMS, puis l'importer avec les données de configuration.

## Partie 1 : empaquetage et transfert de votre clé HSM vers Azure RMS

1.  Suivez les étapes de la section [Implémentation de la solution Bring Your Own Key (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de la rubrique [Planification et implémentation de votre clé de locataire Azure Rights Management](plan-implement-tenant-key.md), à l’aide de la procédure **Générer et transférer votre clé de locataire par Internet** avec les exceptions suivantes :

    -   Ne suivez pas la procédure de **Génération de la clé de client**, car vous avez déjà l'équivalent de votre déploiement AD RMS. Vous devez identifier la clé utilisée par votre serveur AD RMS dans l'installation Thales, et utiliser cette clé lors de la migration. Les fichiers de clé chiffrés Thales sont généralement nommés **key_(keyAppName)_(keyIdentifier)** localement sur le serveur.

    -   Ne suivez pas la procédure de **Transfert de votre clé de locataire vers Azure RMS**, qui utilise la commande Add-AadrmKey.  Au lieu de cela, vous transférerez la clé HSM que vous avez préparée lors du téléchargement du domaine de publication approuvé exporté à l'aide de la commande Import-AadrmTpd.

2.  Sur la station de travail connectée à Internet, dans la session Windows PowerShell, reconnectez-vous au service Azure RMS.

Maintenant que vous avez préparé votre clé HSM pour Azure RMS, vous êtes prêt à importer votre fichier de clé HSM et les données de configuration d'AD RMS.

## Partie 2 : importation de la clé HSM et des données de configuration dans Azure RMS

1.  Toujours sur la station de travail connectée à Internet et dans la session Windows PowerShell, téléchargez le premier fichier (.xml) de domaine de publication approuvé exporté. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté correspondant à la clé HSM que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Par exemple : **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

2.  Une fois la commande exécutée, répétez l'étape 1 pour chaque fichier .xml que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, affectez la valeur **false** à **-Active** lors de l’exécution de la commande Import.  Par exemple : **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```

Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre locataire RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO3-->


