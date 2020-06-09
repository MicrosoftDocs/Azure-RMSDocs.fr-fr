---
title: Concept-justification de l’action dans le kit de développement logiciel (SDK) MIP (C++)
description: Cet article vous aidera à comprendre le scénario de mise à niveau ou de suppression d’une étiquette nécessitant une justification.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: 1b0926114dd4d494593bd0d2340fee35edfe5fe6
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548239"
---
# <a name="action-justification-in-mip-sdk-c"></a>Justification de l’action dans le kit de développement logiciel (SDK) MIP (C++)

## <a name="overview"></a>Vue d’ensemble

Étiquette les stratégies dans Security and Compliance Center permettent aux administrateurs de demander une **Justification** lors de la suppression ou de la rétrogradation d’une étiquette. La rétrogradation est définie comme l’application d’une étiquette qui a une valeur de sensibilité inférieure à la place de l’étiquette existante.

Comme nous l’avons vu précédemment, l’API file fournit des interfaces faciles à utiliser pour lire des étiquettes à partir du service, appliquer des étiquettes à des types de fichiers définis et lire des étiquettes à partir de ces types de fichiers. Il prend également en charge les opérations de fichiers pour supprimer des étiquettes de et la modification des étiquettes sur les FileTypes pris en charge. Les modifications apportées à l’étiquette de fichier sont prises en charge via la `mip::FileHandler` `SetLabel()` fonction de, ce qui permet de définir une nouvelle étiquette sur un fichier non protégé ou précédemment protégé, et la `mip::FileHandler` `DeleteLabel()` fonction de qui supprime l’étiquette d’un fichier précédemment protégé.

Pour certaines des étiquettes de sensibilité, les administrateurs de la sécurité peuvent souhaiter appliquer des stratégies plus strictes, lorsqu’un utilisateur tente de rétrograder la sensibilité en supprimant une étiquette ou en remplaçant l’étiquette par une valeur moins restrictive. Les administrateurs peuvent configurer cette option à l’aide de la configuration de la stratégie d’étiquette dans le [Centre de sécurité et conformité](https://sip.compliance.microsoft.com/) en cochant la case.

![Justification de l’action requise](./media/justify-action.png)

Si le fichier a une étiquette existante et si la stratégie d’étiquette requiert une justification dans le cas d’une rétrogradation de niveau de sensibilité, les `SetLabel()` / `DeleteLabel()` fonctions lèvent `mip::JustificationRequiredError` . Dans ce type de scénario, l’API offre la possibilité d’enregistrer la justification de l’utilisateur. Les consommateurs du SDK doivent fournir une interface d’application à l’utilisateur pour fournir des informations sur la raison du passage à une version antérieure. Une fois la justification enregistrée, l’application peut définir `isDowngradeJustified` la propriété de `mip::LabelingOptions` , ainsi que la définition de la `Justification` propriété.

## <a name="next-steps"></a>Étapes suivantes

- Vérifier le [démarrage rapide de la justification de l’action pour (C++)](quick-file-justify-actions-cpp.md)
- Vérifier le [démarrage rapide de la justification de l’action pour (C#)](quick-file-justify-actions-csharp.md)