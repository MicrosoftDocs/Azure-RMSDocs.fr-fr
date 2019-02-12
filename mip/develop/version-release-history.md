---
title: Version du Kit de développement logiciel Microsoft Information Protection (MIP) historique des versions et politique du support
description: Guide de démarrage rapide vous montrant comment écrire la logique d’initialisation pour des applications clientes du kit SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/08/2019
ms.author: bryanla
manager: barbkess
ms.openlocfilehash: 1d7b30832441180f8673e7430d7d32e8a58a5205
ms.sourcegitcommit: 8c2de5119105cf5d5bc91fcc2202b64e5a779e7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56082789"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Version du Kit de développement logiciel Microsoft Information Protection (MIP) historique des versions et politique du support

## <a name="servicing"></a>Maintenance 

Chaque version en disponibilité générale (GA) est pris en charge pour les six mois, une fois que la prochaine version GA est mise en production. La documentation peut ne pas inclure des informations sur les versions non pris en charge. Correctifs et nouvelles fonctionnalités sont uniquement appliqués à la dernière version GA.

Les versions préliminaires ne doivent pas être déployées en production. Au lieu de cela, utilisez la dernière version d’évaluation pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Version preview la plus récente est prise en charge.

## <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés et les modifications d’une version prise en charge. La dernière version est la première sur la liste. 

> [!NOTE]
> Correctifs mineurs ne sont pas répertoriés donc si vous rencontrez un problème avec le Kit de développement, nous vous recommandons de vérifier si elle est fixe avec la dernière version GA. Si le problème persiste, consultez la préversion actuelle.
>  
> Pour le support technique, visitez le [forum Stack Overflow Microsoft Information Protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection). 

## <a name="version-110"></a>Version 1.1.0.

**Date de publication**: TBD

Cette version introduit la prise en charge pour les plateformes suivantes :

  - .NET
  - iOS SDK (API de stratégie)
  - Kit de développement logiciel Android (stratégie d’API et API de Protection)

**Nouvelles fonctionnalités :**

- Prise en charge d’AD RMS
- Les opérations d’API de protection sont véritablement asynchrones (sur Win32), ce qui permet des opérations de chiffrement/déchiffrement simultanées non bloquant
  - Rappels d’application (authdelegate :, HTTPDelegate, etc.) peuvent désormais être appelés sur *n’importe quel* thread d’arrière-plan
- Propriétés des légendes personnalisées définies par les administrateurs informatiques peuvent désormais être lues via mip::Label::GetCustomSettings
- Licence de publication sérialisé peut désormais être extraites directement à partir d’un fichier sans toutes les opérations HTTP via mip::FileHandler::GetSerializedPublishingLicense
- Applications reçoivent une notification si une opération HTTP est nécessaire pour terminer la création d’un mip::FileEngine/mip::PolicyEngine via mip::FileProfile::Observer::OnAddPolicyEngineStarting / mip::PolicyProfile::Observer::OnAddEngineStarting
- Détection de contenu protégé a une date d’expiration ou pas a été simplifié avec plus de commodité méthode mip::ProtectionDescriptor::DoesContentExpire
- Classification :
  - Types de sensibilité (expressions regex pour CC #, passport #, etc.) peuvent être acquises à partir du service de contrôle de code source
    - Activer la fonctionnalité en définissant mip::FileEngine::Settings / indicateur MIP::policyengine :: Settings
    - Lire des types via mip::FileEngine::ListSensitivityTypes / mip::PolicyEngine::ListSensitivityTypes
  - Résultats de la classification à partir des utilitaires de scanneur de document externe peuvent être transmises à MIP pour piloter des étiquettes recommandé/requis en fonction du contenu du document
    - Passer les résultats à MIP via mip::FileExecutionState::GetClassificationResults / mip::ExecutionState::GetClassificationResults
    - MIP::ApplyLabelAction et mip::RecommendLabelAction peuvent être retournés par mip::PolicyEngine::ComputeActions lorsque les résultats de la classification correspond à une règle de stratégie indiquant les étiquettes requises/recommandé

- Nouvelles exigences :
  - Remplissage appliqué de ID/nom/version champs mip::ApplicationInfo lors de la création de mip::FileProfile, mip::PolicyProfile et mip::ProtectionProfile
  - Les applications doivent implémenter la nouvelle interface mip::FileExecutionState lors de la création de mip::FileHandlers
  
- Exceptions de mise à jour :
  - MIP::NoAuthTokenError levée si authdelegate : l’application retourne un jeton vide (en raison de l’annulation)
    - S’applique à la création de :
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - levée si le client n’est pas configuré pour les étiquettes de MIP::NoPolicyError
    - S’applique à la création de :
      - mip::FileEngine
      - mip::PolicyEngine
  - MIP::ServiceDisabledError levée si le service RMS est désactivé pour un utilisateur/appareil/plateforme/client spécifique
    - S’applique à la création de :
      - mip::FileHandler
      - mip::ProtectionHandler
  - MIP::NoPermissionsError levée si un utilisateur ne dispose pas des droits pour déchiffrer un document ou le contenu est arrivé à expiration
    - S’applique à la création de :
      - mip::FileHandler
      - mip::ProtectionHandler

**Correctifs** :

TBD

## <a name="next-steps"></a>Étapes suivantes

- Consultez [MIP SDK FAQ et problèmes](faqs-known-issues.md) pour plus d’informations sur les plateformes prises en charge et bien plus encore.
- Consultez [le programme d’installation du SDK MIP et configuration](setup-configure-mip.md) pour plus d’informations sur la prise en main avec le SDK MIP.