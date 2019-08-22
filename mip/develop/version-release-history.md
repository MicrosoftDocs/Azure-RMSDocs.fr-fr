---
title: Historique des versions et politique de support de Microsoft Information Protection (MIP) SDK
description: Guide de démarrage rapide vous montrant comment écrire la logique d’initialisation pour des applications clientes du kit SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/08/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: c2a5d89bf318d9e685d00033ba3ad53915659cdb
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882667"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Historique des versions et politique de support de Microsoft Information Protection (MIP) SDK

## <a name="servicing"></a>Maintenance 

Chaque version de disponibilité générale (GA) est prise en charge pendant six mois après la publication de la prochaine version GA. La documentation peut ne pas inclure d’informations sur les versions non prises en charge. Les correctifs et les nouvelles fonctionnalités s’appliquent uniquement à la dernière version GA.

Les versions préliminaires ne doivent pas être déployées en production. Au lieu de cela, utilisez la version préliminaire la plus récente pour tester les nouvelles fonctionnalités ou les correctifs fournis dans la prochaine version GA. Seule la version préliminaire la plus récente est prise en charge.

## <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés ou les modifications apportées à une version prise en charge. La dernière version est répertoriée en première position. 

> [!NOTE]
> Les correctifs mineurs ne sont pas répertoriés. par conséquent, si vous rencontrez un problème avec le kit de développement logiciel (SDK), nous vous recommandons de vérifier s’il est corrigé avec la dernière version de la mise à la disposition générale. Si le problème persiste, consultez la préversion actuelle.
>  
> Pour obtenir un support technique, consultez le [forum Stack Overflow Microsoft information protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection). 


## <a name="version-130"></a>Version 1.3.0

**Date de publication**: TBD

## <a name="version-120"></a>Version 1.2.0

**Date de publication**: Le 15 avril 2019

## <a name="version-110"></a>Version 1.1.0

**Date de publication**: Le 15 janvier 2019

Cette version introduit la prise en charge des plateformes suivantes:

  - .NET
  - Kit de développement logiciel (SDK) iOS (API de stratégie)
  - Android SDK (API de stratégie et API de protection)

**Nouvelles fonctionnalités :**

- Support ADRMS
- Les opérations de l’API de protection sont véritablement asynchrones (sur Win32), ce qui permet des opérations de chiffrement/déchiffrement non bloquantes simultanées.
  - Les rappels d’application (AuthDelegate, HTTPDelegate, etc.) peuvent maintenant être appelés sur *n’importe quel thread d'* arrière-plan
- Les propriétés des légendes personnalisées définies par les administrateurs informatiques peuvent désormais être lues via MIP:: Label:: GetCustomSettings
- La licence de publication sérialisée peut maintenant être récupérée directement à partir d’un fichier sans aucune opération HTTP via MIP:: FileHandler:: GetSerializedPublishingLicense
- Les applications sont notifiées si une opération HTTP est requise pour terminer la création d’un MIP:: FileEngine/MIP::P olicyEngine via MIP:: FileProfile:: observer:: OnAddPolicyEngineStarting/MIP::P olicyProfile:: observer:: OnAddEngineStarting
- Détection de la nécessité ou non d’une date d’expiration pour la détection de contenu protégé avec la méthode de commodité MIP::P rotectionDescriptor::D oesContentExpire
- Classification
  - Les types de sensibilité (expressions régulières pour CC #, Passport #, etc.) peuvent être obtenus à partir du service SCC
    - Activez la fonctionnalité en définissant l’indicateur MIP:: FileEngine:: Settings/MIP::P olicyEngine:: Settings
    - Lire les types via MIP:: FileEngine:: ListSensitivityTypes/MIP::P olicyEngine:: ListSensitivityTypes
  - Les résultats de classification des utilitaires de numérisation de document externe peuvent être fournis à MIP pour conduire des étiquettes recommandées/obligatoires en fonction du contenu du document.
    - Passer les résultats au MIP via MIP:: FileExecutionState:: GetClassificationResults/MIP:: ExecutionState:: GetClassificationResults
    - MIP:: ApplyLabelAction et MIP:: RecommendLabelAction peuvent être retournés par MIP::P olicyEngine:: ComputeActions lorsque les résultats de classification correspondent à une règle de stratégie indiquant les étiquettes required/Recommended

- Nouvelles exigences:
  - Remplissage forcé des champs ID/nom/version MIP:: ApplicationInfo lors de la création de MIP:: FileProfile, MIP::P olicyProfile et MIP::P rotectionProfile
  - Les applications doivent implémenter l’interface MIP:: FileExecutionState lors de la création de MIP:: FileHandlers
  
- Exceptions mises à jour:
  - MIP:: NoAuthTokenError levée si le AuthDelegate de l’application retourne un jeton vide (en raison de l’annulation)
    - S’applique à la création de:
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - MIP:: NoPolicyError levée si le locataire n’est pas configuré pour les étiquettes
    - S’applique à la création de:
      - mip::FileEngine
      - mip::PolicyEngine
  - MIP:: ServiceDisabledError levée si le service RMS est désactivé pour un utilisateur/appareil/plateforme/client spécifique
    - S’applique à la création de:
      - mip::FileHandler
      - mip::ProtectionHandler
  - MIP:: NoPermissionsError levée si un utilisateur ne dispose pas des droits nécessaires pour déchiffrer un document ou si le contenu a expiré
    - S’applique à la création de:
      - mip::FileHandler
      - mip::ProtectionHandler

**Correctifs** :

TBD

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur les plateformes prises en charge et bien plus encore, consultez [FAQ et problèmes du SDK MIP](faqs-known-issues.md) .
- Pour plus d’informations sur la prise en main du kit de développement logiciel MIP [, consultez Installation et configuration du SDK MIP](setup-configure-mip.md) .
