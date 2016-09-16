---
title: "Étape 2 &colon; Migration de clé protégée par logiciel à clé protégée par logiciel | Azure RMS"
description: "Instructions qui font partie du chemin de migration d’AD RMS vers Azure Rights Management. Celles-ci s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Rights Management avec une clé de locataire protégée par logiciel."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: 5ec3d2b275521807c6fd8f9ccfe1136db97d5d79


---


# Étape 2 : Migration de clé protégée par logiciel à clé protégée par logiciel

>*S’applique à : Active Directory Rights Management Services, Azure Rights Management*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), et s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Rights Management avec une clé de locataire protégée par logiciel. 

Si ce n’est pas votre scénario de configuration choisi, revenez à l’[Étape 2. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) et choisissez une configuration différente.

La procédure suivante permet d’importer la configuration d’AD RMS dans Azure RMS pour que votre clé de locataire Azure RMS soit gérée par Microsoft.

## Pour importer les données de configuration dans Azure RMS

1.  Sur une station de travail connectée à Internet, téléchargez et installez le module Windows PowerShell pour Azure RMS (version minimale 2.5.0.0), qui comprend l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Si vous avez précédemment téléchargé et installé le module, vérifiez le numéro de version en exécutant la commande suivante : `(Get-Module aadrm -ListAvailable).Version`

    Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2.  Démarrez Windows PowerShell avec l'option **Exécuter en tant qu'administrateur** , puis utilisez l'applet de commande [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) pour vous connecter au service Azure RMS :

    ```
    Connect-AadrmService
    ```
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur client [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (en général, vous utilisez un compte d’administrateur global pour Azure Active Directory ou Office 365).

3.  Utilisez l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) pour charger le premier fichier (.xml) de domaine de publication approuvé exporté. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Par exemple : **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

4.  Une fois la commande terminée, répétez l’étape 3 pour chaque fichier .xml restant que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, définissez **-Active** avec la valeur **false** quand vous exécutez la commande Import. Par exemple : **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```


Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre client RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).





<!--HONumber=Aug16_HO4-->


