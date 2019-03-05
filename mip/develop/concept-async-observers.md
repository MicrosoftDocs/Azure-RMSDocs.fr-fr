---
title: Concepts – Observateurs dans le kit SDK MIP
description: Le kit SDK MIP est conçu pour être presque entièrement asynchrone. Cet article vous aidera à comprendre comment des observateurs sont implémentés et utilisés pour l’asynchronicité.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e42b9996d737ace5b25988eb72fa02aa87230f13
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330863"
---
# <a name="microsoft-information-protection-sdk---observer-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux observateurs

Le kit SDK MIP est conçu pour être presque entièrement asynchrone. Par exemple, toute opération entraînant des E/S de fichier ou réseau est effectuée de façon asynchrone. Pour gérer les notifications d’événements pour ces événements asynchrones, le kit SDK utilise le [modèle d’observateur](https://wikipedia.org/wiki/Observer_pattern). 

## <a name="implementation-overview"></a>Vue d’ensemble de l’implémentation

Lors de la construction d’un objet qui effectuera une opération asynchrone, une classe `Observer` doit être implémentée. Les observateurs recevront les événements de notification liés aux diverses opérations asynchrones dans le kit SDK MIP et fourniront le résultat à l’appelant.

Les fonctions présentes dans chaque classe `Observer` sont virtuelles et sont remplacées pour le modèle asynchrone privilégié. Le kit SDK implémente le modèle d’observateur de notification d’événements via `std::promise` et `std::future`.

Chaque observateur spécifique à une classe contient un ensemble de fonctions de réussite et d’erreur/échec pour le résultat d’une opération asynchrone. Les fonctions de *réussite* retournent l’objet associé à l’opération. Les fonctions d’*erreur*/*échec* retournent une exception contenant des détails sur la raison pour laquelle l’opération a échoué.

Par exemple, `FileProfile` prend en charge les deux opérations suivantes : 

- Il peut ajouter un nouveau moteur au profil via `FileProfile::AddEngineAsync`. 
- Il peut décharger un moteur du profil via `FileProfile::UnloadEngineAsync`.

Comme deux fonctions `Observer` sont implémentées par opération asynchrone, on peut supposer qu’il y a **quatre** méthodes `Observer` associées à `FileProfile` : 

- `FileProfileObserver::OnAddEngineSuccess()`
- `FileProfileObserver::OnAddEngineError()`
- `FileProfileObserver::OnUnloadEngineSuccess`
- `FileProfileObserver::OnUnloadEngineError()` . 

## <a name="mip-sdk-observer-classes"></a>Classes d’observateur du kit SDK MIP

L’API de fichier du kit SDK MIP contient deux observateurs :

* `mip::FileProfile::Observer`
* `mip::FileHandler::Observer`

L’API de stratégie du kit SDK MIP contient un seul observateur :

* `mip::Profile::Observer`

L’API de Protection du SDK MIP possède trois observateurs :

* `mip::ProtectionProfile::Observer`
* `mip::ProtectionEngine::Observer`
* `mip::ProtectionHandler::Observer`

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur la façon dont les observateurs sont implémentés et utilisés par les différentes API, consultez :

* [Observateurs de l’API de fichier (C++)](concept-async-observers-file-cpp.md)
* [Observateurs de l’API de stratégie (C++)](concept-async-observers-policy-cpp.md)
* [Observateurs de l’API de protection (C++)](concept-async-observers-protection-cpp.md)
