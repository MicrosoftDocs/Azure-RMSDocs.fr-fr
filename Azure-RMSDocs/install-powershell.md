---
title: Installer le module PowerShell AIPService pour Azure Information Protection
description: Instructions pour installer PowerShell pour le service de protection à partir de Azure Information Protection. Le nom de ce module est AIPService.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 89820a815e664589051a91f273cb63280e70713a
ms.sourcegitcommit: 72ae1f635e51ef6c6deb1833a30ff11e5918a3e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063728"
---
# <a name="installing-the-aipservice-powershell-module"></a>Installation du module PowerShell AIPService

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations suivantes pour vous aider à installer le module Windows PowerShell pour le service de protection à partir de Azure Information Protection. Le nom de ce module est AIPService et remplace la version précédente nommée AADRM.

Vous pouvez utiliser ce module PowerShell pour administrer le service de protection (Azure Rights Management) à partir de la ligne de commande à l’aide de n’importe quel ordinateur Windows disposant d’une connexion Internet et qui satisfait aux conditions préalables indiquées dans la section suivante. Windows PowerShell pour Azure Information Protection prend en charge l’écriture de scripts pour l’automatisation ou peut être nécessaire pour les scénarios de configuration avancée. Pour plus d’informations sur les tâches d’administration et les configurations prises en charge par le module, consultez [administration de la protection à partir de Azure information protection à l’aide de PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prérequis
Ce tableau répertorie les conditions préalables à l’installation et l’utilisation du module PowerShell AIPService pour le service de protection de Azure Information Protection.

|Prérequis|Plus d’informations|
|---------------|--------------------|
|Version minimale de Windows PowerShell: 3,0|Vous pouvez vérifier la version de Windows PowerShell que vous exécutez en tapant `$PSVersionTable` dans une session PowerShell. <br /><br /> Si vous devez installer une version ultérieure de Windows PowerShell, consultez [Mise à niveau de la version Windows PowerShell existante](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Version minimale de l’infrastructure Microsoft .NET: 4,5<br /><br />Remarque : Cette version de Microsoft .NET Framework est incluse avec les systèmes d’exploitation ultérieurs. par conséquent, vous devez l’installer manuellement uniquement si votre système d’exploitation client est inférieur à Windows 8,0 ou si votre système d’exploitation serveur est inférieur à Windows Server 2012.|Si la version minimale du Microsoft .NET Framework n’est pas installée, vous pouvez télécharger [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Cette version minimale du Microsoft .NET Framework est requise pour certaines des classes utilisées par le module AIPService.|

## <a name="if-you-have-the-aadrm-module-installed"></a>Si le module AADRM est installé

Le module AIPService remplace l’ancien module, AADRM. Si vous avez installé l’ancien module, désinstallez-le, puis installez le module AIPService.

Le module plus récent a des alias pour les noms d’applets de commande dans l’ancien module afin que tous les scripts existants continuent de fonctionner. Toutefois, prévoyez de mettre à jour ces références avant que l’ancien module ne soit pris en charge. La prise en charge du module AADRM se terminera le 15 juillet 2020.

Si vous avez installé le module AADRM à partir de la PowerShell Gallery, pour le désinstaller, démarrez une session PowerShell avec l’option **exécuter en tant qu’administrateur** , puis tapez:

    Uninstall-Module -Name AADRM

Si vous avez installé le module AADRM avec l’outil d’administration Azure Rights Management, utilisez **programmes et fonctionnalités** pour désinstaller **Windows Azure ad Rights Management Administration**.

## <a name="how-to-install-the-aipservice-module"></a>Comment installer le module AIPService

Le module AIPService se trouve sur le [PowerShell Gallery](/powershell/gallery/readme) et n’est pas disponible dans le centre de téléchargement Microsoft. 

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>Pour installer le module AIPService à partir de la PowerShell Gallery

Si vous n’avez jamais utilisé PowerShell Gallery, consultez [Bien démarrer avec PowerShell](/powershell/gallery/psgallery/psgallery_gettingstarted). Suivez les instructions relatives à la configuration requise de la galerie, avec notamment l’installation du module PowerShellGet et du fournisseur NuGet.

Pour plus d’informations sur le module AIPService sur la PowerShell Gallery, consultez la [page AIPService](https://www.powershellgallery.com/packages/AIPService).

Pour installer le module AIPService, démarrez une session PowerShell avec l’option **exécuter en tant qu’administrateur** , puis tapez:

    Install-Module -Name AIPService

Si vous recevez un avertissement indiquant que l’installation est effectuée à partir d’un dépôt non approuvé, vous pouvez appuyer sur O pour confirmer. Vous pouvez aussi appuyer sur N et configurer le PowerShell Gallery en tant que référentiel approuvé à l’aide `Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` de la commande, puis réexécuter la commande pour installer le module AIPService.  

Si vous disposez d’une version précédente du module AIPService installée à partir de la Galerie, mettez-la à jour avec la dernière version en tapant ce qui suit:

    Update-Module -Name AIPService


## <a name="next-steps"></a>Étapes suivantes
Dans une session Windows PowerShell, vérifiez la version du module installé. Cette vérification est particulièrement importante si vous avez mis à niveau à partir d’une version antérieure :

```
(Get-Module AIPService –ListAvailable).Version
```

Remarque : Si cette commande échoue, exécutez d’abord **import-module AIPService**.

Pour voir les applets de commande disponibles, tapez la commande suivante :

```
Get-Command -Module AIPService
```

Utilisez la commande `Get-Help <cmdlet_name>` pour afficher l’aide relative à une applet de commande spécifique, et utilisez le paramètre **-online** pour afficher l’aide la plus récente sur le site de la documentation de Microsoft. Par exemple :

```
Get-Help Connect-AipService -online
```

Pour plus d'informations :

-   Liste complète des applets de commande disponibles: [Module AIPService](/powershell/module/aipservice/?view=azureipps#aipservice)

-   Liste des principaux scénarios de configuration qui prennent en charge PowerShell: [Administration de la protection à partir de Azure Information Protection à l’aide de PowerShell](administer-powershell.md)

Avant de pouvoir exécuter des commandes qui configurent le service de protection, vous devez vous connecter au service à l’aide de l’applet de commande [Connect-AipService](/powershell/module/aipservice/connect-aipservice) .

Lorsque vous avez terminé d’exécuter vos commandes de configuration, il est recommandé de se déconnecter du service à l’aide de l’applet de commande [Disconnect-AipService](/powershell/module/aipservice/disconnect-aipservice) . Si vous ne vous déconnectez pas, la connexion est interrompue automatiquement après une période d’inactivité. En raison du comportement de déconnexion automatique, vous constaterez que vous devrez occasionnellement vous reconnecter à une session PowerShell. 

> [!NOTE]
> Si le service de protection n’est pas encore activé, vous pouvez le faire après vous être connecté au service, à l’aide de l’applet de commande [Enable-AipService](/powershell/module/aipservice/enable-aipservice) .

