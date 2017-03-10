---
title: "Migrer une clé protégée par logiciel vers une autre clé protégée par logiciel - AIP"
description: "Instructions qui font partie du chemin de migration d’AD RMS vers Azure Information Protection. Celles-ci s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par logiciel."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: dfdea977819434cc4a6d164fecb5727a22fca26f
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Étape 2 : Migration de clé protégée par logiciel à clé protégée par logiciel

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). Elles s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par logiciel. 

Si ce n’est pas votre scénario de configuration choisi, revenez à l’[Étape 2. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) et choisissez une configuration différente.

La procédure suivante permet d’importer la configuration AD RMS dans Azure Information Protection pour que votre clé de locataire Azure Information Protection soit gérée par Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Pour importer les données de configuration dans Azure Information Protection

1.  Sur une station de travail connectée à Internet, téléchargez et installez le module Windows PowerShell pour Azure Rights Management (version minimale 2.5.0.0), qui comprend l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx). Le service Azure Rights Management (Azure RMS) fournit le service de protection pour Azure Information Protection.

    > [!TIP]
    > Si vous avez précédemment téléchargé et installé le module, vérifiez le numéro de version en exécutant la commande suivante : `(Get-Module aadrm -ListAvailable).Version`

    Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2.  Démarrez Windows PowerShell avec l'option **Exécuter en tant qu'administrateur**, puis utilisez l'applet de commande [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) pour vous connecter au service Azure RMS :

    ```
    Connect-AadrmService
    ```
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur client [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (en général, vous utilisez un compte d’administrateur global pour Azure Active Directory ou Office 365).

3.  Utilisez l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) pour charger le premier fichier (.xml) de domaine de publication approuvé exporté. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté que vous voulez utiliser avec Azure Information Protection pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    Vous pouvez utiliser [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) ou [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) pour spécifier le mot de passe sous forme de chaîne sécurisée. Si vous utilisez ConvertTo-SecureString et que votre mot de passe contient des caractères spéciaux, entre ce dernier entre deux apostrophes ou utilisez des caractères d’échappement.
    
    Par exemple, commencez par exécuter la commande **$TPD_Password = Read-Host -AsSecureString**, puis entrez le mot de passe spécifié précédemment. Ensuite, exécutez la commande **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**. Lorsque vous y êtes invité, confirmez que vous souhaitez effectuer cette action.
    
4.  Une fois la commande terminée, répétez l’étape 3 pour chaque fichier .xml restant que vous avez créé en exportant vos domaines de publication approuvés. Par exemple, vous devez disposer d’au moins un fichier supplémentaire à importer si vous avez mis à niveau votre cluster AD RMS pour le Mode de chiffrement 2. Toutefois, pour ces fichiers, définissez **-Active** avec la valeur **false** quand vous exécutez la commande Import. Par exemple : **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

5.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) pour vous déconnecter du service Azure Rights Management :

    ```
    Disconnect-AadrmService
    ```


Vous êtes maintenant prêt à passer à l’[Étape 3. Activez votre locataire Azure Information Protection](migrate-from-ad-rms-phase1.md#step-3-activate-your-azure-information-protection-tenant).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

