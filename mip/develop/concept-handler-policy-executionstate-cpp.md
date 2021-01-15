---
title: Concepts - Implémentation d’ExecutionState dans le kit SDK Microsoft Information Protection
description: Cet article vous aide à comprendre comment utiliser ExecutionState dans le kit SDK Microsoft Information Protection afin d’effectuer des calculs et de fournir des détails pour la journalisation d’audit.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: 732ca5e87b83f578dad3b40f842e31ea29e95c08
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212720"
---
# <a name="implement-executionstate"></a>Implémenter ExecutionState

Le passage d’informations dans le kit SDK MIP pour calculer une action à effectuer, en fonction de l’état actuel et de l’état souhaité, est implémenté via la classe `mip::ExecutionState`. Comme d’autres classes du kit SDK, `ExecutionState` est une classe abstraite et doit être implémentée par le développeur.

> Pour obtenir un exemple complet d’implémentation de `ExecutionState`, consultez l’exemple de source suivant :
>
> * [execution_state_impl.h](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h)
> * [execution_state_impl.cpp](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.cpp)

## <a name="mipexecutionstate-members"></a>Membres de mip::ExecutionState

`ExecutionState` expose les membres virtuels suivants. Chacun d’eux fournit un contexte au moteur de stratégies pour retourner des informations sur les actions à entreprendre par l’application. De plus, vous pouvez utiliser ces informations pour fournir des informations d’audit à la fonctionnalité de création de rapports Azure Information Protection.

| Membre                                                                             | Retours                                                                                                              |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `std::shared_ptr<mip::Label> GetNewLabel()`                                        | Retourne l’étiquette à appliquer à l’objet.                                                                       |
| `mip::DataState GetDataState()`                                                    | Retourne le ataState MIP ::D de l’objet.                                                                            |
| `std::pair<bool, std::string> IsDowngradeJustified()`                              | Retourne un std::pair qui indique si le passage à une version antérieure est justifié et pour quelle raison.                                 |
| `std::string GetContentIdentifier()`                                               | Retourne l’identificateur de contenu. Il doit s’agir d’un identificateur lisible, qui désigne l’emplacement de l’objet.        |
| `mip::ActionSource GetNewLabelActionSource()`                                      | Retourne le mip::ActionSource de l’étiquette.                                                                          |
| `mip::AssignmentMethod GetNewLabelAssignmentMethod()`                              | Retourne le mip::AssignmentMethod de l’étiquette.                                                                       |
| `std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties()` | Retourne un std::vector du std::pairs des chaînes contenant les métadonnées personnalisées à appliquer au document. |
| `std::vector<std::pair<std::string, std::string>> GetContentMetadata()`            | Retourne un std::vector du std::pairs de la chaîne contenant les métadonnées de contenu actuelles.                               |
| `std::shared_ptr<mip::ProtectionDescriptor> GetProtectionDescriptor()`             | Retourne un pointeur vers mip::ProtectionDescriptor                                                                     |
| `std::string GetContentFormat()`                                            | Retourne une chaîne                                                                                           |
| `mip::ActionType GetSupportedActions()`                                            | Retourne mip::ActionTypes pour l’étiquette.                                                                              |
| `std::shared_ptr<mip::ClassificationResults>`                                      | Retourne une liste de résultats de classification, si elle est implémentée.                                                            |

Chacun doit être substitué dans une implémentation d’une classe dérivée de `mip::ExecutionState`. Dans l’exemple d’application lié ci-dessus, ce processus est accompli via l’implémentation d’un struct appelé `ExecutionStateOptions`, et son passage au constructeur de la classe dérivée.

Dans l’[exemple](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h), un struct appelé `ExecutionStateOptions` est défini comme suit :

```cpp
struct ExecutionStateOptions {
    std::unordered_map<std::string, std::string> metadata;
    std::string newLabelId;
    std::string contentIdentifier;
    mip::ActionSource actionSource = mip::ActionSource::MANUAL;
    mip::DataState dataState = mip::DataState::USE;
    mip::AssignmentMethod assignmentMethod = mip::AssignmentMethod::STANDARD;
    bool isDowngradeJustified = false;
    std::string downgradeJustification;
    std::string templateId;
    std::string contentFormat = mip::GetFileContentFormat();
    mip::ActionType supportedActions;
    bool generateAuditEvent;
};
```

Chaque propriété est définie par l’application, puis `ExecutionStateOptions` est passé au constructeur de la classe dérivée de `mip::ExecutionState`. Ces informations sont utilisées pour déterminer les actions à entreprendre. Les données fournies dans `mip::ExecutionState` figurent également dans les fonctionnalités d’analyse Azure Information Protection.

### <a name="next-steps"></a>Étapes suivantes

- Découvrez comment déterminer [des actions de calcul pour une étiquette nouvelle ou existante](concept-handler-policy-computeactions-cpp.md), en fonction de l’état actuel et souhaité.
- Téléchargez les [exemples d’API de stratégie à partir de GitHub et essayez l’API de stratégie](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
