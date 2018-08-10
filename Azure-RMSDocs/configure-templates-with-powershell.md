---
title: PowerShell pour les modèles de protection | Azure Information Protection
description: Tout ce que vous pouvez faire dans le portail Azure pour créer et gérer des modèles de protection, vous pouvez le faire également à partir de la ligne de commande via PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: aad2683fb5c30eda8b94f2208a1c72f46d4a0e13
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490132"
---
# <a name="powershell-reference-for-protection-templates"></a>Informations de référence sur PowerShell pour les modèles de protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les paramètres de protection pour Azure Information Protection sont enregistrés dans des modèles de protection. Tout ce que vous pouvez faire dans le portail Azure pour créer et gérer des paramètres de protection, vous pouvez le faire également à partir de la ligne de commande via PowerShell. 

Vous pouvez aussi exporter et importer des modèles de protection. Ces deux actions vous permettent de copier des modèles de protection entre locataires ou d’effectuer des modifications en bloc de propriétés complexes, telles que les noms et les descriptions multilingues.

Vous pouvez également utiliser l’exportation et l’importation pour sauvegarder et restaurer vos modèles de protection. Comme bonne pratique, sauvegardez régulièrement vos modèles. Ensuite, si vous apportez une modification aux paramètres de protection qui n’était pas volontaire, vous pouvez facilement revenir à une version antérieure.

Pour connaître les instructions d'installation, voir [Installation du module PowerShell AADRM](install-powershell.md).

Applets de commande prenant en charge la création et la gestion de modèles de protection :

- [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate)

- [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate)

- [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate)

- [Get-AadrmTemplateProperty](/powershell/module/aadrm/get-aadrmtemplateproperty)

- [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate)

- [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition)

- [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate)

- [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty)



## <a name="see-also"></a>Voir aussi
[Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md)

