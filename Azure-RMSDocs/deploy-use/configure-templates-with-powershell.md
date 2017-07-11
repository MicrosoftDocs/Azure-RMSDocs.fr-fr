---
title: "Utilisation de PowerShell pour des modèles Azure RMS personnalisés - AIP"
description: "Toutes les opérations de création et de gestion des modèles de gestion des droits que vous pouvez effectuer via le portail Azure Classic sont également exécutables à partir de la ligne de commande de PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8da24d00f6b6cb62bc745404e68e691b5afc2cb8
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="powershell-reference-for-custom-templates" class="xliff"></a>

# Informations de référence sur PowerShell pour les modèles personnalisés

>*S’applique à : Azure Information Protection, Office 365*

Toutes les opérations de création et de gestion des modèles de gestion des droits que vous pouvez effectuer via le portail Azure Classic sont également exécutables à partir de la ligne de commande de PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues.

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



<a id="see-also" class="xliff"></a>

## Voir aussi
[Configurer des modèles personnalisés pour Azure Rights Management](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]