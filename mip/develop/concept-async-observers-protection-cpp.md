---
title: Concepts – Observateurs de l’API de protection dans le kit SDK MIP
description: Le kit SDK MIP est conçu pour être presque entièrement asynchrone. Cet article vous aidera à comprendre comment des observateurs de l’API de protection sont implémentés et utilisés pour l’asynchronicité.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: d7077678ba336b031f7a8f812a3c4e90d8c5b05a
ms.sourcegitcommit: d677088db8588fb2cc4a5d7dd296e76d0d9a2e9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251707"
---
# <a name="microsoft-information-protection-sdk---protection-api-observers"></a>Kit SDK Microsoft Information Protection – Observateurs de l’API de protection

L’API de protection contient trois classes d’observateur. Les membres observateurs sont virtuels et peuvent être remplacés pour gérer les rappels pour les opérations asynchrones.

- [Profil de protection : `mip::ProtectionProfile::Observer`](reference/class_mip_ProtectionProfile_observer.md)
- [Moteur de protection : `mip::ProtectionEngine::Observer`](reference/class_mip_ProtectionEngine_observer.md)
- [Gestionnaire de protection : `mip::ProtectionHandler::Observer`](reference/class_mip_Protectionhandler_observer.md)

Lorsqu’une opération asynchrone se termine, la fonction membre `OnXxx()` correspondant au résultat est appelée. `OnLoadSuccess()`, `OnLoadFailure()` et `OnAddEngineSuccess()` sont des exemples pour `mip::ProtectionProfile::Observer`.

Les exemples ci-dessous illustrent le modèle de promesse/futur, qui est également utilisé par les exemples du kit SDK et qui peut être étendu pour implémenter le comportement de rappel souhaité. 

## <a name="protection-protection-observer-implementation"></a>Implémentation d’observateurs de protection Protection

Dans l’exemple suivant, nous avons créé une classe, `ProtectionProfileObserverImpl`, qui est dérivée de `mip::ProtectionProfile::Observer`. Les fonctions membres ont été remplacées pour utiliser le modèle de promesse/futur utilisé dans tous les exemples.

### <a name="protectionprofileobserverimpl-class-declaration"></a>Déclaration de la classe ProtectionProfileObserverImpl

Dans l’en-tête, nous définissons la classe `ProtectionProfileObserverImpl`, dérivée de `mip::ProtectionProfile::Observer`, puis nous remplaçons chacune des fonctions membres.

```cpp
//ProtectionProfileObserverImpl.h
class ProtectionProfileObserverImpl final : public mip::ProtectionProfile::Observer {
public:
  ProtectionProfileObserverImpl() { }
  void OnLoadSuccess(const shared_ptr<mip::ProtectionProfile>& profile, const shared_ptr<void>& context) override;
  void OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) override;
  void OnAddEngineSuccess(const shared_ptr<mip::ProtectionEngine>& engine, const shared_ptr<void>& context) override;
  void OnAddEngineError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionprofileobserverimpl-implementation"></a>Implémentation de ProtectionProfileObserverImpl

Dans l’implémentation proprement dite, nous définissons simplement une action à entreprendre pour chaque fonction membre d’observateur.

Chaque membre accepte deux paramètres. Le premier est un pointeur partagé vers la classe que nous traitons dans la fonction. `ProtectionObserver::OnLoadSuccess` s’attend à recevoir un objet `mip::ProtectionProtection`, `ProtectionObserver::OnAddEngineSuccess` s’attend à recevoir `mip::ProtectionEngine`.

Le second est un pointeur partagé vers le *contexte*. Dans notre implémentation, le contexte est une référence à un objet `std::promise`, transmise en tant que `shared_ptr<void>`. La première ligne de la fonction caste ceci en `std::promise`, puis le stocke dans un objet appelé `promise`.

Enfin, le futur est préparé en définissant `promise->set_value()` et en lui transmettant l’objet `mip::ProtectionProtection`.

```cpp
//protection_observers.cpp

void ProtectionProfileObserverImpl::OnLoadSuccess(
  const shared_ptr<mip::ProtectionProfile>& profile,
  const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_value(profile);
};

void ProtectionProfileObserverImpl::OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_exception(error);
};

void ProtectionProfileObserverImpl::OnAddEngineSuccess(
  const shared_ptr<mip::ProtectionEngine>& engine,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_value(engine);
};

void ProtectionProfileObserverImpl::OnAddEngineError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_exception(error);
};
```

Lorsque nous instancions une classe du kit SDK ou utilisons une fonction qui effectue des opérations asynchrones, nous passons l’implémentation des observateurs au constructeur de paramètres ou à la fonction asynchrone elle-même. Lors de l’instanciation de l’objet `mip::ProtectionProfile::Settings`, le constructeur accepte `mip::ProtectionProfile::Observer` comme l’un des paramètres. L’exemple ci-dessous montre notre objet `ProtectionProfileObserverImpl` personnalisé, utilisé dans un constructeur `mip::ProtectionProfile::Settings`.

## <a name="protectionhandler-observer-implementation"></a>Implémentation d’observateurs ProtectionHandler

De façon similaire à l’observateur de protection, l’objet `mip::ProtectionHandler` implémente une classe `mip::ProtectionHandler::Observer` pour la gestion des notifications d’événements asynchrones lors d’opérations de protection. L’implémentation est similaire à celle détaillée ci-dessus. `ProtectionHandlerObserverImpl` est partiellement défini ci-dessous. Vous trouverez l’implémentation complète dans notre [dépôt d’exemples GitHub](https://azure.microsoft.com/resources/samples/?sort=0&term=mip+sdk).

### <a name="protectionhandlerobserverimpl-class-declaration"></a>Déclaration de la classe ProtectionProfileObserverImpl

```cpp
//protection_observers.h

class ProtectionHandlerObserverImpl final : public mip::ProtectionHandler::Observer {
public:
  ProtectionHandlerObserverImpl() { }
  void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
  void OnCreateProtectionHandlerError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionhandlerobserverimpl-partial-implementation"></a>Implémentation partielle de ProtectionProfileObserverImpl

Cet exemple correspond simplement aux deux premières fonctions, mais les fonctions restantes utilisent un modèle similaire à celles-ci et à `ProtectionObserver`.

```cpp
//protection_observers.cpp

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerSuccess(
  const shared_ptr<mip::ProtectionHandler>& protectionHandler,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_value(protectionHandler);
};

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_exception(error);
};
```

