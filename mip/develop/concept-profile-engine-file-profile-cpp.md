---
title: Concepts – Objet de profil de l’API de fichier
description: Cet article vous aidera à comprendre les concepts liés à l’objet de profil de fichier qui est créé pendant l’initialisation de l’application.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 33ec266068d15e827267b7d518344aebd0f8f072
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445901"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au profil de l’API de fichier

Le profil est la classe racine pour toutes les opérations dans le kit SDK MIP. Avant d’utiliser toute fonctionnalité de l’API de fichier, un objet `FileProfile` doit être créé et toutes les opérations futures seront effectuées par ce profil ou par d’autres objets *ajoutés* à ce profil.

Certaines exigences de code doivent être remplies avant d’essayer d’instancier un profil :

- `AuthDelegateImpl` est implémenté pour étendre `mip::AuthDelegate`.
- `ConsentDelegateImpl` est implémenté pour étendre `mip::ConsentDelegate`.
- L’application a été [inscrite dans Azure Active Directory](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) et l’ID client est codé en dur dans les fichiers de configuration ou d’application. 
- Une classe héritant de `mip::FileProfile::Observer` a été correctement implémentée.

## <a name="load-a-profile"></a>Charger un profil

Les objets `ProfileObserver`, `ConsentDelegateImpl` et `AuthDelegateImpl` ayant été définis, `mip::FileProfile` peut maintenant être instancié. La création de l’objet `mip::FileProfile` nécessite [`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) pour stocker toutes les informations de paramétrage concernant `FileProfile`.

### <a name="fileprofilesettings-parameters"></a>Paramètres FileProfile::Settings

Le constructeur `FileProfile::Settings` accepte cinq paramètres, répertoriés ci-dessous :

- `std::string path` : le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant.
- `bool useInMemoryStorage` : définit si tous les états doivent être stockés en mémoire plutôt que sur le disque.
- `std::shared_ptr<mip::AuthDelegate> authDelegate` : un pointeur partagé de classe `mip::AuthDelegate`. 
- `std::shared_ptr<mip::ConsentDelegate>` : 
- `std::shared_ptr<mip::FileProfile::Observer> observer` : un pointeur partagé vers l’implémentation de `FileProfile::Observer`.
- `mip::ApplicationInfo applicationInfo` : objet. Utilisé pour définir des informations sur l’application qui consomme le kit SDK.

Les exemples ci-dessous montrent comment créer l’objet `profileSettings` en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

#### <a name="store-state-in-memory-only"></a>Stocker l’état en mémoire uniquement

```cpp
FileProfile::Settings profileSettings(
    "",                                          //path to store settings
    true,                                        //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Paramètres de profil de lecture/écriture à partir du chemin de stockage sur disque

L’extrait de code suivant indiquera à l’objet `FileProfile` de stocker toutes les données d’état d’application dans `./mip_app_data`.

```cpp
FileProfile::Settings profileSettings(
    "./mip_app_data",                            //path to store settings
    false,                                       //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
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
    const string userName = "MyTestUser@consoto.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    FileProfile::Settings profileSettings("",
            false,
            authDelegateImpl,
            std::make_shared<ConsentDelegateImpl>(),
            std::make_shared<ProfileObserver>(),
            mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

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