---
# required metadata

title: Étape 2 : Migration de clé protégée par logiciel à clé protégée par logiciel | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Étape 2 : Migration de clé protégée par logiciel à clé protégée par logiciel

Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), et s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Rights Management avec une clé de locataire protégée par logiciel. 

Si ce n’est pas votre scénario de configuration choisi, revenez à l’[Étape 2. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) et choisissez une configuration différente.

La procédure suivante permet d’importer la configuration d’AD RMS dans Azure RMS pour que votre clé de locataire Azure RMS soit gérée par Microsoft.

## Pour importer les données de configuration dans Azure RMS

1.  Sur une station de travail connectée à Internet, téléchargez et installez le module Windows PowerShell pour Azure RMS (version minimale 2.1.0.0), qui comprend l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Si vous avez précédemment téléchargé et installé le module, vérifiez le numéro de version en exécutant la commande suivante : `(Get-Module aadrm -ListAvailable).Version`

    Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2.  Démarrez Windows PowerShell avec l'option **Exécuter en tant qu'administrateur** , puis utilisez l'applet de commande [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) pour vous connecter au service Azure RMS :

    ```
    Connect-AadrmService
    ```
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur client [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (en général, vous utiliserez un compte d’administrateur global pour Azure Active Directory ou Office 365).

3.  Utilisez l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) pour charger le premier fichier (.xml) de domaine de publication approuvé exporté. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Par exemple : **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

4.  Une fois la commande exécutée, répétez l'étape 3 pour chaque fichier .xml que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, affectez la valeur **false** à **-Active** lors de l’exécution de la commande Import. Par exemple : **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```

Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre locataire RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO3-->


