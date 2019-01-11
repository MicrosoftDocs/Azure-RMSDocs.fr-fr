---
title: Concepts – Concepts principaux dans le kit SDK MIP – Profil et moteur
description: Cet article vous aidera à comprendre les concepts principaux du kit SDK, appelés profil et moteur, qui sont créés pendant l’initialisation de l’application.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 05a66dc7a00b976dfb9883f44b3c93a25b4b6975
ms.sourcegitcommit: 0d3b43c9cedbaeae65299ac372fbfb9ad66ce27f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54183624"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux objets de profil et de moteur

## <a name="profiles"></a>Profils

Le profil est la classe racine pour toutes les opérations dans le kit SDK MIP. Avant d’utiliser une des trois API, l’application cliente doit créer un profil. Les opérations ultérieures sont exécutées par le profil, ou par d’autres objets *ajouté* au profil.

Il existe trois types de profil dans le kit SDK MIP :

- [`PolicyProfile`](reference/class_mip_policyprofile.md): La classe de profil pour l’API de stratégie MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): La classe de profil pour l’API de Protection MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md): La classe de profil pour l’API de fichier MIP.

L’API utilisée dans l’application consommatrice détermine quelle classe de profil doit être utilisé.

Le profil lui-même offre les fonctionnalités suivantes :

- Il définit l’emplacement de stockage de l’état du kit SDK. Les données d’état incluent les détails de l’utilisateur, les stratégies d’utilisateur téléchargées, les journaux et les données de télémétrie.
- Il définit si l’état doit être chargé en mémoire ou enregistré sur le disque.
- Il gère l’authentification en acceptant un `mip::AuthDelegate`.
- Il définit l’ID d’application et un nom convivial de l’application qui consomme le kit SDK.

### <a name="profile-settings"></a>Paramètres de profil

- `Path`: Chemin d’accès de fichier sous l’enregistrement, données de télémétrie et les autres état persistant est stocké.
- `useInMemoryStorage`: Une valeur booléenne qui définit si l’état doit être stocké en mémoire, ou sur le disque.
- `authDelegate`: Un pointeur partagé de la classe `mip::AuthDelegate`. 
- `consentDelegate`: Un pointeur partagé de classe [ `mip::ConsentDelegate` ](reference/class_consentdelegate.md). 
- `observer`: Un pointeur partagé vers le profil `Observer` implémentation (dans [ `PolicyProfile` ](reference/class_mip_policyprofile_observer.md), [ `ProtectionProfile` ](reference/class_mip_protectionprofile_observer.md), et [ `FileProfile` ](reference/class_mip_fileprofile_observer.md)).
- `applicationInfo`: Un [ `mip::ApplicationInfo` ](reference/mip-enums-and-structs.md#structures) objet. Informations sur l’application qui consomme le SDK, qui correspond à votre ID d’inscription de l’application Azure Active Directory et le nom.

## <a name="engines"></a>Moteurs

Les moteurs de fichier, le profil et API de Protection de fournissent une interface pour les opérations effectuées pour une identité spécifique. Un seul moteur est ajouté à l’objet de profil pour chaque utilisateur qui se connecte à l’application. Toutes les opérations effectuées par le moteur sont dans le contexte de cette identité.

Il existe trois classes de moteur dans le kit SDK, une pour chaque API. La liste suivante montre les classes de moteur et quelques fonctions associées à chacune :

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`: Obtient la liste des étiquettes pour le moteur chargé.
  - `GetSensitivityLabel()`: Obtient l’étiquette à partir de contenu existant.
  - `ComputeActions()`: Fournie avec un ID de l’étiquette et éventuellement les métadonnées, renvoie la liste des actions qui doivent se produire pour un élément spécifique.
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`: Obtient la liste des étiquettes pour le moteur chargé.
  - `CreateFileHandler()`: Crée un `mip::FileHandler` pour un fichier spécifique ou un flux.

### <a name="engine-states"></a>États de moteur

Un moteur peut avoir deux états différents :

- `CREATED`: Créé indique que le Kit de développement logiciel possède suffisamment d’informations état local après l’appel de services principaux requis.
- `LOADED`: Le SDK a intégré les structures de données requises pour le moteur soit opérationnelle.

Un moteur doit être à la fois créé et chargé pour effectuer des opérations quelconques. La classe `Profile` expose plusieurs méthodes de gestion du moteur : `AddEngineAsync`, `RemoveEngineAsync` et `UnloadEngineAsync`.

Le tableau suivant décrit les états possibles de moteur, et les méthodes qui peuvent modifier cet état :

|         | NONE              | CRÉÉ           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NONE    |                   |                   | AddEngineAsync |
| CRÉÉ | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>ID de moteur

Chaque moteur possède un identificateur unique, `id`, qui est utilisé dans toutes les opérations de gestion du moteur. L’application peut fournir un `id`, ou le Kit de développement peut généré un, si elle n’est pas fourni par l’application. Toutes les autres propriétés du moteur (par exemple, l’adresse de messagerie dans les informations d’identité) sont des charges utiles opaques pour le kit SDK. Le kit SDK n’exécute AUCUNE logique pour maintenir uniques les autres propriétés ou appliquer d’autres contraintes.

### <a name="engine-management-methods"></a>Méthodes de gestion du moteur

Comme mentionné précédemment, il existe trois méthodes de gestion de moteur dans le SDK : `AddEngineAsync`, `DeleteEngineAsync`, et `UnloadEngineAsync`.

#### <a name="addengineasync"></a>AddEngineAsync

Cette méthode charge un moteur existant ou crée un s’il n’existe pas dans l’état local.

Si l’application ne fournit pas un `id`, `AddEngineAsync` génère un nouvel `id`. Elle vérifie alors si un moteur doté de cet `id` existe déjà dans l’état local. Dans l’affirmative, elle charge ce moteur. Si le moteur *n’existe pas* dans l’état local, un nouveau moteur est créé en appelant les API et les services backend nécessaires.

Dans les deux cas, si la méthode réussit, le moteur est chargé et prêt à être utilisé.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Supprime le moteur avec l’objet `id` donné. Toutes les traces du moteur sont supprimées de l’état local.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Décharge les structures de données en mémoire pour le moteur avec l’objet `id` donné. L’état local de ce moteur est toujours intact et peut être rechargé avec `AddEngineAsync`.

Cette méthode permet à l’application à être judicieuse sur l’utilisation de la mémoire par les moteurs de déchargement qui ne sont pas censés être utilisés plus tôt.

## <a name="next-steps"></a>Étapes suivantes

- Ensuite, découvrez plus en détails les [concepts d’authentification](concept-authentication-cpp.md) et les [observateurs](concept-async-observers.md). MIP fournit un modèle d’authentification extensible, tandis que les observateurs sont utilisés pour fournir des notifications d’événements pour les événements asynchrones. Les deux sont des éléments fondamentaux et s’appliquent à tous les ensembles d’API de MIP.
- Ensuite, étudiez les concepts de profil et de moteur pour les API de fichier, de stratégie et de protection
  - [Concepts de profil de l’API de fichier](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de fichier](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de stratégie](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de stratégie](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de protection](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de protection](concept-profile-engine-file-engine-cpp.md)  
