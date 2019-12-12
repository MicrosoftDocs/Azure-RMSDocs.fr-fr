---
title: Concepts – Objet de profil de l’API de stratégie
description: Cet article vous aidera à comprendre les concepts liés à l’objet de profil de stratégie qui est créé pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 9b3b32464cae35560c74a05b28506ca60dc963d2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "69886049"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au profil de l’API de stratégie

L’objet `mip::Profile` doit être chargé avant que des opérations de l’API de stratégie puissent être effectuées.

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

## <a name="load-a-profile"></a>Charger un profil

Maintenant que les `MipContext`, `ProfileObserver`et `AuthDelegateImpl` sont définis, nous les utiliserons pour instancier `mip::PolicyProfile`. La création de l’objet `mip::PolicyProfile` nécessite [`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md) et `mip::MipContext`.

### <a name="profilesettings-parameters"></a>Paramètres Profile::Settings

Le constructeur `PolicyProfile::Settings` accepte quatre paramètres, répertoriés ci-dessous :

- `const std::shared_ptr<MipContext>`: objet `mip::MipContext` qui a été initialisé pour stocker les informations sur l’application, le chemin d’accès à l’État, etc.
- `mip::CacheStorageType`: définit le mode de stockage de l’État : en mémoire, sur disque, sur disque et chiffré. Pour plus d’informations, consultez [concepts de stockage du cache](concept-cache-storage.md).
- `std::shared_ptr<mip::AuthDelegate>` : un pointeur partagé de classe `mip::AuthDelegate`.
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`: pointeur partagé vers l’implémentation du profil `Observer` (dans [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)et [`FileProfile`](reference/class_mip_fileprofile_observer.md)).

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

#### <a name="store-state-in-memory-only"></a>Stocker l’état en mémoire uniquement

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                   // mipContext object
    mip::CacheStorageType::InMemory,              // use in memory storage
    authDelegateImpl,                             // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Paramètres de profil de lecture/écriture à partir du chemin de stockage sur disque

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                    // mipContext object
    mip::CacheStorageType::OnDisk,                 // use on disk storage
    authDelegateImpl,                              // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer
```

Ensuite, utilisez le modèle de promesse/futur pour charger `Profile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<Profile>>>();
auto profileFuture = profilePromise->get_future();
Profile::LoadAsync(profileSettings, profilePromise);
```

Si un profil est chargé avec succès, `ProfileObserver::OnLoadSuccess`, notre implémentation de `mip::Profile::Observer::OnLoadSuccess` est avertie. L’objet résultant, un objet `mip::Profile` dans notre cas, ainsi que le contexte, sont transmis comme paramètres à la fonction d’observateur.

Le *contexte* est un pointeur vers l’objet `std::promise` que nous avons créé pour gérer l’opération asynchrone. La fonction définit simplement la valeur de la promesse sur l’objet de profil qui a été transmis pour le premier paramètre. Lorsque la fonction principale utilise `Future.get()`, le résultat peut être stocké dans un nouvel objet dans le thread appelant.

```cpp
//get the future value and store in profile.
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>Récapitulatif

Ayant pleinement implémenté les observateurs et le délégué d’authentification, il est désormais possible de charger complètement un profil. L’extrait de code ci-dessous suppose que tous les en-têtes nécessaires sont déjà inclus.

```cpp
int main()
{
    const string userName = "MyTestUser@consoto.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    PolicyProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer

    auto profilePromise = std::make_shared<promise<shared_ptr<PolicyProfile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Comme résultat final, nous avons correctement chargé le profil et stocké l’objet appelé `profile`.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que le profil a été ajouté, l’étape suivante consiste à ajouter un moteur au profil.

[Concepts liés au moteur de stratégie](concept-profile-engine-policy-engine-cpp.md)
