---
title: Concepts – Objet de profil de l’API de stratégie
description: Cet article vous aidera à comprendre les concepts liés à l’objet de profil de stratégie qui est créé pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: f9bb02dd4508b5e09761b3684a2a4e6d92224b6a
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60175328"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au profil de l’API de stratégie

L’objet `mip::Profile` doit être chargé avant que des opérations de l’API de stratégie puissent être effectuées.

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

## <a name="load-a-profile"></a>Charger un profil

Maintenant que les objets `ProfileObserver` et `AuthDelegateImpl` sont définis, nous allons les utiliser pour instancier `mip::PolicyProfile`. La création de l'objet `mip::PolicyProfile` nécessite [`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md).

### <a name="profilesettings-parameters"></a>Paramètres Profile::Settings

- `std::string path`: Chemin d’accès de fichier sous l’enregistrement, données de télémétrie et les autres état persistant est stocké.
- `bool useInMemoryStorage`: Définit ou non tous les États doivent être stockées en mémoire et non sur le disque.
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: Un pointeur partagé de classe `mip::AuthDelegate` 
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`: Un pointeur partagé vers le `PolicyProfile::Observer` implémentation.
- `mip::ApplicationInfo applicationInfo` : objet. Utilisé pour définir des informations sur l’application qui consomme le kit SDK.

Les deux exemples ci-dessous montrent comment créer l’objet profileSettings en utilisant un stockage local pour le stockage de l’état, ainsi qu’un stockage en mémoire uniquement. Les deux supposent que l’objet `authDelegateImpl` a déjà été créé.

#### <a name="store-state-in-memory-only"></a>Stocker l’état en mémoire uniquement

```cpp
Profile::Settings profileSettings("",
    true,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Paramètres de profil de lecture/écriture à partir du chemin de stockage sur disque

```cpp
Profile::Settings profileSettings("./mip_app_data",
    false,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
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
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    Profile::Settings profileSettings("", false, authDelegateImpl, std::make_shared<ProfileObserver>(), mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<Profile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Comme résultat final, nous avons correctement chargé le profil et stocké l’objet appelé `profile`.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que le profil a été ajouté, l’étape suivante consiste à ajouter un moteur au profil.

[Concepts liés au moteur de stratégie](concept-profile-engine-policy-engine-cpp.md)
