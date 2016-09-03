---
title: Installation de Windows PowerShell pour Azure Rights Management | Azure RMS
description: Utilisez les informations suivantes pour installer Windows PowerShell pour Microsoft Azure RMS.
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 0f22d69387b89a590b516d3a93148fec82b23acd


---

# Installation de Windows PowerShell pour Azure Rights Management

>*S’applique à : Azure Rights Management, Office 365*

Utilisez les informations suivantes pour installer Windows PowerShell pour Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS).

Vous pouvez utiliser ce module PowerShell pour administrer [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] à partir de la ligne de commande avec un ordinateur qui a une connexion Internet et qui remplit les conditions préalables répertoriées dans la section suivante. Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] prend en charge les scripts d’automatisation ou peut être nécessaire pour les scénarios de configuration avancée. Pour plus d’informations sur les tâches d’administration et les configurations prises en charge par le module, consultez [Administration d’Azure Rights Management à l’aide de Windows PowerShell](administer-powershell.md).

## Conditions préalables
Ce tableau répertorie les conditions préalables à l’installation et à l’utilisation de Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Une version de Windows qui prend en charge le module d’administration [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]|Vérifiez la liste des systèmes d’exploitation pris en charge dans la section **Configuration système** de la [page de téléchargement de l’outil d’administration Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Version minimale de Windows PowerShell : 2.0|Le module d’administration [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est pris en charge depuis Windows PowerShell 2.0.<br /><br />Par défaut, la plupart des systèmes d’exploitation Windows s’installent avec la version 2.0 de Windows PowerShell au minimum. Si vous avez besoin d’installer Windows PowerShell 2.0, voir [Installer Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx).<br /><br />Astuce : Vous pouvez vérifier la version de Windows PowerShell que vous exécutez en tapant `$PSVersionTable` dans une session PowerShell.|
|Version minimale du Microsoft .NET Framework : 4.5<br /><br />Remarque : Cette version du Microsoft .NET Framework étant fournie avec les systèmes d’exploitation de version plus récente, une installation manuelle ne devrait être nécessaire que si le système d’exploitation de votre client est antérieur à Windows 8.0, ou si celui de votre serveur est antérieur à Windows Server 2012.|Si la version minimale du Microsoft .NET Framework n’est pas installée, vous pouvez télécharger [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Cette version minimale du Microsoft .NET Framework est requise pour certaines des classes utilisées par le module d’administration [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|

> [!NOTE]
> À compter de la version 2.5.0.0 du module d’administration Rights Management, l’Assistant de connexion Microsoft Online Services n’est plus nécessaire.
> 
> Si une version précédente du module d’administration Rights Management est installée, utilisez **Programmes et fonctionnalités** pour désinstaller **Administration de Microsoft Azure AD Rights Management** avant d’installer la version la plus récente.


## Comment installer le module d’administration de la Gestion des droits

1.  Accédez au Centre de téléchargement Microsoft et [téléchargez l’outil d’administration Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721), qui contient le module d’administration [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] pour Windows PowerShell.

2.  À partir du dossier local dans lequel vous avez téléchargé et enregistré le fichier d’installation [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], double-cliquez sur le fichier exécutable que vous avez téléchargé pour votre plateforme (WindowsAzureADRightsManagementAdministration_x64 ou WindowsAzureADRightsManagementAdministration_x86.exe) pour lancer l’Assistant Installation de l’administration Azure AD Rights Management.

3.  Effectuez toutes les étapes de l'Assistant.

Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] est maintenant installé.

## Étapes suivantes
Pour savoir quelles applets de commande sont disponibles, démarrez Windows PowerShell avec l’option **Exécuter en tant qu’administrateur** et tapez ce qui suit :

```
Get-Command -Module aadrm
```
Utilisez la commande `the Get-Help <cmdlet_name>` pour afficher l’aide d’une applet de commande particulière.

Pour plus d’informations :

-   Liste complète des applets de commande disponibles : [Applets de commande d’Azure Rights Management](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Liste des principaux scénarios de configuration prenant en charge Windows PowerShell : [Administration d’Azure Rights Management à l’aide de Windows PowerShell](administer-powershell.md)

Avant de pouvoir exécuter des commandes pour configurer le service [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], vous devez vous connecter au service à l’aide de l’applet de commande [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) . Lorsque vous avez terminé l’exécution des commandes de configuration souhaitées, déconnectez le service à l’aide de l’applet de commande [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) .

> [!NOTE]
> Si vous n’avez pas encore activé [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], vous pouvez le faire une fois connecté au service, à l’aide de l’applet de commande [Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) .

## Voir aussi
[Administration d’Azure Rights Management à l'aide de Windows PowerShell](administer-powershell.md)



<!--HONumber=Aug16_HO4-->


