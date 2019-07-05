---
title: Installer le module AIPService PowerShell pour Azure Information Protection
description: Instructions pour installer PowerShell pour le service de protection d’Azure Information Protection. Le nom de ce module est AIPService.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d6f5ccc34669781f4ec9723014d5254444255649
ms.sourcegitcommit: 849c493cef6b2578945c528f4e17373a2ef26287
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67563402"
---
# <a name="installing-the-aipservice-powershell-module"></a>Installation du module PowerShell AIPService

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations suivantes pour vous aider à installer le module Windows PowerShell pour le service de protection d’Azure Information Protection. Le nom de ce module est AIPService, et il remplace la version précédente qui a été nommée AADRM.

Vous pouvez utiliser ce module PowerShell pour administrer le service de protection (Azure Rights Management) à partir de la ligne de commande à l’aide de n’importe quel ordinateur doté d’une connexion Internet et qui remplit les conditions préalables répertoriées dans la section suivante. PowerShell de Windows pour Azure Information Protection prend en charge les scripts d’automatisation ou peut être nécessaire pour les scénarios de configuration avancée. Pour plus d’informations sur les tâches d’administration et les configurations qui prend en charge par le module, consultez [administration protection d’Azure Information Protection à l’aide de PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prérequis
Ce tableau répertorie les conditions préalables pour installer et utiliser le module PowerShell de AIPService pour le service de protection d’Azure Information Protection.

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Version minimale de Windows PowerShell : 3.0|Vous pouvez vérifier la version de Windows PowerShell que vous exécutez en tapant `$PSVersionTable` dans une session PowerShell. <br /><br /> Si vous devez installer une version ultérieure de Windows PowerShell, consultez [Mise à niveau de la version Windows PowerShell existante](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Version minimale du Microsoft .NET Framework : 4.5<br /><br />Remarque : Cette version de Microsoft .NET Framework étant fournie avec les systèmes d’exploitation ultérieures, vous devez l’installer manuellement uniquement si votre système d’exploitation de client est inférieure à Windows 8.0 ou votre système d’exploitation de serveur est antérieur à Windows Server 2012.|Si la version minimale du Microsoft .NET Framework n’est pas installée, vous pouvez télécharger [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Cette version minimale du Microsoft .NET Framework est requise pour certaines des classes qui utilise le module AIPService.|

## <a name="if-you-have-the-aadrm-module-installed"></a>Si vous avez installé le module AADRM

Le module AIPService remplace le module plus anciens, AADRM. Si vous avez installé le module plus anciens, désinstallez-le, puis installez le module AIPService.

Le nouveau module dispose d’alias pour les noms d’applet de commande dans le module plus anciens afin que tous les scripts existants continueront de fonctionner. Toutefois, envisagez de mettre à jour ces références avant de l’ancien module n’est plus prise en charge. Prise en charge pour le module AADRM prendra fin le 15 juillet 2020.

Si vous avez installé le module AADRM à partir de PowerShell Gallery, pour le désinstaller, démarrez une session PowerShell avec le **exécuter en tant qu’administrateur** option, puis tapez :

    Uninstall-Module -Name AADRM

Si vous avez installé le module AADRM avec l’outil d’Administration Azure Rights Management, utilisez **programmes et fonctionnalités** pour désinstaller **Administration de Windows Azure AD Rights Management**.

## <a name="how-to-install-the-aipservice-module"></a>Comment installer le module AIPService

Le module AIPService se trouve sur le [PowerShell Gallery](/powershell/gallery/readme) et n’est pas disponible à partir du Microsoft Download Center. 

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>Pour installer le module AIPService à partir de PowerShell Gallery

Si vous n’avez jamais utilisé PowerShell Gallery, consultez [Bien démarrer avec PowerShell](/powershell/gallery/psgallery/psgallery_gettingstarted). Suivez les instructions relatives à la configuration requise de la galerie, avec notamment l’installation du module PowerShellGet et du fournisseur NuGet.

Pour afficher des détails sur le module AIPService dans PowerShell Gallery, visitez le [AIPService page](https://www.powershellgallery.com/packages/AIPService).

Pour installer le module AIPService, démarrez une session PowerShell avec le **exécuter en tant qu’administrateur** option, puis tapez :

    Install-Module -Name AIPService

Si vous recevez un avertissement indiquant que l’installation est effectuée à partir d’un dépôt non approuvé, vous pouvez appuyer sur O pour confirmer. Ou bien, appuyez sur N et configurez PowerShell Gallery comme un référentiel fiable à l’aide de la commande `Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` , puis réexécutez la commande pour installer le module AIPService.  

Si vous avez une version précédente du module AIPService installé à partir de la galerie, mettre à jour vers la dernière version en tapant :

    Update-Module -Name AIPService


## <a name="next-steps"></a>Étapes suivantes
Dans une session Windows PowerShell, vérifiez la version du module installé. Cette vérification est particulièrement importante si vous avez mis à niveau à partir d’une version antérieure :

```
(Get-Module AIPService –ListAvailable).Version
```

Remarque : Si cette commande échoue, commencez par exécuter **Import-Module AIPService**.

Pour voir les applets de commande disponibles, tapez la commande suivante :

```
Get-Command -Module AIPService
```

Utilisez la commande `Get-Help <cmdlet_name>` pour afficher l’aide relative à une applet de commande spécifique, et utilisez le paramètre **-online** pour afficher l’aide la plus récente sur le site de la documentation de Microsoft. Exemple :

```
Get-Help Connect-AipService -online
```

Pour plus d’informations :

-   Liste complète des applets de commande disponibles : [Module de AIPService](/powershell/module/aipservice/?view=azureipps#aipservice)

-   Liste des principaux scénarios de configuration qui prennent en charge de PowerShell : [Administration de la protection d’Azure Information Protection à l’aide de PowerShell](administer-powershell.md)

Avant de pouvoir exécuter des commandes pour configurer le service de protection, vous devez vous connecter au service à l’aide de la [Connect-AipService](/powershell/module/aipservice/connect-aipservice) applet de commande.

Lorsque vous avez terminé d’exécuter vos commandes de configuration, comme une meilleure pratique, vous déconnecter du service à l’aide de la [Disconnect-AipService](/powershell/module/aipservice/disconnect-aipservice) applet de commande. Si vous ne vous déconnectez pas, la connexion est interrompue automatiquement après une période d’inactivité. En raison du comportement de déconnexion automatique, vous constaterez que vous devrez occasionnellement vous reconnecter à une session PowerShell. 

> [!NOTE]
> Si le service de protection n’est pas encore activé, vous pouvez le faire après vous être connecté au service, à l’aide de la [Enable-AipService](/powershell/module/aipservice/enable-aipservice) applet de commande.

