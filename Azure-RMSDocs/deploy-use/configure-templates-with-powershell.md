---
title: "Utilisation de PowerShell pour des modèles Azure RMS personnalisés - AIP"
description: "Tout ce que vous pouvez faire dans le portail Azure pour créer et gérer des modèles de gestion des droits, vous pouvez le faire également à partir de la ligne de commande via PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c3b1662275b051ea75dcc104c4f09b5db53dbe3e
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2017
---
# <a name="powershell-reference-for-custom-templates"></a>Informations de référence sur PowerShell pour les modèles personnalisés

>*S’applique à : Azure Information Protection, Office 365*

Tout ce que vous pouvez faire dans le portail Azure pour créer et gérer des modèles, vous pouvez le faire également à partir de la ligne de commande via PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues.

Vous pouvez aussi avoir recours à l’exportation et à l’importation pour sauvegarder et restaurer vos modèles personnalisés. Nous vous recommandons de sauvegarder régulièrement vos modèles personnalisés. De cette manière, si vous apportez une modification qui n’était pas désirée, vous pourrez facilement rétablir une version antérieure.

> [!IMPORTANT]
> Pour utiliser PowerShell pour créer et gérer des modèles Azure Rights Management, vous devez disposer au minimum de la version 2.0.0.0 du [module Windows PowerShell pour Azure RMS](https://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Si vous avez déjà installé ce module PowerShell, exécutez la commande suivante dans une fenêtre PowerShell pour vérifier le numéro de version : `(Get-Module aadrm -ListAvailable).Version`

Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Applets de commande prenant en charge la création et la gestion de modèles :

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]