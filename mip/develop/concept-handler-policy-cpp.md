---
title: Concepts - Gestionnaires de stratégies dans le kit SDK MIP.
description: Cet article vous aide à comprendre comment les gestionnaires d’API de stratégie sont créés et utilisés pour les opérations d’appel.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 583e59832e40f87665232ebf39e1dddb462ba212
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556178"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Kit SDK Microsoft Information Protection - Concepts liés au gestionnaire de stratégies

Dans l’API de stratégie, `mip::PolicyHandler` expose les opérations utilisées pour calculer des actions de stratégie et soumettre des événements d’audit.

## <a name="policy-handler-functions"></a>Fonctions du gestionnaire de stratégies

`mip::PolicyHandler` expose des méthodes pour lire, écrire et supprimer des étiquettes et des informations de protection. Pour obtenir la liste complète, consultez la [référence de l’API](reference/class_mip_PolicyHandler.md).

Dans cet article, nous couvrirons les méthodes suivantes :

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>Conditions requises

La création de `PolicyHandler` nécessite :

- Un `mip::MipContext`
- Un `mip::PolicyProfile`
- L’ajout d’un `mip::PolicyEngine` au `mip::PolicyProfile`
- Classe qui implémente `mip::PolicyHandler::Observer`

## <a name="create-a-policy-handler"></a>Créer un gestionnaire de stratégies

La première étape obligatoire pour obtenir des actions de stratégie consiste à créer un objet `PolicyHandler`. Cette classe implémente les fonctionnalités requises pour obtenir la liste des actions qu’une étiquette spécifique doit prendre. Il implémente également la fonction pour déclencher un événement d’audit.

Pour créer le `PolicyHandler`, il suffit d’appeler la fonction `CreatePolicyHandlerAsync` de `PolicyEngine` en utilisant le modèle de promesse/futur.

`CreatePolicyHandlerAsync` accepte un seul paramètre : **isAuditDiscoveryEnabled**. Définissez cette valeur sur **true** si l’application doit exposer les événements de pulsation et de découverte dans la journalisation d’audit.

> [!NOTE]
> La classe `mip::PolicyHandler::Observer` doit être implémentée dans une classe dérivée, car `CreatePolicyHandler` nécessite l’objet `Observer`. 

```cpp
auto createPolicyHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyHandler>>>();
auto createPolicyHandlerFuture = createPolicyHandlerPromise->get_future();
PolicyEngine->CreatePolicyHandlerAsync(true);
auto handler = createPolicyHandlerFuture.get();
```

Une fois l’objet `PolicyHandler` correctement créé, les actions peuvent être calculées et les événements d’audit envoyés.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris à créer un gestionnaire de stratégie :

- Découvrez comment [créer une classe d’état d’exécution](concept-handler-policy-executionstate-cpp.md), qui est utilisée pour déterminer des actions de calcul.
- Téléchargez les [exemples d’API de stratégie à partir de GitHub et essayez l’API de stratégie](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
