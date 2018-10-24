---
title: Concepts – Objet de profil de l’API de protection
description: Cet article vous aidera à comprendre les concepts liés à l’objet de profil de protection qui est créé pendant l’initialisation de l’application.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ae6699212d45a6c8a2fa95f648e7f5a2be3de93e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445306"
---
# <a name="microsoft-information-protection-sdk---protection-api-profile-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au profil de l’API de protection

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

## <a name="load-a-profile"></a>Charger un profil

Maintenant que les objets `ProtectionProfileObserverImpl` et `AuthDelegateImpl` sont définis, nous allons les utiliser pour instancier `mip::ProtectionProfile`. La création de l'objet `mip::ProtectionProfile` nécessite [`mip::ProtectionProfile::Settings`](reference/class_mip_ProtectionProfile_settings.md).

### <a name="protectionprofilesettings-parameters"></a>Paramètres ProtectionProfile::Settings

- `std::string path` : le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant.
- `bool useInMemoryStorage` : définit si tous les états doivent être stockés en mémoire plutôt que sur le disque.
- `std::shared_ptr<mip::AuthDelegate> authDelegate` : un pointeur partagé de classe `mip::AuthDelegate`.
- `std::shared_ptr<mip::ProtectionProfile::Observer> observer` : un pointeur partagé vers l’implémentation de `ProtectionProfile::Observer`.
- `mip::ApplicationInfo applicationInfo` : objet. Utilisé pour définir des informations sur l’application qui consomme le kit SDK.

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

#### <a name="store-state-in-memory-only"></a>Stocker l’état en mémoire uniquement

```cpp
ProtectionProfile::Settings profileSettings(
    "",                                     //path to store settings
    true,                                   //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Paramètres de profil de lecture/écriture à partir du chemin de stockage sur disque

```cpp
ProtectionProfile::Settings profileSettings(
    "./mip_app_data",                       //path to store settings
    false,                                  //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

Ensuite, utilisez le modèle de promesse/futur pour charger `ProtectionProfile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<ProtectionProfile>>>();
auto profileFuture = profilePromise->get_future();
ProtectionProfile::LoadAsync(profileSettings, profilePromise);
```

Si nous avons chargé un profil et que l’opération a réussi, `ProtectionProfileObserverImpl::OnLoadSuccess`, notre implémentation de `mip::ProtectionProfile::Observer::OnLoadSuccess` est appelée. L’objet résultant ou le pointeur d’exception, ainsi que le contexte, sont transmis comme paramètres à la fonction. Le contexte est un pointeur vers l’objet `std::promise` que nous avons créé pour gérer l’opération asynchrone. La fonction définit simplement la valeur de la promesse sur l’objet ProtectionProfile (contexte). Lorsque la fonction principale utilise `Future.get()`, le résultat peut être stocké dans un nouvel objet.

```cpp
//get the future value and store in profile.
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>Récapitulatif

Ayant pleinement implémenté les observateurs et le délégué d’authentification, il est désormais possible de charger complètement un profil. L’extrait de code ci-dessous suppose que tous les en-têtes nécessaires sont déjà inclus.

```cpp
int main()
{
    const string userName = "MyTestUser@contoso.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    ProtectionProfile::Settings profileSettings("",
        false,
        authDelegateImpl,
        std::make_shared<ConsentDelegateImpl>(),
        std::make_shared<ProfileObserver>(),
        mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    ProtectionProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Comme résultat final, nous avons correctement chargé le profil et stocké l’objet appelé `profile`.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que le profil a été ajouté, l’étape suivante consiste à ajouter un moteur au profil.

[Concepts liés au moteur de protection](concept-profile-engine-protection-engine-cpp.md)