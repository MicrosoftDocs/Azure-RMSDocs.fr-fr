---
title: Concepts – Observateurs de l’API de fichier dans le kit SDK MIP
description: Le kit SDK MIP est conçu pour être presque entièrement asynchrone. Cet article vous aidera à comprendre comment des observateurs de l’API de fichier sont implémentés et utilisés pour l’asynchronicité.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: baa62e34e10de3fb4cacc3eb7cb21c0b3e2ebf75
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "60175443"
---
# <a name="microsoft-information-protection-sdk---file-api-observers"></a>Kit SDK Microsoft Information Protection – Observateurs de l’API de fichier

L’API de fichier contient deux classes d’observateur. Les membres observateurs sont virtuels et peuvent être remplacés pour gérer des rappels d’événement.

- [`mip::FileProfile::Observer`](reference/class_mip_fileprofile_observer.md)
- [`mip::FileHandler::Observer`](reference/class_mip_filehandler_observer.md)

Lorsqu’une opération asynchrone se termine, la fonction membre `OnXxx()` correspondant au résultat est appelée. `OnLoadSuccess()`, `OnLoadFailure()` et `OnAddEngineSuccess()` sont des exemples pour `mip::FileProfile::Observer`.

Les exemples ci-dessous illustrent le modèle de promesse/futur, qui est également utilisé par les exemples du kit SDK et qui peut être étendu pour implémenter le comportement de rappel souhaité. 

## <a name="file-profile-observer-implementation"></a>Implémentation d’observateurs du profil de fichier

Dans l’exemple suivant, nous avons créé une classe, `ProfileObserver`, qui est dérivée de `mip::FileProfile::Observer`. Les fonctions membres ont été remplacées pour utiliser le modèle de promesse/futur utilisé dans tous les exemples.

**Remarque** : Les exemples ci-dessous ne sont que partiellement implémentés et n’incluent pas de remplacements pour les observateurs liés à `mip::FileEngine`.

### <a name="profile_observerh"></a>profile_observer.h

Dans l’en-tête, nous définissons la classe `ProfileObserver`, dérivée de `mip::FileProfile::Observer`, puis nous remplaçons chacune des fonctions membres.

```cpp
class ProfileObserver final : public mip::FileProfile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement mip::FileEngine related observers.
};
```

### <a name="profile_observercpp"></a>profile_observer.cpp

Dans l’implémentation proprement dite, nous définissons une action à entreprendre pour chaque fonction membre d’observateur.

Chaque membre accepte deux paramètres. Le premier est un pointeur partagé vers la classe que nous traitons dans la fonction. `ProfileObserver::OnLoadSuccess` s’attend à recevoir un `mip::FileProfile`. `ProfileObserver::OnAddEngineSuccess` s’attend à `mip::FileEngine`.

Le second est un pointeur partagé vers le *contexte*. Dans notre implémentation, le contexte est une référence à un objet `std::promise`, transmise par référence en tant que `std::shared_ptr<void>`. La première ligne de la fonction caste ceci en `std::promise`, puis le stocke dans un objet appelé `promise`.

Enfin, le futur est préparé en définissant `promise->set_value()` et en lui transmettant l’objet `mip::FileProfile`.

```cpp
#include "profile_observer.h"
#include <future>

//Called when FileProfile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = 
  std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when FileProfile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement mip::FileEngine related observers.
```

Lorsque nous instancions une classe du kit SDK ou utilisons une fonction qui effectue des opérations asynchrones, nous passons l’implémentation des observateurs au constructeur de paramètres ou à la fonction asynchrone elle-même. Lors de l’instanciation de l’objet `mip::FileProfile::Settings`, le constructeur accepte `mip::FileProfile::Observer` comme l’un des paramètres. L’exemple ci-dessous montre notre objet `ProfileObserver` personnalisé, utilisé dans un constructeur `mip::FileProfile::Settings`.

## <a name="filehandler-observer-implementation"></a>Implémentation d’observateurs du gestionnaire de fichiers

De façon similaire à l’observateur de profil, l’objet `mip::FileHandler` implémente une classe `mip::FileHandler::Observers` pour la gestion des notifications d’événements asynchrones lors d’opérations de fichier. L’implémentation est similaire à celle détaillée ci-dessus. `FileHandlerObserver` est partiellement défini ci-dessous. 

### <a name="file_handler_observerh"></a>file_handler_observer.h

```cpp
#include "mip/file/file_handler.h"

class FileHandlerObserver final : public mip::FileHandler::Observer {
public:
  void OnCreateFileHandlerSuccess(
      const std::shared_ptr<mip::FileHandler>& fileHandler,
      const std::shared_ptr<void>& context) override;

  void OnCreateFileHandlerFailure(
      const std::exception_ptr& error,
      const std::shared_ptr<void>& context) override;

  //TODO: override remaining member functions inherited from mip::FileHandler::Observer
};
```

### <a name="file_handler_observercpp"></a>file_handler_observer.cpp

Cet exemple correspond simplement aux deux premières fonctions, mais les fonctions restantes utilisent un modèle similaire à celles-ci et à `ProfileObserver`.

```cpp
#include "file_handler_observer.h"

void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_value(fileHandler);
}

void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_exception(error);
}

//TODO: override remaining member functions inherited from mip::FileHandler::Observer
```

