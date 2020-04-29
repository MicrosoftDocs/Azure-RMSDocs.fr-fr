---
title: Historique des versions et politique de support de Microsoft Information Protection (MIP) SDK
description: Historique des versions et notes de modification pour le kit de développement logiciel MIP.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/25/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: bd786925f22774c3e9173a69d88a08618da299fe
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760709"
---
# <a name="microsoft-information-protection-mip-software-development-kit-sdk-version-release-history-and-support-policy"></a>Microsoft Information Protection (MIP) Kit de développement logiciel (SDK), historique des versions et stratégie de support

## <a name="servicing"></a>Maintenance 

Chaque version de disponibilité générale (GA) est prise en charge pendant six mois après la publication de la prochaine version GA. La documentation peut ne pas inclure d’informations sur les versions non prises en charge. Les correctifs et les nouvelles fonctionnalités s’appliquent uniquement à la dernière version GA.

Les versions préliminaires ne doivent pas être déployées en production. Au lieu de cela, utilisez la version préliminaire la plus récente pour tester les nouvelles fonctionnalités ou les correctifs fournis dans la prochaine version GA. Seule la version préliminaire la plus récente est prise en charge.

## <a name="release-history"></a>Historique des mises en production

Utilisez les informations suivantes pour découvrir les nouveautés ou les modifications apportées à une version prise en charge. La dernière version est répertoriée en première position. 

> [!NOTE]
> Les correctifs mineurs ne sont pas répertoriés. par conséquent, si vous rencontrez un problème avec le kit de développement logiciel (SDK), nous vous recommandons de vérifier s’il est corrigé avec la dernière version de la mise à la disposition générale. Si le problème persiste, consultez la préversion actuelle.
>  
> Pour obtenir un support technique, consultez le [forum Stack Overflow Microsoft information protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection). 

## <a name="version-16103"></a>Version 1.6.103

**Date de publication**: 16 avril 2020

### <a name="general-sdk-changes"></a>Modifications générales du SDK

- TLS 1,2 appliqué à toutes les communications HTTP non ADRMS.
- Implémentation HTTP iOS/MacOS migrée à partir de NSURLConnection vers passer.
- Composant de télémétrie iOS migré du kit de développement logiciel (SDK) Aria vers 1DS SDK.
- Le composant de télémétrie utilise désormais le HttpDelegate MIP sur iOS, MacOs et Linux. (Auparavant Win32 uniquement).
- Amélioration de la sécurité des types pour l’API C.
- Déplacement de AuthDelegate depuis le profil vers le moteur en C++, C# et les API Java.
- AuthDelegate déplacé du constructeur de `Profile::Settings` à `Engine::Settings`.
- Catégorie ajoutée à NoPolicyError pour fournir plus d’informations sur la raison de l’échec de la synchronisation de la stratégie.
- Méthode `PolicyEngine::GetTenantId` ajoutée.
- Ajout de la prise en charge explicite du Cloud souverain.
  - Nouvelle `Engine::Settings::SetCloud` méthode pour définir le Cloud cible (GCC High, 21-VIANET, etc.).
  - L' `Engine::Settings::SetCloudEndpointBaseUrl` appel de méthode existant n’est plus nécessaire pour les clouds reconnus.
- Bitcode activé pour les fichiers binaires iOS.

### <a name="file-sdk"></a>SDK de fichiers

- Ajouté `IFileHandler::InspectAsync` aux wrappers C# et Java
- Nouvelle prise en `FileProfile::AcquirePolicyAuthToken` charge via pour déclencher l’acquisition de jetons de stratégie pour permettre à une application de chauffer son cache de jeton.    
- `MsgInspector::GetAttachments`retourne `vector<shared_ptr<MsgAttachmentData>>` à la place de`vector<unique_ptr<MsgAttachmentData>>`
- `TelemetryConfiguration::isOptedOut`le paramètre désactive maintenant complètement la télémétrie. Précédemment, un ensemble de données de télémétrie minimales a été envoyé.

### <a name="policy-sdk"></a>SDK de stratégie

- Nouvelle prise en charge du déclenchement de l’acquisition de jetons pour permettre à une application de chauffer `PolicyProfile::AcquireAuthToken`son cache de jetons via.
- Les étiquettes HYOK sont filtrées par défaut.
- Les métadonnées associées aux étiquettes supprimées seront supprimées.
- En cas de discordance entre une stratégie d’étiquette mise en cache et une stratégie de sensibilité, le cache de stratégie est maintenant effacé.
- Nouvelle prise en charge des métadonnées avec version :
  - Un format de fichier peut être en révision de l’emplacement/du format de ses métadonnées d’étiquette. Dans ce cas, une application doit fournir un MIP avec toutes les métadonnées, et MIP déterminera les métadonnées qui ont la valeur « true ».
  - `ContentLabel::GetExtendedProperties`retourne `vector<MetadataEntry>` à présent à `vector<pair<string, string>>`la place de.
  - `MetadataAction::GetMetadataToAdd`retourne `vector<MetadataEntry>` à présent à `vector<pair<string, string>>`la place de.
  - `ExecutionState::GetContentMetadata`doit maintenant retourner `vector<MetadataEntry>` à la `vector<pair<string, string>>`place de.
  - `ExecutionState::GetContentMetadataVersion`doit retourner la version la plus récente des métadonnées que l’application reconnaît pour le format de fichier actuel (généralement 0).
  - `PolicyEngine::GetWxpMetadataVersion`retourne la version des métadonnées pour les documents Office configurés par l’administrateur de locataire (0 = par défaut, 1 = format compatible avec coauth).
  - Modifications équivalentes dans l’API C :
    - `MIP_CC_ContentLabel_GetExtendedProperties`
    - `MIP_CC_MetadataAction_GetMetadataToAdd`
    - `mip_cc_metadata_callback`
    - `mip_cc_document_state`
    - `MIP_CC_PolicyEngine_GetWxpMetadataVersion`
- `TelemetryConfiguration::isOptedOut`le paramètre désactive maintenant complètement la télémétrie. Précédemment, un ensemble de données de télémétrie minimales a été envoyé. 

### <a name="protection-sdk"></a>SDK protection

- Nouvelle prise en charge de l’inscription et de la révocation pour le suivi des documents.
- Nouvelle prise en charge de la génération d’une pré-licence lors de la publication.
- Le certificat Microsoft SSL public exposé est utilisé par le service de protection.
   - `GetMsftCert` et `GetMsftCertPEM`
   - Si une application remplace l' `HttpDelegate` interface, elle doit faire confiance aux certificats de serveur émis par cette autorité de certification.
   - Cette exigence est attendue en retard dans 2020.    

## <a name="version-15124"></a>Version 1.5.124

**Date de publication**: 2 mars 2020

### <a name="general-sdk-changes"></a>Modifications générales du SDK

- API Java (Windows uniquement)
- Annulation des tâches MIP Async
  - Tous les appels Async retournent l’objet MIP :: AsyncControl avec une méthode Cancel ()
- Binaires dépendants de chargement différé
- Masquer éventuellement des propriétés de télémétrie/d’audit spécifiques
   - Configurable via MIP :: TelemetryConfiguration :: maskedProperties
- Exceptions améliorées :
  - Toutes les erreurs incluent des ID de corrélation actionnable dans la chaîne de description
  - L’erreur réseau contient les champs « Category », « BaseUrl », « RequestId » et « StatusCode »
- Détails de l’erreur/du résultat de l’API C amélioré

### <a name="file-sdk"></a>SDK de fichiers

- Vérifier sans réseau si le fichier est étiqueté ou protégé
  - MIP :: FileHandler :: IsLabeledOrProtected ()
  - Risque mineur de faux positifs (par exemple si le fichier contient des métadonnées d’étiquette Zombie)
- Filtrer les étiquettes associées à des types de protection spécifiques
  - Configurable via MIP :: FileEngine :: Settings :: SetLabelFilter ()
- Exposer les données de stratégie à l’API de fichier
  - MIP :: FileEngine :: GetPolicyDataXml ()

### <a name="policy-sdk"></a>SDK de stratégie

- Marquage du contenu dynamique pour les actions de filigrane/d’en-tête/pied de page :
  - Les champs tels que $ {Item. Label}, $ {Item.Name}, $ {User.Name}, $ {Event. DateTime} seront automatiquement remplis par MIP
  - MIP :: Identity peut être construit avec un champ « Name » convivial utilisé par le marquage de contenu dynamique
  - Configurable via MIP ::P olicyEngine :: Settings :: SetVariableTextMarkingType ()
- Vérifier sans réseau si le contenu est étiqueté
  - MIP ::P olicyHandler :: IsLabeled ()
  - Risque mineur de faux positifs (par exemple, si le contenu contient des métadonnées d’étiquette Zombie)
- Durée de vie du cache de stratégie d’étiquette
  - Par défaut : 30 jours
  - Configurable via MIP ::P olicyProfile :: SetCustomSettings ()
- **Modification avec rupture**
  - Mise à jour de PolicyEngine. Settings. LabelFilter à partir de la liste d’enums vers un champ de type Nullable.

### <a name="protection-sdk"></a>SDK protection

- Pré-licence
  - L’existence d’une pré-licence et du contenu chiffré, ainsi qu’un certificat utilisateur récupéré précédemment, permettent le déchiffrement hors connexion du contenu.
  - MIP ::P rotectionHandler :: ConsumptionSettings peut être construit avec une pré-licence
  - MIP ::P rotectionEngine :: LoadUserCert | Async () récupère le certificat de l’utilisateur qui est stocké conformément au MIP ::P stratégie de mise en cache de rotectionProfile
- Vérification des fonctionnalités propres au serveur
  - Vérifie si le locataire de l’utilisateur prend en charge la fonctionnalité « chiffrer uniquement » (disponible uniquement dans Azure RMS)
  - MIP ::P rotectionEngine :: IsFeatureSupported ()
- Détails plus détaillés lors de la récupération des modèles RMS
- **Modifications avec rupture**
  - `mip::ProtectionEngine::GetTemplates()``vector<shared_ptr<string>>` valeur de retour remplacée `vector<shared_ptr<mip::TemplateDescriptor>>` par (C++)
  - `mip::ProtectionEngine::Observer::OnGetTemplatesSuccess()`paramètre `shared_ptr<vector<string>>` de rappel remplacé `vector<shared_ptr<mip::TemplateDescriptor>>` par (C++)
  - IProtectionEngine. GetTemplates | La valeur `List<string>` de retour Async () `List<TemplateDescriptor>`est remplacée par. (C#)
  - MIP_CC_ProtectionEngine_GetTemplates () mip_cc_guid * param remplacé par mip_cc_template_descriptor * (API C)

### <a name="c-api"></a>API C

- **Modifications avec rupture**: la plupart des fonctions mises à jour pour inclure mip_cc_error paramètre, peuvent être null
  

### <a name="errorexception-updates"></a>Mises à jour des erreurs/exceptions

- Résumé de la gestion des erreurs :
  - AccessDeniedError : l’utilisateur ne dispose pas des droits d’accès au contenu
      - NoAuthTokenError : l’application n’a pas fourni de jeton d’authentification
      - NoPermissionsError : l’utilisateur ne dispose pas de droits sur un contenu spécifique, mais le référent/propriétaire est disponible
      - ServiceDisabledError : le service est désactivé pour l’utilisateur/appareil/plateforme/locataire
  - AdhocProtectionRequiredError : la protection ad hoc doit être définie avant de définir une étiquette
  - BadInputError : entrée non valide de l’utilisateur/de l’application
      - InsufficientBufferError : entrée de mémoire tampon non valide de l’utilisateur/de l’application
      - LabelDisabledError : l’ID d’étiquette est reconnu mais désactivé pour une utilisation
      - LabelNotFoundError : ID d’étiquette non reconnu
      - TemplateNotFoundError : ID de modèle non reconnu
  - ConsentDeniedError : une opération qui nécessite le consentement de l’utilisateur/de l’application n’a pas été accordée
  - DeprecatedApiError : cette API a été dépréciée
  - FileIOError : échec de la lecture/écriture du fichier
  - InternalError : défaillance interne inattendue
  - NetworkError
      - ProxyAuthenticationError : l’authentification du proxy est requise
    - Category = BadResponse : le serveur a retourné une réponse HTTP non lisible (une nouvelle tentative peut être effectuée)
    - Catégorie = annulée : échec de l’établissement de la connexion HTTP, car l’opération a été annulée par l’utilisateur/l’application (une nouvelle tentative réussira probablement)
    - Category = FailureResponseCode : le serveur a retourné une réponse d’échec générique (une nouvelle tentative peut être effectuée)
    - Catégorie = noconnect : échec de l’établissement de la connexion HTTP (une nouvelle tentative peut être effectuée)
    - Catégorie = hors connexion : échec de l’établissement de la connexion HTTP, car l’application est en mode hors connexion (la nouvelle tentative échoue)
    - Catégorie = proxy : échec de l’établissement de la connexion HTTP en raison d’un problème de proxy (la nouvelle tentative échouera probablement)
    - Catégorie = SSL : échec de l’établissement de la connexion HTTP en raison d’un problème SSL (la nouvelle tentative échouera probablement)
    - Category = Throttled : le serveur a retourné une réponse « limitée » (interruption/nouvelle tentative réussie)
    - Catégorie = délai d’expiration : échec de l’établissement de la connexion HTTP Après le délai d’attente (une nouvelle tentative réussira probablement)
    - Category = UnexpectedResponse : le serveur a retourné des données inattendues (la tentative peut être effectuée)
  - NoPolicyError : le locataire ou l’utilisateur n’est pas configuré pour les étiquettes
  - NotSupportedError : opération non prise en charge dans l’état actuel
  - OperationCancelledError : l’opération a été annulée
  - PrivilegedRequiredError : impossible de modifier l’étiquette, sauf si méthode d’assignation = privilégié
- Changements
  - Suppression de PolicySyncError inutilisée. Remplacé par NetworkError
  - Suppression de TransientNetworkError inutilisée. Remplacé par les catégories NetworkError

## <a name="version-140"></a>Version 1.4.0 

**Date de publication**: 6 novembre 2019

Cette version introduit la prise en charge du kit de développement logiciel (SDK) de protection dans le package .NET (Microsoft. InformationProtection. file).

### <a name="sdk-changes"></a>Modifications du kit SDK
- Améliorations des performances et correctifs de bogues
- Énumération StorageType renommée en CacheStorageType
- Liens Android vers libc + + à la place de gnustl
- Suppression des API previouslydeprecated
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

### <a name="file-sdk"></a>SDK de fichiers

- RPMSG
  - Chiffrement
  - Ajout de la prise en charge du déchiffrement String8
- Comportement d’extension PFILE configurable (par défaut <EXT>,. PFILE ou P<EXT>)
  - ProtectionSettings::SetPFileExtensionBehavior

### <a name="policy-sdk"></a>SDK de stratégie

- Terminer l’API C
- Configurer le filtrage des étiquettes associées à la protection
  - PolicyEngine :: paramètres :: SetLabelFilter ()

### <a name="protection-sdk"></a>SDK protection

- Suppression des API previouslydeprecated
  - Suppression de ProtectionEngine :: CreateProtectionHandlerFromDescriptor [Async] (utilisation de ProtectionEngine :: CreateProtectionHandlerForPublishing [Async])
  - Suppression de ProtectionEngine :: CreateProtectionHandlerFromPublishingLicense [Async] (utilisation de ProtectionEngine :: CreateProtectionHandlerForConsumption [Async])
- Exécuter l’API C#
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

- `mip::MipContext`nouvel objet de niveau supérieur.
- Le déchiffrement des fichiers de messages protégés est maintenant pris en charge.
- L’inspection des fichiers message. rpmsg est prise `mip::FileInspector` en `mip::FileHandler::InspectAsync()`charge via et.
- Le cache sur disque peut désormais être éventuellement chiffré.
- Le kit de développement logiciel de protection prend désormais en charge le cloud Souverain.
- Prise en charge d’Arm64 sur Android.
- Prise en charge d’Arm64e sur iOS.
- Le cache des licences utilisateur final peut désormais être désactivé.
- le chiffrement. pfile peut être désactivé via`mip::FileEngine::EnablePFile`
- Amélioration des performances pour les opérations de protection en réduisant le nombre d’appels HTTP
- Suppression des `mip::Identity` détails de l’identité déléguée à partir `DelegatedUserEmail` de `mip::FileEngine::Settings`et `mip::ProtectionSettings`ajoutés `mip::PolicyEngine::Settings`à, `mip::ProtectionHandler`, `PublishingSettings` et `ConsumptionSettings`de et de.
- Les fonctions qui retournaient précédemment ID `mip::Label` retournent désormais un objet.

### <a name="changes"></a>Changements

* Dans les versions précédentes, nous avions requis que `mip::ReleaseAllResources`vous appeliez. La version 1,3 remplace ceci `mip::MipContext::~MipContext` par `mip::MipContext::Shutdown`ou.
* `ActionSource` Supprimée `mip::LabelingOptions` de et`mip::ExecutionState::GetNewLabelActionSource`
* Remplacé `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` par `mip::ProtectionEngine::CreateProtectionHandlerForPublishing`.
* Remplacé `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` par `mip::ProtectionEngine::CreateProtectionHandlerForConsumption`.
* A été `mip::PublishingLicenseContext` renommé `mip::PublishingLicenseInfo` en et mis à jour pour contenir des champs enrichis au lieu d’octets sérialisés bruts.
* `mip::PublishingLicenseInfo`contient les données relatives au MIP après l’analyse d’une licence de publication (PL).
* `mip::TemplateNotFoundError`et `mip::LabelNotFoundError` levée lorsque l’application transmet MIP un ID de modèle ou un ID d’étiquette qui n’est pas reconnu.
* Ajout de la prise en charge de l’accès conditionnel basé sur les `AcquireToken()` étiquettes `mip::AuthDelegate::OAuth2Challenge()`via le paramètre claims de et. Cette fonctionnalité n’a pas encore été exposée par le biais du portail Centre de sécurité et conformité.


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
 - l’exception MIP :: AdhocProtectionRequiredError est levée par FileHandler :: SetLabel pour avertir une application qu’elle doit d’abord appliquer la protection ad hoc avant d’appliquer une étiquette.
 - l’exception MIP :: OperationCancelledError est levée lorsqu’une opération a été annulée (par exemple en raison d’un arrêt ou d’une annulation HTTP).
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
    - MIP :: HttpRequest :: GetBody retourne std :: Vector<uint8_t> au lieu de std :: String
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
 - (interface) MIP :: HttpResponse :: GetBody retourne std :: Vector<uint8_t> au lieu de std :: String
 - (interface) MIP :: HttpResponse l’interface requiert l’implémentation de la méthode’GetId'
 - MIP :: ContentLabel :: GetCreationTime retourne std :: Chrono :: time_point au lieu de std :: String
 - MIP :: FileEngine :: CreateFileHandlerAsync n’accepte plus le paramètre « contentIdentifier »
 - MIP ::P olicyHandler :: NotifyCommitedActions renommé MIP ::P olicyHandler :: NotifyCommittedActions


## <a name="version-110"></a>Version 1.1.0 

**Date de publication**: 15 janvier 2019

Cette version introduit la prise en charge des plateformes suivantes :

  - .NET
  - SDK iOS (SDK de stratégie)
  - Android SDK (SDK de stratégie et kit de développement logiciel de protection)

### <a name="new-features"></a>Nouvelles fonctionnalités

- Support ADRMS
- Les opérations du SDK de protection sont véritablement asynchrones (sur Win32), ce qui permet d’exécuter des opérations de chiffrement/déchiffrement non bloquantes simultanées.
  - Les rappels d’application (AuthDelegate, HTTPDelegate, etc.) peuvent maintenant être appelés sur un thread en arrière-plan
- Les propriétés des légendes personnalisées définies par les administrateurs informatiques peuvent désormais être lues via MIP :: Label :: GetCustomSettings
- La licence de publication sérialisée peut maintenant être récupérée directement à partir d’un fichier sans aucune opération HTTP via MIP :: FileHandler :: GetSerializedPublishingLicense
- Les applications sont notifiées si une opération HTTP est requise pour terminer la création d’un MIP :: FileEngine/MIP ::P olicyEngine via MIP :: FileProfile :: observer :: OnAddPolicyEngineStarting/MIP ::P olicyProfile :: observer :: OnAddEngineStarting
- Détection de la nécessité ou non d’une date d’expiration pour la détection de contenu protégé avec la méthode de commodité MIP ::P rotectionDescriptor ::D oesContentExpire
- Classification :
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
