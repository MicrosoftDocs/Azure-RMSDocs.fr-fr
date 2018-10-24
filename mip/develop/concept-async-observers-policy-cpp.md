---
title: Concepts – Observateurs de l’API de stratégie dans le kit SDK MIP
description: Le kit SDK MIP est conçu pour être presque entièrement asynchrone. Cet article vous aidera à comprendre comment des observateurs de l’API de stratégie sont implémentés et utilisés pour l’asynchronicité.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 50bc3bfd9bcba8e90a386a6e0444f65389bcfa76
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445799"
---
# <a name="microsoft-information-protection-sdk---policy-api-observers"></a>Kit SDK Microsoft Information Protection – Observateurs de l’API de stratégie

L’API de stratégie du kit SDK contient une classe d’observateur. Les membres observateurs sont virtuels et doivent être remplacés pour gérer les rappels pour les opérations asynchrones.

- [`mip::PolicyProfile::Observer`](reference/class_mip_policyprofile_observer.md)

Lorsqu’une opération asynchrone se termine, la fonction membre `OnXxx()` correspondant au résultat est appelée. `OnLoadSuccess()`, `OnLoadFailure()` et `OnAddEngineSuccess()` sont des exemples pour `mip::Profile::Observer`.

Les exemples ci-dessous illustrent le modèle de promesse/futur, qui est également utilisé par les exemples du kit SDK et qui peut être étendu pour implémenter le comportement de rappel souhaité. 

## <a name="profile-observer-implementation"></a>Implémentation d’observateurs de profil

Dans l’exemple suivant, nous avons créé une classe, `ProfileObserver`, qui est dérivée de `mip::Profile::Observer`. Les fonctions membres ont été remplacées pour utiliser le modèle de promesse/futur utilisé dans tous les exemples.

**Remarque** : Les exemples ci-dessous ne sont que partiellement implémentés et n’incluent pas de remplacements pour les observateurs liés à `mip::ProfileEngine`.

### <a name="profileobserverh"></a>profile_observer.h

Dans l’en-tête, nous définissons la classe `ProfileObserver`, dérivée de `mip::Profile::Observer`, puis nous remplaçons chacune des fonctions membres.

```cpp
class ProfileObserver final : public mip::Profile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement remaining members
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

Dans l’implémentation proprement dite, nous définissons une action à entreprendre pour chaque fonction membre d’observateur.

Chaque membre accepte deux paramètres. Le premier est un pointeur partagé vers la classe gérée par la fonction. `ProfileObserver::OnLoadSuccess` s’attend à recevoir un `mip::Profile`. `ProfileObserver::OnAddEngineSuccess` s’attend à `mip::ProfileEngine`.

Le second est un pointeur partagé vers le *contexte*. Dans notre implémentation, le contexte est une référence à un objet `std::promise`, transmise en tant que `shared_ptr<void>`. La première ligne de la fonction caste ceci vers `std::promise`, puis le stocke dans un objet appelé `promise`.

Enfin, le futur est préparé en définissant `promise->set_value()` et en lui transmettant l’objet `mip::Profile`.

```cpp
#include "profile_observer.h"
#include <future>

//Called when Profile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when Profile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement remaining observer members
```

Lorsque vous effectuez une opération asynchrone, l’implémentation des observateurs est transmise au constructeur de paramètres ou à la fonction asynchrone proprement dite. 

