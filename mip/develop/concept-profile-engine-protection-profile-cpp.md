---
title: Concepts – Objet de profil de l’API de protection
description: Cet article vous aidera à comprendre les concepts liés à l’objet de profil de protection qui est créé pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 45234963d7401107dca26a4c461e92818226465b
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555226"
---
# <a name="microsoft-information-protection-sdk---protection-api-profile-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au profil de l’API de protection

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

## <a name="load-a-profile"></a>Charger un profil

Maintenant que les objets `ProtectionProfileObserverImpl` et `AuthDelegateImpl` sont définis, nous allons les utiliser pour instancier `mip::ProtectionProfile`. La création de l'objet `mip::ProtectionProfile` nécessite [`mip::ProtectionProfile::Settings`](reference/class_mip_ProtectionProfile_settings.md).

### <a name="protectionprofilesettings-parameters"></a>Paramètres ProtectionProfile::Settings

- `std::shared_ptr<MipContext>`: objet `mip::MipContext` qui a été initialisé pour stocker les informations sur l’application, le chemin d’accès à l’État, etc.
- `mip::CacheStorageType`: définit le mode de stockage de l’État : en mémoire, sur disque, sur disque et chiffré.
- `std::shared_ptr<mip::AuthDelegate>` : un pointeur partagé de classe `mip::AuthDelegate`.
- `std::shared_ptr<mip::ConsentDelegate>`: pointeur partagé de la classe [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md).
- `std::shared_ptr<mip::ProtectionProfile::Observer> observer`: pointeur partagé vers l’implémentation du profil `Observer` (dans [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)et [`FileProfile`](reference/class_mip_fileprofile_observer.md)).

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

#### <a name="store-state-in-memory-only"></a>Stocker l’état en mémoire uniquement

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

ProtectionProfile::Settings profileSettings(
    mipContext,                                        // mipContext object
    mip::CacheStorageType::InMemory,                   // use in memory storage
    authDelegateImpl,                                  // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),           // new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Paramètres de profil de lecture/écriture à partir du chemin de stockage sur disque

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

ProtectionProfile::Settings profileSettings(
    mipContext,                                         // mipContext object
    mip::CacheStorageType::OnDisk,                      // use on disk storage
    authDelegateImpl,                                   // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),            // new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>()); // new protection profile
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

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    ProtectionProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
        std::make_shared<ProfileObserver>());          // new protection profile observer

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
