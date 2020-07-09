---
title: PowerShell pour les modèles de protection | Azure Information Protection
description: Utilisez PowerShell pour créer et gérer des modèles de protection pour Azure Information Protection.
author: mlottner
ms.author: mlottner
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
ms.openlocfilehash: 38d5a71e6820c4ad95395c06dffea5d5e57ee7d6
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136781"
---
# <a name="powershell-reference-for-protection-templates"></a>Informations de référence sur PowerShell pour les modèles de protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

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

