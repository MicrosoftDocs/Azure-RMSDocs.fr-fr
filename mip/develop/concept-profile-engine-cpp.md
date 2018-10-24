---
title: Concepts – Concepts principaux dans le kit SDK MIP – Profil et moteur
description: Cet article vous aidera à comprendre les concepts principaux du kit SDK, appelés profil et moteur, qui sont créés pendant l’initialisation de l’application.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6f11944e7cceed39423af2a8104ce044d1f6eec6
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453416"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux objets de profil et de moteur

## <a name="profiles"></a>Profils

Le profil est la classe racine pour toutes les opérations dans le kit SDK MIP. Avant d’utiliser une des trois API, un profil doit être créé par l’application cliente. Toutes les opérations futures seront effectuées par ce profil ou par d’autres objets *ajoutés* à ce profil.

Il existe trois types de profil dans le kit SDK MIP :

- [`PolicyProfile`](reference/class_mip_policyprofile.md) : la classe de profil pour l’API de stratégie MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md) : la classe de profil pour l’API de protection MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md) : la classe de profil pour l’API de fichier MIP.

L’API utilisée dans l’application consommatrice détermine la classe de profil à utiliser.

Le profil lui-même offre les fonctionnalités suivantes :

- Il définit l’emplacement de stockage de l’état du kit SDK. Les données d’état incluent les détails de l’utilisateur, les stratégies d’utilisateur téléchargées, les journaux et les données de télémétrie.
- Il définit si l’état doit être chargé en mémoire ou enregistré sur le disque.
- Il gère l’authentification en acceptant un `mip::AuthDelegate`.
- Il définit l’ID d’application et un nom convivial de l’application qui consomme le kit SDK.

### <a name="profile-settings"></a>Paramètres du profil

- `Path` : le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant.
- `useInMemoryStorage` : une valeur booléenne qui définit si l’état doit être stocké en mémoire ou sur le disque.
- `authDelegate` : un pointeur partagé de classe `mip::AuthDelegate`. 
- `consentDelegate` : un pointeur partagé de classe `mip::ConsentDelegate`. 
- `observer` : un pointeur partagé vers l’implémentation `Observer` du profil (dans `PolicyProfile`, `ProtectionProfile` et `EngineProfile`).
- `applicationInfo` : un objet `mip::ApplicationInfo`. Informations sur l’application qui consomme le kit SDK.

## <a name="engines"></a>Moteurs

Dans les API de fichier, de profil et de protection, les moteurs fournissent une interface pour les opérations effectuées au nom d’une identité spécifique. Un seul moteur sera ajouté à l’objet de profil pour chaque utilisateur qui se connecte à l’application. Toutes les opérations effectuées par le moteur figureront dans le contexte de cette identité.

Il existe trois classes de moteur dans le kit SDK, une pour chaque API. La liste suivante montre les classes de moteur et quelques fonctions associées à chacune :

- [`mip::ProtectionEngine`]
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()` : obtient la liste des étiquettes pour le moteur chargé.
  - `GetSensitivityLabel()` : obtient l’étiquette issue du contenu existant.
  - `ComputeActions()` : fournie avec un ID d’étiquette et des métadonnées facultatives, retourne la liste des actions qui doivent se produire pour un élément spécifique.
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()` : obtient la liste des étiquettes pour le moteur chargé.
  - `CreateFileHandler()` : crée un `mip::FileHandler` pour un flux ou un fichier spécifique.

### <a name="engine-states"></a>États de moteur

Un moteur peut avoir deux états différents :

- `CREATED` : indique que le kit SDK possède suffisamment d’informations d’état local après l’appel aux services backend requis.
- `LOADED` : le SDK a généré les structures de données requises pour que le moteur soit opérationnel.

Un moteur doit être à la fois créé et chargé pour effectuer des opérations quelconques. La classe `Profile` expose plusieurs méthodes de gestion du moteur : `AddEngineAsync`, `RemoveEngineAsync` et `UnloadEngineAsync`.

Le tableau suivant décrit les états de moteur possibles et les méthodes permettant de modifier ces états.

|         | NONE              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NONE    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>ID du moteur

Chaque moteur possède un identificateur unique, `id`, qui est utilisé dans toutes les opérations de gestion du moteur. L’application peut fournir un `id` ou le kit SDK génère un nouvel identificateur unique, si l’application n’en fournit aucun. Toutes les autres propriétés du moteur (par exemple, l’adresse de messagerie dans les informations d’identité) sont des charges utiles opaques pour le kit SDK. Le kit SDK n’exécute AUCUNE logique pour maintenir uniques les autres propriétés ou appliquer d’autres contraintes.

### <a name="engine-management-methods"></a>Méthodes de gestion du moteur

Comme mentionné ci-dessus, il existe trois méthodes de gestion de moteur dans le kit SDK : `AddEngineAsync`, `DeleteEngineAsync` et `UnloadEngineAsync`.

#### <a name="addengineasync"></a>AddEngineAsync

Cette méthode charge un moteur existant ou en crée un nouveau s’il n’en existe pas déjà un dans l’état local.

Si l’application ne fournit pas un `id`, `AddEngineAsync` génère un nouvel `id`. Elle vérifie alors si un moteur doté de cet `id` existe déjà dans l’état local. Dans l’affirmative, elle charge ce moteur. Si le moteur *n’existe pas* dans l’état local, un nouveau moteur est créé en appelant les API et les services backend nécessaires.

Dans les deux cas, si la méthode réussit, le moteur est chargé et prêt à être utilisé.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Supprime le moteur avec l’objet `id` donné. Toutes les traces du moteur sont supprimées de l’état local.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Décharge les structures de données en mémoire pour le moteur avec l’objet `id` donné. L’état local de ce moteur est toujours intact et peut être rechargé avec `AddEngineAsync`.

Cette méthode permet à l’application d’agir de façon judicieuse quant à l’utilisation de la mémoire, en déchargeant les moteurs qui ne sont pas censés être utilisés à court terme.

## <a name="next-steps"></a>Étapes suivantes

- Ensuite, découvrez plus en détails les [concepts d’authentification](concept-authentication-cpp.md) et les [observateurs](concept-async-observers.md). MIP fournit un modèle d’authentification extensible, tandis que les observateurs sont utilisés pour fournir des notifications d’événements pour les événements asynchrones. Les deux sont des éléments fondamentaux et s’appliquent à tous les ensembles d’API de MIP.
- Ensuite, étudiez les concepts de profil et de moteur pour les API de fichier, de stratégie et de protection
  - [Concepts de profil de l’API de fichier](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de fichier](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de stratégie](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de stratégie](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de protection](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de protection](concept-profile-engine-file-engine-cpp.md)  
