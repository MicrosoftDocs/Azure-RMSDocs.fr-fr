---
title: Installer PowerShell pour AADRM - AIP
description: Instructions d’installation de Windows PowerShell pour le service Azure Rights Management d’Azure Information Protection. Le nom de ce module est AADRM.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d061a7e65bce1e5072e4e06fd3ed1ef2132810c8
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="installing-the-aadrm-powershell-module"></a>Installation du module PowerShell AADRM

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Pour installer le module Windows PowerShell pour le service Azure Rights Management à partir Azure Information Protection, aidez-vous des informations suivantes. Le nom de ce module est AADRM.

Vous pouvez utiliser ce module PowerShell pour administrer le service Azure Rights Management à partir de la ligne de commande avec un ordinateur qui a une connexion Internet et qui remplit les conditions préalables répertoriées dans la section suivante. Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] prend en charge les scripts d’automatisation ou peut être nécessaire pour les scénarios de configuration avancée. Pour plus d’informations sur les tâches d’administration et les configurations prises en charge par le module, consultez [Administration d’Azure Rights Management à l’aide de Windows PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prérequis
Le tableau ci-dessous répertorie les prérequis pour l’installation et l’utilisation du module PowerShell AADRM pour le service Azure Rights Management à partir d’Azure Information Protection.

|Condition requise|Autres informations|
|---------------|--------------------|
|Version minimale de Windows PowerShell : 3.0|Vous pouvez vérifier la version de Windows PowerShell que vous exécutez en tapant `$PSVersionTable` dans une session PowerShell. <br /><br /> Si vous devez installer une version ultérieure de Windows PowerShell, consultez [Mise à niveau de la version Windows PowerShell existante](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Version minimale du Microsoft .NET Framework : 4.5<br /><br />Remarque : Cette version du Microsoft .NET Framework étant fournie avec les systèmes d’exploitation de version plus récente, une installation manuelle ne devrait être nécessaire que si le système d’exploitation de votre client est antérieur à Windows 8.0, ou si celui de votre serveur est antérieur à Windows Server 2012.|Si la version minimale du Microsoft .NET Framework n’est pas installée, vous pouvez télécharger [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Cette version minimale du Microsoft .NET Framework est requise pour certaines des classes utilisées par le module d’administration AADRM.|

> [!NOTE]
> À compter de la version 2.5.0.0 du module AADRM, l’Assistant de connexion Microsoft Online Services n’est plus nécessaire.
> 
> Si une version précédente du module AADRM est installée, utilisez **Programmes et fonctionnalités** pour désinstaller **Administration de Microsoft Azure AD Rights Management** avant d’installer la version la plus récente.


## <a name="how-to-install-the-aadrm-module"></a>Comment installer le module AADRM

Le module AADRM a été déplacé dans [PowerShell Gallery](/powershell/gallery/readme), mais il est également disponible, pour une durée limitée, dans le Centre de téléchargement Microsoft. 

### <a name="to-install-the-aadrm-module-from-the-powershell-gallery"></a>Pour installer le module AADRM à partir de PowerShell Gallery

Si vous n’avez jamais utilisé PowerShell Gallery, consultez [Bien démarrer avec PowerShell](/powershell/gallery/psgallery/psgallery_gettingstarted). Suivez les instructions relatives à la configuration requise de la galerie, avec notamment l’installation du module PowerShellGet et du fournisseur NuGet.

Pour consulter des informations détaillées sur le module AADRM dans PowerShell Gallery, visitez la [page AADRM](https://www.powershellgallery.com/packages/AADRM).

Pour installer le module AADRM, démarrez une session PowerShell et tapez :

    Install-Module -Name AADRM


### <a name="to-install-the-aadrm-module-from-the-microsoft-download-center"></a>Pour installer le module AADRM à partir du Centre de téléchargement Microsoft

1. Accédez au Centre de téléchargement Microsoft et localisez [l’outil d’administration Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721), qui contient le module d’administration [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] pour Windows PowerShell.

2. Téléchargez et enregistrez le fichier du programme d’installation [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], **WindowsAzureADRightsManagementAdministration_x64**. Puis double-cliquez sur ce fichier pour lancer l’Assistant Installation de l’administration Azure AD Rights Management.

3.  Effectuez toutes les étapes de l'Assistant. Celui-ci installe le module PowerShell AADRM.

## <a name="next-steps"></a>Étapes suivantes
Dans une session Windows PowerShell, confirmez la version du module installé. Cette vérification est particulièrement importante si vous avez mis à niveau à partir d’une version antérieure :

```
(Get-Module AADRM –ListAvailable).Version
```

Remarque : si cette commande échoue, exécutez d’abord **Import-Module AADRM**.

Pour voir les applets de commande disponibles, tapez la commande suivante :

```
Get-Command -Module AADRM
```

Utilisez la commande `Get-Help <cmdlet_name>` pour afficher l’aide relative à une applet de commande spécifique, et utilisez le paramètre **-online** pour afficher l’aide la plus récente sur le site de la documentation de Microsoft. Par exemple :

```
Get-Help Connect-AadrmService -online
```

Pour plus d’informations :

-   Liste complète des applets de commande disponibles : [Module AADRM](/powershell/aadrm/vlatest/rightsmanagement)

-   Liste des principaux scénarios de configuration prenant en charge PowerShell : [Administration d’Azure Rights Management à l’aide de Windows PowerShell](administer-powershell.md)

Avant de pouvoir exécuter des commandes pour configurer le service [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], vous devez vous connecter au service à l’aide de l’applet de commande [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice). Lorsque vous avez terminé l’exécution de vos commandes de configuration, nous vous conseillons de vous déconnecter du service à l’aide de l’applet de commande [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice). Si vous ne vous déconnectez pas, la connexion est interrompue automatiquement après une période d’inactivité. En raison du comportement de déconnexion automatique, vous constaterez que vous devrez occasionnellement vous reconnecter à une session PowerShell. 

> [!NOTE]
> Si le service Azure Rights Management n’est pas encore activé, vous pouvez le faire une fois connecté au service, à l’aide de l’applet de commande [Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]