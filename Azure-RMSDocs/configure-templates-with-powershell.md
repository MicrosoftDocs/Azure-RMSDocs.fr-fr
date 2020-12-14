---
title: PowerShell pour les modèles de protection | Azure Information Protection
description: Utilisez les applets de commande PowerShell pour ajouter, obtenir, exporter, importer, supprimer et configurer des modèles de protection pour Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0188b757dc1f09fb3d153fe3430d9da6185e6836
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382902"
---
# <a name="powershell-reference-for-protection-templates"></a>Informations de référence sur PowerShell pour les modèles de protection

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) dans la documentation de Microsoft 365. *

> [!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>

Les paramètres de protection pour Azure Information Protection sont enregistrés dans des modèles de protection. Tout ce que vous pouvez faire dans le portail Azure pour créer et gérer des paramètres de protection, vous pouvez le faire également à partir de la ligne de commande via PowerShell. 

Vous pouvez aussi exporter et importer des modèles de protection. Ces deux actions vous permettent de copier des modèles de protection entre locataires ou d’effectuer des modifications en bloc de propriétés complexes, telles que les noms et les descriptions multilingues.

Vous pouvez également utiliser l’exportation et l’importation pour sauvegarder et restaurer vos modèles de protection. Comme bonne pratique, sauvegardez régulièrement vos modèles. Ensuite, si vous apportez une modification aux paramètres de protection qui n’était pas volontaire, vous pouvez facilement revenir à une version antérieure.

Pour obtenir des instructions d’installation, consultez [installation du module PowerShell AIPService](install-powershell.md).

Applets de commande prenant en charge la création et la gestion de modèles de protection :

- [Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)

- [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)

- [AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)

- [AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)

- [Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetpd)

- [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)

- [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)

- [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)

## <a name="see-also"></a>Voir aussi
[Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md)

