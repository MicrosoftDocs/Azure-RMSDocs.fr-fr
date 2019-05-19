---
title: Utiliser PowerShell avec le client d’étiquetage unifié Azure Information Protection
description: Instructions et informations destinées aux administrateurs de gérer le client d’étiquetage unifié Azure Information Protection à l’aide de PowerShell.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: a7e7ad68a5b7ce6c465b990b15bbef6824fadf75
ms.sourcegitcommit: c0d8b7239fc16e66b51f736636da7f7212f72dd6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65837795"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guide de l’administrateur : À l’aide de PowerShell avec le client unifié d’Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Lorsque vous installez le client d’étiquetage unifié Azure Information Protection, les commandes PowerShell sont installées automatiquement. Vous pouvez ainsi gérer le client en exécutant des commandes que vous pouvez placer dans des scripts d’automatisation.

Les applets de commande sont installés avec le module PowerShell **AzureInformationProtection**, qui a des applets de commande pour l’étiquetage. Exemple :

|Étiquetage des applets de commande|Exemple d’utilisation|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Dans le cas d’un dossier partagé, identifiez tous les fichiers avec une étiquette spécifique.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Pour un dossier partagé, inspectez le contenu du fichier puis étiquetez automatiquement les fichiers sans étiquette, selon les conditions que vous avez spécifiées.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Pour un dossier partagé, appliquez une étiquette spécifiée à tous les fichiers dépourvus d’étiquette.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Étiqueter des fichiers de manière interactive, à l’aide d’un autre compte d’utilisateur dans votre propre.|

> [!TIP]
> Pour utiliser des applets de commande avec des chemins comprenant plus de 260 caractères, utilisez le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) disponible à compter de la version 1607 de Windows 10 :<br /> **Stratégie de l’ordinateur local** > **Configuration ordinateur** > **modèles d’administration** > **tous les paramètres**  >  **Win32 activer les chemins d’accès longs** 
> 
> Pour Windows Server 2016, vous pouvez utiliser le même paramètre de stratégie de groupe lorsque vous installez les derniers modèles d’administration (.admx) pour Windows 10.
>
> Pour plus d’informations, consultez la section consacréee à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

Ce module s’installe dans **\ProgramFiles (x86)\Microsoft Azure Information Protection** et ajoute ce dossier à la variable système **PSModulePath**. Le fichier .dll de ce module est nommé **AIP.dll**.

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Configuration requise pour l’utilisation du module AzureInformationProtection

Outre la configuration requise pour l’installation du module AzureInformationProtection, il existe des conditions préalables supplémentaires pour lorsque vous utilisez les applets de commande étiquetage pour Azure Information Protection :

1. Le service Azure Rights Management doit être activé.

2. Pour supprimer la protection des fichiers pour les autres utilisateurs à l’aide de votre propre compte : 

    - La fonctionnalité de super utilisateur doit être activée pour votre organisation et votre compte doit être configuré pour être un super utilisateur d’Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prérequis 1 : Le service Azure Rights Management doit être activé

Si votre client Azure Information Protection n’est pas activé pour appliquer la protection, consultez les instructions pour [activation d’Azure Rights Management](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prérequis 2 : Pour supprimer la protection des fichiers pour les autres utilisateurs en utilisant votre propre compte

Les scénarios classiques de suppression de la protection des fichiers pour les autres utilisateurs incluent la détection de données ou la récupération de données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer la protection en définissant une nouvelle étiquette qui n’applique pas la protection ou en supprimant l’étiquette.

Pour supprimer la protection des fichiers, vous devez disposer d’un droit d’utilisation Rights Management ou être un super utilisateur. Pour la découverte de données ou la récupération de données, la fonctionnalité de super utilisateur est généralement utilisée. Pour activer cette fonctionnalité et configurer votre compte pour un super utilisateur, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../configure-super-users.md).


## <a name="next-steps"></a>Étapes suivantes
Pour l’aide d’applet de commande lorsque vous êtes dans une session PowerShell, tapez `Get-Help <cmdlet name> -online`. Exemple : 

    Get-Help Set-AIPFileLabel -online

Pour des informations supplémentaires nécessaires pour la prise en charge du client Azure Information Protection, consultez les éléments suivants :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](clientv2-admin-guide-file-types.md)
