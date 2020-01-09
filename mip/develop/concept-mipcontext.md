---
title: 'Concepts : concepts de base du kit de développement logiciel (SDK) MIP-MipContext'
description: Cet article vous aidera à comprendre le concept principal du kit de développement logiciel (SDK), appelé MipContext, qui pilote l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 97b6720a4501ab389099b7c2d49fa7cfbf81e00b
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555668"
---
# <a name="microsoft-information-protection-sdk---mipcontext-object-concepts"></a>Microsoft Information Protection SDK-concepts des objets MipContext

## <a name="mipcontext"></a>MipContext

`MipContext` est l’objet de niveau le plus élevé dans le kit de développement logiciel (SDK). Il est responsable de la gestion de l’État sur tous les profils qui peuvent être créés dans le cadre d’une application ou d’un service. En outre, il gère la libération des ressources du kit de développement logiciel (SDK) MIP une fois l’objet MipContext détruit.

Plus précisément, `MipContext` définit les éléments suivants :

- `mip::ApplicationInfo` dans le kit de développement logiciel (SDK), utilisé pour l’ID d’application, la version et le nom de l’application.
- Chemin d’accès où les informations d’État MIP doivent être stockées, si elles sont activées.
- Niveau de journalisation.
- Délégué d’enregistreur d’événements personnalisé, si vous le souhaitez.
- Remplacement de la configuration de la télémétrie.
- Activez les fonctionnalités en version préliminaire du kit de développement logiciel (SDK) qui se trouvent derrière les indicateurs de fonctionnalité.

Une fois qu’un objet de `mip::MipContext` a été créé, l’objet `MipContext` peut être utilisé pour créer des objets `mip::FileProfile` (ou `PolicyProfile`/`ProtectionProfile`).

### <a name="mipcontext-functions"></a>MipContext, fonctions

`mip::MipContext` expose trois fonctions statiques importantes utilisées pour créer et détruire des objets `MipContext`.

#### `mip::MipContext::Create()`

Crée une instance MipContext à utiliser lors de l’initialisation des profils. Cette fonction accepte les éléments suivants :

- `mip::ApplicationInfo`
- Chemin d’accès pour le cache de stockage MIP.
- `mip::LogLevel`
- (Facultatif) `mip::LoggerDelegate`
- (Facultatif) `mip::TelemetryConfiguration`

#### `mip::MipContext::CreateWithCustomFeatureSettings()`

Crée une nouvelle instance MipContext à utiliser lors de l’initialisation de profils, avec les paramètres de fonctionnalités personnalisés activés.

- `mip::ApplicationInfo`
- Chemin d’accès pour le cache de stockage MIP.
- `mip::LogLevel`
- (Facultatif) `mip::LoggerDelegate`
- (Facultatif) `mip::TelemetryConfiguration`
- `mip::FlightingFeature`

#### `mip::mipContext::Shutdown()`

Libère toutes les ressources MIP. Doit être appelé avant l’arrêt de l’application. Le destructeur `MipContext` l’appellera également lorsque l’objet `MipContext` sera détruit.

## <a name="next-steps"></a>Étapes suivantes

- Ensuite, découvrez plus en détails les [concepts d’authentification](concept-authentication-cpp.md) et les [observateurs](concept-async-observers.md). MIP fournit un modèle d’authentification extensible, tandis que les observateurs sont utilisés pour fournir des notifications d’événements pour les événements asynchrones. Les deux sont des éléments fondamentaux et s’appliquent à tous les ensembles d’API de MIP.
- Ensuite, étudiez les concepts de profil et de moteur pour les API de fichier, de stratégie et de protection
  - [Concepts de profil de l’API de fichier](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de fichier](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de stratégie](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de stratégie](concept-profile-engine-file-engine-cpp.md)
  - [Concepts de profil de l’API de protection](concept-profile-engine-file-profile-cpp.md)
  - [Concepts de moteur de l’API de protection](concept-profile-engine-file-engine-cpp.md)
