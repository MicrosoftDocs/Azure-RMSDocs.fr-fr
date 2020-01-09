---
title: Historique des versions et politique de support de Microsoft Information Protection (MIP) SDK
description: Historique des versions et notes de modification pour le kit de développement logiciel MIP.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/25/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: c28ab93feedea4c27ef9fe032f889d17da078d49
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555940"
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

## <a name="version-140"></a>Version 1.4.0 

**Date de publication**: 6 novembre 2019

Cette version introduit la prise en charge de l’API de protection dans le package .NET (Microsoft. InformationProtection. file).

### <a name="sdk-changes"></a>Modifications du kit SDK
- Améliorations des performances et correctifs de bogues
- Énumération StorageType renommée en CacheStorageType
- Liens Android vers libc + + à la place de gnustl
- Suppression des API précédemment dépréciées
  - Fichier/stratégie/profil :: les paramètres doivent être initialisés avec un MipContext
  - Fichier/stratégie/profil :: paramètres chemin d’accès, informations sur l’application, déléguer enregistreur, télémétrie et les accesseurs get/set de niveau de journalisation ont été supprimés. Ces propriétés sont gérées par MipContext
- Meilleure prise en charge des bibliothèques statiques sur les plateformes Apple
  - Bibliothèques statiques monolithiques
    - libmip_file_sdk_static. a
    - libmip_upe_sdk_static. a
    - libmip_protection_sdk_static. a
    - libmip_upe_and_protection_sdk_static. a
  - dépendances tierces extraites dans des bibliothèques distinctes
    - libsqlite3. a
    - libssl. a
- Suppression de mip_telemetry. dll (fusionnée dans mip_core. dll)

### <a name="file-api"></a>API de fichier

- RPMSG
  - Chiffrement
  - Ajout de la prise en charge du déchiffrement String8
- Comportement d’extension PFILE configurable (par défaut, <EXT>. PFILE ou P<EXT>)
  - ProtectionSettings::SetPFileExtensionBehavior

### <a name="policy-api"></a>API de stratégie

- Terminer l’API C
- Configurer le filtrage des étiquettes associées à la protection
  - PolicyEngine :: paramètres :: SetLabelFilter ()

### <a name="protection-api"></a>API de protection

- Suppression des API précédemment dépréciées
  - Suppression de ProtectionEngine :: CreateProtectionHandlerFromDescriptor [Async] (utilisation de ProtectionEngine :: CreateProtectionHandlerForPublishing [Async])
  - Suppression de ProtectionEngine :: CreateProtectionHandlerFromPublishingLicense [Async] (utilisation de ProtectionEngine :: CreateProtectionHandlerForConsumption [Async])
- API C# complète
- Terminer l’API C
  - Modifications de la normalisation de l’API c à partir de la version préliminaire de l’API C 1.3 C :
    - Mip_cc_storage_type renommé en mip_cc_cache_storage_type
    - MIP_CC_AddProtectionProfileEngine renommé en MIP_CC_ProtectionProfile_AddEngine
    - MIP_CC_CreateProtectionEngineSettingsForExistingEngine renommé en MIP_CC_CreateProtectionEngineSettingsWithEng
    - MIP_CC_CreateProtectionEngineSettingsForNewEngine renommé en MIP_CC_CreateProtectionEngineSettingsWithIdentity
    - MIP_CC_SetProtectionProfileSettingsHttpDelegate renommé en MIP_CC_ProtectionProfileSettings_SetHttpDelegate
    - MIP_CC_CreateProtectionHandlerForConsumption renommé en MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption
    - MIP_CC_CreateProtectionHandlerForPublishing renommé en MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing
    - MIP_CC_GetProtectionEngineId renommé en MIP_CC_ProtectionEngine_GetEngineId
    - MIP_CC_GetProtectionEngineTemplates renommé en MIP_CC_ProtectionEngine_GetTemplates
    - MIP_CC_GetProtectionEngineTemplatesSize renommé en MIP_CC_ProtectionEngine_GetTemplatesSize
    - MIP_CC_SetTelemetryConfigurationHttpDelegate renommé en MIP_CC_TelemetryConfiguration_SetHttpDelegate
    - MIP_CC_SetTelemetryConfigurationHostName renommé en MIP_CC_TelemetryConfiguration_SetHostName
    - MIP_CC_SetTelemetryConfigurationIsLocalCachingEnabled renommé en MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled
    - MIP_CC_SetTelemetryConfigurationIsNetworkDetectionEnabled renommé en MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled
    - MIP_CC_SetTelemetryConfigurationIsTelemetryOptedOut renommé en MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut
    - MIP_CC_SetTelemetryConfigurationLibraryName renommé en MIP_CC_TelemetryConfiguration_SetLibraryName
    - Suppression de la MIP_CC_ProtectionEngine_GetRightsForLabelIdSize et de la mise à jour MIP_CC_ProtectionEngine_GetRightsForLabelId pour remplir un mip_cc_string_list au lieu d’une mémoire tampon de chaîne séparée par des virgules
    - Suppression de la MIP_CC_ProtectionHandler_GetRightsSize et de la mise à jour MIP_CC_ProtectionHandler_GetRights pour remplir un mip_cc_string_list au lieu d’une mémoire tampon de chaîne séparée par des virgules
    - Ajout de MIP_CC_ProtectionEngine_GetEngineIdSize et mise à jour MIP_CC_ProtectionEngine_GetEngineId pour remplir un tampon de chaîne au lieu d’un mip_cc_guid
    - MIP_CC_CreateProtectionDescriptorFromUserRights prend maintenant le paramètre « mip_cc_dictionary- » au lieu de « mip_cc_dictionary »
    - MIP_CC_ProtectionEngineSettings_SetCustomSettings prend maintenant le paramètre « mip_cc_dictionary- » au lieu de « mip_cc_dictionary »
    - MIP_CC_ProtectionProfileSettings_SetCustomSettings prend maintenant le paramètre « mip_cc_dictionary- » au lieu de « mip_cc_dictionary »
    - MIP_CC_TelemetryConfiguration_SetCustomSettings prend maintenant le paramètre « mip_cc_dictionary- » au lieu de « mip_cc_dictionary »
    - MIP_CC_CreateMipContext accepte les paramètres « isOfflineOnly » et « loggerDelegateOverride »


## <a name="version-130"></a>Version 1.3.0

**Date de publication**: 22 août 2019

### <a name="new-features"></a>Nouvelles fonctionnalités

- `mip::MipContext` est le nouvel objet de niveau supérieur.
- Le déchiffrement des fichiers de messages protégés est maintenant pris en charge.
- L’inspection des fichiers message. rpmsg est prise en charge via `mip::FileInspector` et `mip::FileHandler::InspectAsync()`.
- Le cache sur disque peut désormais être éventuellement chiffré.
- L’API de protection prend désormais en charge la Chine souveraine Cloud.
- Prise en charge d’Arm64 sur Android.
- Prise en charge d’Arm64e sur iOS.
- Le cache des licences utilisateur final peut désormais être désactivé.
- le chiffrement. pfile peut être désactivé via `mip::FileEngine::EnablePFile`
- Amélioration des performances pour les opérations de protection en réduisant le nombre d’appels HTTP
- Les détails de l’identité déléguée ont été supprimés de `mip::Identity` et ont été ajoutés à la place `DelegatedUserEmail` à `mip::FileEngine::Settings`, `mip::ProtectionSettings`, `mip::PolicyEngine::Settings`et `mip::ProtectionHandler`et `PublishingSettings` de `ConsumptionSettings`.
- Les fonctions qui retournaient précédemment ID retournent désormais un objet `mip::Label`.

### <a name="changes"></a>Modifications

* Dans les versions précédentes, nous avions requis que vous ayez appelé `mip::ReleaseAllResources`. La version 1,3 remplace ceci par `mip::MipContext::~MipContext` ou `mip::MipContext::Shutdown`.
* Suppression de `ActionSource` de `mip::LabelingOptions` et `mip::ExecutionState::GetNewLabelActionSource`
* `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` remplacé par `mip::ProtectionEngine::CreateProtectionHandlerForPublishing`.
* `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` remplacé par `mip::ProtectionEngine::CreateProtectionHandlerForConsumption`.
* Renommé `mip::PublishingLicenseContext` en `mip::PublishingLicenseInfo` et mis à jour pour contenir des champs enrichis au lieu d’octets sérialisés bruts.
* `mip::PublishingLicenseInfo` contient les données relatives au MIP après l’analyse d’une licence de publication (PL).
* `mip::TemplateNotFoundError` et `mip::LabelNotFoundError` levées lorsque l’application transmet MIP un ID de modèle ou un ID d’étiquette qui n’est pas reconnu.
* Ajout de la prise en charge de l’accès conditionnel basé sur les étiquettes via le paramètre claims de `AcquireToken()` et `mip::AuthDelegate::OAuth2Challenge()`. Cette fonctionnalité n’a pas encore été exposée par le biais du portail Centre de sécurité et conformité.


## <a name="version-120"></a>Version 1.2.0

**Date de publication**: 15 avril 2019

### <a name="new-features"></a>Nouvelles fonctionnalités

 - Le composant de télémétrie utilise désormais la même pile HTTP que le reste du MIP, même si l’application cliente l’a remplacée par HttpDelegate.
 - Les applications clientes peuvent contrôler le comportement de thread des tâches asynchrones en remplaçant TaskDispatcherDelegate dans les profils.
 - Chiffrement RPMSG maintenant en préversion.
 - Aligner le comportement de gestion des exceptions du SDK de fichier/de stratégie avec le kit de développement logiciel de protection :
    - ProxyAuthError levée par tous les kits de développement logiciel (SDK) si un proxy est configuré pour exiger une authentification.
    - NoAuthTokenError levée par tous les kits de développement logiciel si le jeton d’authentification vide est fourni par l’implémentation de l’application de MIP :: AuthDelegate :: AcquireOAuth2Token.
 - La mise en cache HTTP améliorée pour le SDK de stratégie réduit de moitié le nombre d’appels HTTP requis.
 - Journaux/audits/télémétrie plus enrichis pour améliorer la détection des défaillances et le débogage.
 - Prise en charge des étiquettes externes/étrangères pour faciliter la migration vers des étiquettes AIP.
 - Activation de la prise en charge des applications tierces pour télécharger les types de sensibilité à partir de SCC.
 - D’autres paramètres de télémétrie sont exposés et configurables (comportement de mise en cache/thread, etc.).
 
### <a name="sdk-changes"></a>Modifications du SDK

 - mip_common. dll se divise en mip_core. dll et mip_telemetry. dll.
 - MIP :: ContentState renommé MIP ::D ataState pour décrire la façon dont une application interagit avec les données à un niveau élevé.
 - l’exception MIP :: AdhocProtectionRequiredError est levée par FileHandler :: SetLabel pour avertir une application qu’elle doit d’abord appliquer une protection ad hoc avant d’appliquer une étiquette.
 - l’exception MIP :: OperationCancelledError est levée lorsqu’une opération a été annulée (par exemple, en raison de l’arrêt ou de l’annulation HTTP).
 - Nouvelles API :
    - MIP :: ClassificationResult :: GetSensitiveInformationDetections
    - MIP :: FileEngine :: GetLastPolicyFetchTime
    - MIP :: FileEngine :: GetDefaultSensitivityLabel
    - MIP :: FileEngine :: GetPolicyId
    - MIP :: FileEngine :: HasClassificationRules
    - MIP :: FileEngine :: Settings :: SetPolicyCloudEndpointBaseUrl
    - MIP :: FileHandler :: GetDecryptedTemporaryFileAsync
    - MIP :: FileHandler :: observer :: OnGetDecryptedTemporaryFileFailure
    - MIP :: FileHandler :: observer :: OnGetDecryptedTemporaryFileSuccess
    - MIP :: file/Policy/ProtectionProfile :: SetTaskDispatcherDelegate
    - MIP :: file/Policy/ProtectionProfile :: SetTelemetryConfiguration
    - MIP :: HttpRequest :: GetBody retourne std :: Vector < uint8_t > au lieu de std :: String
    - MIP :: HttpRequest :: GetId
    - MIP ::P olicyEngine :: GetLastPolicyFetchTime
    - MIP ::P olicyEngine :: GetPolicyId
    - MIP ::P olicyEngine :: HasClassificationRules
    - MIP ::P olicyEngine :: Settings :: SetCloudEndpointBaseUrl
    - MIP ::P rotectionDescriptor :: GetContentId
    - (interface) MIP :: TaskDispatcherDelegate
 
### <a name="new-requirements"></a>Nouvelles exigences
 - MIP :: ReleaseAllResources doit être appelé avant l’arrêt du processus (après avoir effacé les références à tous les profils, moteurs et gestionnaires)
 - (interface) MIP :: ExecutionState :: GetClassificationResults type de retour et le paramètre « classificationIds » a changé
 - (interface) MIP :: FileExecutionState :: GetAuditMetadata peut être implémenté par les applications pour spécifier des informations détaillées à faire figurer dans le tableau de bord d’audit d’un administrateur de locataire (par exemple, expéditeur, destinataires, dernière modification, etc.)
 - (interface) MIP :: FileExecutionState :: le type de retour de GetClassificationResults a changé, et il requiert désormais un paramètre FileHandler
 - (interface) MIP :: FileExecutionState :: GetDataState doit être implémenté par les applications pour spécifier comment une application interagit avec contentIdentifier
 - (interface) MIP :: HttpDelegate l’interface requiert les méthodes’CancelOperation’et’CancelAllOperations'
 - (interface) MIP :: HttpDelegate l’interface’Send’et’SendAsync’retournent MIP :: HttpOperation au lieu de MIP :: HttpResponse
 - (interface) MIP :: HttpResponse :: GetBody retourne std :: Vector < uint8_t > au lieu de std :: String
 - (interface) MIP :: HttpResponse l’interface requiert l’implémentation de la méthode’GetId'
 - MIP :: ContentLabel :: GetCreationTime retourne std :: Chrono :: time_point au lieu de std :: String
 - MIP :: FileEngine :: CreateFileHandlerAsync n’accepte plus le paramètre « contentIdentifier »
 - MIP ::P olicyHandler :: NotifyCommitedActions renommé MIP ::P olicyHandler :: NotifyCommittedActions


## <a name="version-110"></a>Version 1.1.0

**Date de publication**: 15 janvier 2019

Cette version introduit la prise en charge des plateformes suivantes :

  - .NET
  - Kit de développement logiciel (SDK) iOS (API de stratégie)
  - Android SDK (API de stratégie et API de protection)

### <a name="new-features"></a>Nouvelles fonctionnalités

- Support ADRMS
- Les opérations de l’API de protection sont véritablement asynchrones (sur Win32), ce qui permet des opérations de chiffrement/déchiffrement non bloquantes simultanées.
  - Les rappels d’application (AuthDelegate, HTTPDelegate, etc.) peuvent maintenant être appelés sur un thread en arrière-plan
- Les propriétés des légendes personnalisées définies par les administrateurs informatiques peuvent désormais être lues via MIP :: Label :: GetCustomSettings
- La licence de publication sérialisée peut maintenant être récupérée directement à partir d’un fichier sans aucune opération HTTP via MIP :: FileHandler :: GetSerializedPublishingLicense
- Les applications sont notifiées si une opération HTTP est requise pour terminer la création d’un MIP :: FileEngine/MIP ::P olicyEngine via MIP :: FileProfile :: observer :: OnAddPolicyEngineStarting/MIP ::P olicyProfile :: observer :: OnAddEngineStarting
- Détection de la nécessité ou non d’une date d’expiration pour la détection de contenu protégé avec la méthode de commodité MIP ::P rotectionDescriptor ::D oesContentExpire
- Classification :
  - Les types de sensibilité (expressions régulières pour CC #, Passport #, etc.) peuvent être obtenus à partir du service SCC
    - Activez la fonctionnalité en définissant l’indicateur MIP :: FileEngine :: Settings/MIP ::P olicyEngine :: Settings
    - Lire les types via MIP :: FileEngine :: ListSensitivityTypes/MIP ::P olicyEngine :: ListSensitivityTypes
  - Les résultats de classification des utilitaires de numérisation de document externe peuvent être fournis à MIP pour conduire des étiquettes recommandées/obligatoires en fonction du contenu du document.
    - Passer les résultats au MIP via MIP :: FileExecutionState :: GetClassificationResults/MIP :: ExecutionState :: GetClassificationResults
    - MIP :: ApplyLabelAction et MIP :: RecommendLabelAction peuvent être retournés par MIP ::P olicyEngine :: ComputeActions lorsque les résultats de classification correspondent à une règle de stratégie indiquant les étiquettes required/Recommended

### <a name="new-requirements"></a>Nouvelles exigences 

  - Remplissage forcé des champs ID/nom/version MIP :: ApplicationInfo lors de la création de MIP :: FileProfile, MIP ::P olicyProfile et MIP ::P rotectionProfile
  - Les applications doivent implémenter l’interface MIP :: FileExecutionState lors de la création de MIP :: FileHandlers
  
### <a name="new-exceptions"></a>Nouvelles exceptions 

  - MIP :: NoAuthTokenError levée si le AuthDelegate de l’application retourne un jeton vide (en raison de l’annulation)
    - S’applique à la création de :
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - MIP :: NoPolicyError levée si le locataire n’est pas configuré pour les étiquettes
    - S’applique à la création de :
      - mip::FileEngine
      - mip::PolicyEngine
  - MIP :: ServiceDisabledError levée si le service RMS est désactivé pour un utilisateur/appareil/plateforme/client spécifique
    - S’applique à la création de :
      - mip::FileHandler
      - mip::ProtectionHandler
  - MIP :: NoPermissionsError levée si un utilisateur ne dispose pas des droits nécessaires pour déchiffrer un document ou si le contenu a expiré
    - S’applique à la création de :
      - mip::FileHandler
      - mip::ProtectionHandler

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur les plateformes prises en charge et bien plus encore, consultez [FAQ et problèmes du SDK MIP](faqs-known-issues.md) .
- Pour plus d’informations sur la prise en main du kit de développement logiciel MIP [, consultez Installation et configuration du SDK MIP](setup-configure-mip.md) .
