---
title: Concepts – Concepts principaux dans le kit SDK MIP – Profil et moteur
description: Cet article vous aidera à comprendre les concepts principaux du kit SDK, appelés profil et moteur, qui sont créés pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2019
ms.author: mbaldwin
ms.openlocfilehash: 193b65a392060e38731a1a8eda4c7565e82ca0df
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764126"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux objets de profil et de moteur

## <a name="profiles"></a>Profils

Où `MipContext` est la classe pour le stockage des paramètres propres au kit de développement logiciel (SDK), le profil est la classe racine pour toutes les opérations d’étiquetage MIP et de protection spécifiques dans le SDK MIP. Avant d’utiliser l’un des trois ensembles d’API, l’application cliente doit créer un profil. Les opérations ultérieures sont effectuées par le profil ou par d’autres objets *ajoutés* au profil.

Il existe trois types de profil dans le kit SDK MIP :

- [`PolicyProfile`](reference/class_mip_policyprofile.md): Classe de profil pour l’API de stratégie MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): Classe de profil pour l’API de protection MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md): Classe de profil pour l’API de fichier MIP.

L’API utilisée dans l’application consommatrice détermine la classe de profil à utiliser.

Le profil lui-même offre les fonctionnalités suivantes :

- Définit si l’État doit être chargé en mémoire ou rendu persistant sur le disque et, s’il est rendu persistant sur le disque, doit être chiffré.
- Définit le `mip::ConsentDelegate` qui doit être utilisé pour les opérations de consentement.
- Définit l' `mip::FileProfile::Observer` implémentation qui sera utilisée pour les rappels asynchrones pour les opérations de profil.

### <a name="profile-settings"></a>Paramètres du profil

- `MipContext`: L' `MipContext` objet qui a été initialisé pour stocker les informations sur l’application, le chemin d’accès à l’État, etc.
- `CacheStorageType`: Définit le mode de stockage de l’État : en mémoire, sur disque, sur disque et chiffré.
- `consentDelegate`: Pointeur partagé de la classe [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md).
- `observer`: Pointeur partagé vers l’implémentation de `Observer` profil (dans [`PolicyProfile`](reference/class_mip_policyprofile_observer.md), [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)et [`FileProfile`](reference/class_mip_fileprofile_observer.md)).
- `applicationInfo`: [`mip::ApplicationInfo`](reference/mip-enums-and-structs.md#structures) Objet. Informations sur l’application qui utilise le kit de développement logiciel (SDK), qui correspond à votre ID d’inscription et à votre nom d’application de Azure Active Directory.

## <a name="engines"></a>Moteurs

Les moteurs d’API de fichier, de profil et de protection fournissent une interface pour les opérations effectuées sur par une identité spécifique. Un moteur est ajouté à l’objet de profil pour chaque utilisateur ou principal de service qui se connecte à l’application. Il est possible d’effectuer des opérations déléguées `mip::ProtectionSettings` via et le gestionnaire de fichiers ou de protection. Pour plus d’informations, consultez [la section paramètres de protection dans les concepts de fileHandler](concept-handler-file-cpp.md) .

Il existe trois classes de moteur dans le kit SDK, une pour chaque API. La liste suivante montre les classes de moteur et quelques fonctions associées à chacune :

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()` : obtient la liste des étiquettes pour le moteur chargé.
  - `GetSensitivityLabel()` : obtient l’étiquette issue du contenu existant.
  - `ComputeActions()` : fournie avec un ID d’étiquette et des métadonnées facultatives, retourne la liste des actions qui doivent se produire pour un élément spécifique.
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()` : obtient la liste des étiquettes pour le moteur chargé.
  - `CreateFileHandler()` : crée un `mip::FileHandler` pour un flux ou un fichier spécifique.

La création d’un moteur requiert la transmission d’un objet de paramètres de moteur spécifique qui contient les paramètres pour le type de moteur à créer. L’objet Settings permet au développeur de spécifier des détails sur l’identificateur du moteur `mip::AuthDelegate` , l’implémentation, les paramètres régionaux et les paramètres personnalisés, ainsi que d’autres détails spécifiques à l’API.

### <a name="engine-states"></a>États de moteur

Un moteur peut avoir deux états différents :

- `CREATED` : indique que le kit SDK possède suffisamment d’informations d’état local après l’appel aux services backend requis.
- `LOADED` : le SDK a généré les structures de données requises pour que le moteur soit opérationnel.

Un moteur doit être à la fois créé et chargé pour effectuer des opérations quelconques. La classe `Profile` expose plusieurs méthodes de gestion du moteur : `AddEngineAsync`, `RemoveEngineAsync` et `UnloadEngineAsync`.

Le tableau suivant décrit les États de moteur possibles et les méthodes qui peuvent modifier cet État :

|         | Aucune              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| Aucune    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>ID du moteur

Chaque moteur possède un identificateur unique, `id`, qui est utilisé dans toutes les opérations de gestion du moteur. L’application peut fournir un `id`ou le kit de développement logiciel (SDK) peut en générer un, s’il n’est pas fourni par l’application. Toutes les autres propriétés du moteur (par exemple, l’adresse de messagerie dans les informations d’identité) sont des charges utiles opaques pour le kit SDK. Le kit SDK n’exécute AUCUNE logique pour maintenir uniques les autres propriétés ou appliquer d’autres contraintes.

> [!IMPORTANT]
> Il est recommandé d’utiliser un ID de moteur qui est propre à l’utilisateur et de l’utiliser chaque fois que l’utilisateur effectue une opération avec le kit de développement logiciel (SDK). L’échec de la fourniture d’un ID de moteur existant entraîne des allers-retours supplémentaires vers la stratégie de récupération et récupère les licences qui ont peut-être déjà été mises en cache pour le moteur existant.

### <a name="engine-management-methods"></a>Méthodes de gestion du moteur

Comme mentionné précédemment, il existe trois méthodes de gestion des moteurs dans le `AddEngineAsync`Kit `DeleteEngineAsync`de développement `UnloadEngineAsync`logiciel (SDK) :, et.

#### <a name="addengineasync"></a>AddEngineAsync

Cette méthode charge un moteur existant ou en crée un s’il n’existe pas déjà dans l’état local.

Si l’application ne fournit pas un `id`, `AddEngineAsync` génère un nouvel `id`. Elle vérifie alors si un moteur doté de cet `id` existe déjà dans l’état local. Dans l’affirmative, elle charge ce moteur. Si le moteur *n’existe pas* dans l’état local, un nouveau moteur est créé en appelant les API et les services backend nécessaires.

Dans les deux cas, si la méthode réussit, le moteur est chargé et prêt à être utilisé.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Supprime le moteur avec l’objet `id` donné. Toutes les traces du moteur sont supprimées de l’état local.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Décharge les structures de données en mémoire pour le moteur avec l’objet `id` donné. L’état local de ce moteur est toujours intact et peut être rechargé avec `AddEngineAsync`.

Cette méthode permet à l’application d’être judicieuse en ce qui concerne l’utilisation de la mémoire, en déchargeant les moteurs qui ne sont pas censés être utilisés prochainement.

## <a name="next-steps"></a>Étapes suivantes

- Ensuite, découvrez plus en détails les [concepts d’authentification](concept-authentication-cpp.md) et les [observateurs](concept-async-observers.md). MIP fournit un modèle d’authentification extensible, tandis que les observateurs sont utilisés pour fournir des notifications d’événements pour les événements asynchrones. Les deux sont des éléments fondamentaux et s’appliquent à tous les ensembles d’API de MIP.
- Ensuite, étudiez les concepts de profil et de moteur pour les API de fichier, de stratégie et de protection
  - [Concepts de profil de l’API de fichier](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de fichier](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de stratégie](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de stratégie](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de protection](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de protection](concept-profile-engine-file-engine-cpp.md)  
