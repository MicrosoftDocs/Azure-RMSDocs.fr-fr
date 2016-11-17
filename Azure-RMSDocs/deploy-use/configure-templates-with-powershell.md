---
title: "Informations de référence sur PowerShell pour les modèles personnalisés | Azure Information Protection"
description: "Toutes les opérations de création et de gestion des modèles de gestion des droits que vous pouvez effectuer via le portail Azure Classic sont également exécutables à partir de la ligne de commande de PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: aad5bc49b15b32c74352d5c9d6d48cd4f1f3cf9c


---



# <a name="powershell-reference-for-custom-templates"></a>Informations de référence sur PowerShell pour les modèles personnalisés

>*S’applique à : Azure Information Protection, Office 365*

Toutes les opérations de création et de gestion des modèles de gestion des droits que vous pouvez effectuer via le portail Azure Classic sont également exécutables à partir de la ligne de commande de PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues.

Vous pouvez aussi avoir recours à l’exportation et à l’importation pour sauvegarder et restaurer vos modèles personnalisés. Nous vous recommandons de sauvegarder régulièrement vos modèles personnalisés. De cette manière, si vous apportez une modification qui n’était pas désirée, vous pourrez facilement rétablir une version antérieure.

> [!IMPORTANT]
> Pour utiliser Windows PowerShell pour créer et gérer des modèles Azure Rights Management, vous devez disposer au minimum de la version 2.0.0.0 du [module Windows PowerShell pour Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Si vous avez déjà installé ce module PowerShell, exécutez la commande suivante dans une fenêtre PowerShell pour vérifier le numéro de version : `(Get-Module aadrm -ListAvailable).Version`

Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Applets de commande prenant en charge la création et la gestion de modèles :

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## <a name="see-also"></a>Voir aussi
[Configurer des modèles personnalisés pour Azure Rights Management](configure-custom-templates.md)


<!--HONumber=Nov16_HO2-->


