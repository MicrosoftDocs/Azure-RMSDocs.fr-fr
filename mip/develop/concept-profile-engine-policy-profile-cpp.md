---
title: Concepts – Objet de profil de l’API de stratégie
description: Cet article vous aidera à comprendre les concepts liés à l’objet de profil de stratégie qui est créé pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: bdc72bc3da8added696733cb271116764d0fd0c7
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764046"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au profil de l’API de stratégie

L’objet `mip::Profile` doit être chargé avant que des opérations de l’API de stratégie puissent être effectuées.

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. 

## <a name="load-a-profile"></a>Charger un profil

Maintenant que les objets `MipContext` et `ProfileObserver` sont définis, nous allons les utiliser pour instancier `mip::PolicyProfile`. La création `mip::PolicyProfile` de l' [`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md) objet `mip::MipContext`requiert et.

### <a name="profilesettings-parameters"></a>Paramètres Profile::Settings

Le `PolicyProfile::Settings` constructeur accepte quatre paramètres, répertoriés ci-dessous :

- `const std::shared_ptr<MipContext>`: L' `mip::MipContext` objet qui a été initialisé pour stocker les informations sur l’application, le chemin d’accès à l’État, etc.
- `mip::CacheStorageType`: Définit le mode de stockage de l’État : en mémoire, sur disque, sur disque et chiffré. Pour plus d’informations, consultez [concepts de stockage du cache](concept-cache-storage.md).
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`: Pointeur partagé vers l’implémentation de `Observer` profil (dans [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)et [`FileProfile`](reference/class_mip_fileprofile_observer.md)).

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. 

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
    std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer
```

Ensuite, utilisez le modèle de promesse/futur pour charger `Profile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<Profile>>>();
auto profileFuture = profilePromise->get_future();
Profile::LoadAsync(profileSettings, profilePromise);
```

Si un profil est chargé avec succès, `ProfileObserver::OnLoadSuccess`, notre implémentation de `mip::Profile::Observer::OnLoadSuccess` est avertie. L’objet résultant, un objet `mip::Profile` dans notre cas, ainsi que le contexte, sont transmis comme paramètres à la fonction d’observateur.

Le *contexte* est un pointeur vers le `std::promise` que nous avons créé pour gérer l’opération asynchrone. La fonction définit simplement la valeur de la promesse sur l’objet de profil qui a été transmis pour le premier paramètre. Lorsque la fonction principale utilise `Future.get()`, le résultat peut être stocké dans un nouvel objet dans le thread appelant.

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
 
    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    PolicyProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
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
