---
title: Concept-justification de l’action dans le SDK MIP
description: Cet article explique comment supprimer une étiquette qui nécessite une justification ou la faire passer à une version antérieure.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: mbaldwin
ms.openlocfilehash: b6f5ebaa08a2726671f891c583d46f310952d1d2
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864938"
---
# <a name="action-justification-in-mip-sdk"></a>Justification de l’action dans le SDK MIP

## <a name="overview"></a>Vue d’ensemble

Étiquette les stratégies dans Security and Compliance Center permettent aux administrateurs de demander une **Justification** lors de la suppression ou de la rétrogradation d’une étiquette. La rétrogradation est définie comme l’application d’une étiquette qui a une valeur de sensibilité inférieure à la place de l’étiquette existante.

Comme nous l’avons vu précédemment, l’API file fournit des interfaces faciles à utiliser pour lire des étiquettes à partir du service, appliquer des étiquettes à des types de fichiers définis et lire des étiquettes à partir de ces types de fichiers. Il prend également en charge les opérations de fichiers pour la suppression et la modification des étiquettes pour les FileTypes pris en charge. Les modifications apportées à l’étiquette de fichier sont prises en charge via la `mip::FileHandler` `SetLabel()` fonction de, ce qui permet de définir une nouvelle étiquette sur un fichier non protégé ou précédemment protégé, et la `mip::FileHandler` `DeleteLabel()` fonction de qui supprime l’étiquette d’un fichier précédemment protégé.

Pour certaines des étiquettes de sensibilité, les administrateurs de la sécurité peuvent souhaiter appliquer des stratégies plus strictes, lorsqu’un utilisateur tente de rétrograder la sensibilité en supprimant une étiquette ou en remplaçant l’étiquette par une valeur moins restrictive. Les administrateurs peuvent configurer cette option à l’aide de la configuration de la stratégie d’étiquette dans le [Centre de sécurité et conformité](https://sip.compliance.microsoft.com/) en cochant la case.

![Justification de l’action requise](./media/justify-action.png)

Si le fichier a une étiquette existante et que la stratégie d’étiquette requiert une justification en cas de rétrogradation d’une étiquette, les `SetLabel()` / `DeleteLabel()` fonctions lèvent `mip::JustificationRequiredError` . L’application doit intercepter cette exception, puis fournir une interface d’application à l’utilisateur pour fournir une entrée sur la raison du passage à une version antérieure. Une fois la justification enregistrée, l’application peut définir `isDowngradeJustified` la propriété de `mip::LabelingOptions` , ainsi que la définition de la `Justification` propriété.

## <a name="next-steps"></a>Étapes suivantes

- Vérifier le [démarrage rapide de la justification de l’action pour (C++)](quick-file-justify-actions-cpp.md)
- Vérifier le [démarrage rapide de la justification de l’action pour (C#)](quick-file-justify-actions-csharp.md)