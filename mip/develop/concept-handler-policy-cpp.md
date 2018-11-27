---
title: Concepts - Gestionnaires de stratégies dans le kit SDK MIP.
description: Cet article vous aide à comprendre comment les gestionnaires d’API de stratégie sont créés et utilisés pour les opérations d’appel.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/16/2018
ms.author: tommos
ms.openlocfilehash: 02198f7762e2952f946757d14c13a41b22d73c7a
ms.sourcegitcommit: ef70dab87478084fca853f389dab2408b95d1df1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303989"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Kit SDK Microsoft Information Protection - Concepts liés au gestionnaire de stratégies

Dans l’API de la stratégie, `mip::PolicyHandler` expose les opérations utilisées pour calculer les actions de stratégie et envoyer des événements d’audit.

## <a name="policy-handler-functions"></a>Fonctions du gestionnaire de stratégies

`mip::PolicyHandler` expose des méthodes pour lire, écrire et supprimer des étiquettes et des informations de protection. Pour obtenir la liste complète, consultez la [référence de l’API](reference/class_mip_PolicyHandler.md).

Dans cet article, nous couvrirons les méthodes suivantes :

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>Configuration requise

La création de `PolicyHandler` nécessite :

- Un `PolicyProfile`
- L’ajout d’un `PolicyEngine` au `PolicyProfile`
- Une classe qui hérite de `mip::PolicyHandler::Observer`

## <a name="create-a-policy-handler"></a>Créer un gestionnaire de stratégies

La première étape obligatoire pour obtenir des actions de stratégie consiste à créer un objet `PolicyHandler`. Cette classe implémente les fonctionnalités requises pour obtenir la liste des actions de qu'une étiquette spécifique doit prendre. Il implémente également la fonction pour déclencher un événement d’audit.

Pour créer le `PolicyHandler`, il suffit d’appeler la fonction `CreatePolicyHandlerAsync` de `PolicyEngine` en utilisant le modèle de promesse/futur.

`CreatePolicyHandlerAsync` accepte un seul paramètre : **isAuditDiscoveryEnabled**. Affectez la valeur **true** si l’application doit afficher les événements de pulsation dans la journalisation d’audit.

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

Maintenant que vous avez appris sur la création d’un gestionnaire de stratégie :

- Découvrez comment [créer une classe d’état d’exécution](concept-handler-policy-executionstate-cpp.md), qui est utilisé pour déterminer les actions de calcul.
- Téléchargez le [exemples d’API de stratégie à partir de GitHub et essayer de l’API de la stratégie](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
