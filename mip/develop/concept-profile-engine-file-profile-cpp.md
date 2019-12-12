---
title: Concepts – Objet de profil de l’API de fichier
description: Cet article vous aidera à comprendre les concepts liés à l’objet de profil de fichier qui est créé pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 5534cf804422de2d02a53e8c21ceae77af52691d
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "69886092"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au profil de l’API de fichier

Le profil est la classe racine pour toutes les opérations dans le kit SDK MIP. Avant d’utiliser toute fonctionnalité de l’API de fichier, un objet `FileProfile` doit être créé et toutes les opérations futures seront effectuées par ce profil ou par d’autres objets *ajoutés* à ce profil.

Certaines exigences de code doivent être remplies avant d’essayer d’instancier un profil :

- `MipContext` a été créé et stocké dans un objet accessible à l’objet `mip::FileProfile`.
- L'objet `AuthDelegateImpl` implémente l'objet `mip::AuthDelegate`.
- L'objet `ConsentDelegateImpl` implémente l'objet `mip::ConsentDelegate`.
- L’application a été [inscrite dans Azure Active Directory](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) et l’ID client est codé en dur dans les fichiers de configuration ou d’application.
- Une classe héritant de `mip::FileProfile::Observer` a été correctement implémentée.

## <a name="load-a-profile"></a>Charger un profil

Les objets `ProfileObserver`, `ConsentDelegateImpl` et `AuthDelegateImpl` ayant été définis, `mip::FileProfile` peut maintenant être instancié. La création de l’objet `mip::FileProfile` nécessite que [`mip::MipContext`] ait et [`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) pour stocker toutes les informations de paramètres concernant le `FileProfile`.

### <a name="fileprofilesettings-parameters"></a>Paramètres FileProfile::Settings

Le constructeur `FileProfile::Settings` accepte cinq paramètres, répertoriés ci-dessous :

- `std::shared_ptr<MipContext>`: objet `mip::MipContext` qui a été initialisé pour stocker les informations sur l’application, le chemin d’accès à l’État, etc.
- `mip::CacheStorageType`: définit le mode de stockage de l’État : en mémoire, sur disque, sur disque et chiffré.
- `std::shared_ptr<mip::AuthDelegate>` : un pointeur partagé de classe `mip::AuthDelegate`.
- `std::shared_ptr<mip::ConsentDelegate>`: pointeur partagé de la classe [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md).
- `std::shared_ptr<mip::FileProfile::Observer> observer`: pointeur partagé vers l’implémentation du profil `Observer` (dans [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)et [`FileProfile`](reference/class_mip_fileprofile_observer.md)).

Les exemples ci-dessous montrent comment créer l’objet `profileSettings` en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

#### <a name="store-state-in-memory-only"></a>Stocker l’état en mémoire uniquement

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

FileProfile::Settings profileSettings(
    mipContext,                                   // mipContext object
    mip::CacheStorageType::InMemory,              // use in memory storage
    authDelegateImpl,                             // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),      // new consent delegate
    std::make_shared<FileProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Paramètres de profil de lecture/écriture à partir du chemin de stockage sur disque

L’extrait de code suivant indiquera à l’objet `FileProfile` de stocker toutes les données d’état d’application dans `./mip_app_data`.

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

FileProfile::Settings profileSettings(
    mipContext,                                    // mipContext object
    mip::CacheStorageType::OnDisk,                 // use on disk storage
    authDelegateImpl,                              // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
    std::make_shared<FileProfileObserverImpl>());  // new protection profile observer
```

#### <a name="load-the-profile"></a>Charger le profil

À l’aide des détails d’une des approches ci-dessus, utilisez maintenant le modèle de promesse/futur pour charger l’objet `FileProfile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<FileProfile>>>();
auto profileFuture = profilePromise->get_future();
FileProfile::LoadAsync(profileSettings, profilePromise);
```

Si nous avons chargé un profil et que l’opération a réussi, `ProfileObserver::OnLoadSuccess`, notre implémentation de `mip::FileProfile::Observer::OnLoadSuccess` est appelée. L’objet résultant ou le pointeur d’exception, ainsi que le contexte, sont transmis comme paramètres à la fonction. Le contexte est un pointeur vers l’objet `std::promise` que nous avons créé pour gérer l’opération asynchrone. La fonction définit simplement la valeur de la promesse sur l’objet FileProfile qui a été transmis pour le premier paramètre. Lorsque la fonction principale utilise `Future.get()`, le résultat peut être stocké dans un nouvel objet.

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

    FileProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
        std::make_shared<FileProfileObserverImpl>());  // new file profile observer

        auto profilePromise = std::make_shared<promise<shared_ptr<FileProfile>>>();
        auto profileFuture = profilePromise->get_future();
        FileProfile::LoadAsync(profileSettings, profilePromise);
        auto profile = profileFuture.get();
}
```

Comme résultat final, nous avons correctement chargé le profil et stocké l’objet appelé `profile`.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que le profil a été ajouté, l’étape suivante consiste à ajouter un moteur au profil. 

- [Concepts liés au moteur de fichier](concept-profile-engine-file-engine-cpp.md)
