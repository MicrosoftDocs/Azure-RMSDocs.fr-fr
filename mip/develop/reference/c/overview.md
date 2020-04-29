---
title: Référence du kit de développement logiciel MIP pour C
description: Référence du kit de développement logiciel MIP pour C
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 4/16/2020
ms.openlocfilehash: 438cdc93989ffbd5b294adb24175c443aeaf1024
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763869"
---
# <a name="mip-sdk-for-c-reference"></a>Référence du kit de développement logiciel MIP pour C

Le kit de développement logiciel (SDK) Microsoft Information Protection pour C permet aux développeurs de gérer et d’appliquer des stratégies de protection des données à des données et à d’autres ressources numériques.

Le kit de développement logiciel MIP pour C comprend

- [Énumérations](enumerations.md)
- [Structures](structures.md)
- Les fonctions suivantes :

Fonction | Brève description |
|---|---|
| [mip_cc_auth_callback](functions.md#mip_cc_auth_callback) | définition de la fonction de rappel pour l’acquisition du jeton OAuth2 |
| [mip_cc_consent_callback](functions.md#mip_cc_consent_callback) | définition de la fonction de rappel pour le consentement de l’utilisateur à accéder au point de terminaison de service externe |
| [MIP_CC_CreateDictionary](functions.md#mip_cc_createdictionary) | Créer un dictionnaire de clés/valeurs de chaîne |
| [MIP_CC_Dictionary_GetEntries](functions.md#mip_cc_dictionary_getentries) | Obtenir des paires clé/valeur qui composent un dictionnaire |
| [MIP_CC_ReleaseDictionary](functions.md#mip_cc_releasedictionary) | Libérer les ressources associées à un dictionnaire |
| [mip_cc_http_send_callback_fn](functions.md#mip_cc_http_send_callback_fn) | Définition de fonction de rappel pour l’émission d’une requête HTTP |
| [mip_cc_http_cancel_callback_fn](functions.md#mip_cc_http_cancel_callback_fn) | Définition de fonction de rappel pour l’annulation d’une requête HTTP |
| [MIP_CC_CreateHttpDelegate](functions.md#mip_cc_createhttpdelegate) | Crée un délégué HTTP qui peut être utilisé pour remplacer la pile HTTP par défaut du MIP |
| [MIP_CC_NotifyHttpDelegateResponse](functions.md#mip_cc_notifyhttpdelegateresponse) | Avertit un délégué HTTP qu’une réponse HTTP est prête |
| [MIP_CC_ReleaseHttpDelegate](functions.md#mip_cc_releasehttpdelegate) | Libérer les ressources associées à un descripteur délégué HTTP |
| [mip_cc_logger_init_callback_fn](functions.md#mip_cc_logger_init_callback_fn) | Définition de fonction de rappel pour l’initialisation d’un enregistreur d’événements |
| [mip_cc_logger_write_callback_fn](functions.md#mip_cc_logger_write_callback_fn) | Définition de fonction de rappel pour l’écriture d’une instruction de journal |
| [MIP_CC_CreateLoggerDelegate](functions.md#mip_cc_createloggerdelegate) | Crée un délégué d’enregistreur d’événements qui peut être utilisé pour substituer le journal par défaut du MIP. |
| [MIP_CC_ReleaseLoggerDelegate](functions.md#mip_cc_releaseloggerdelegate) | Libérer les ressources associées à un handle de délégué d’enregistreur d’événements |
| [MIP_CC_CreateMipContext](functions.md#mip_cc_createmipcontext) | Créer un contexte MIP pour gérer l’état partagé entre toutes les instances de profil |
| [MIP_CC_CreateMipContextWithCustomFeatureSettings](functions.md#mip_cc_createmipcontextwithcustomfeaturesettings) | Créer un contexte MIP pour gérer l’état partagé entre toutes les instances de profil |
| [MIP_CC_ReleaseMipContext](functions.md#mip_cc_releasemipcontext) | Libérer les ressources associées à un contexte MIP |
| [MIP_CC_ProtectionDescriptor_GetProtectionType](functions.md#mip_cc_protectiondescriptor_getprotectiontype) | Obtient le type de protection, qu’il soit défini ou non par un modèle RMS. |
| [MIP_CC_ProtectionDescriptor_GetOwnerSize](functions.md#mip_cc_protectiondescriptor_getownersize) | Obtient la taille de la mémoire tampon requise pour stocker le propriétaire |
| [MIP_CC_ProtectionDescriptor_GetOwner](functions.md#mip_cc_protectiondescriptor_getowner) | Obtient le propriétaire de la protection |
| [MIP_CC_ProtectionDescriptor_GetNameSize](functions.md#mip_cc_protectiondescriptor_getnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom |
| [MIP_CC_ProtectionDescriptor_GetName](functions.md#mip_cc_protectiondescriptor_getname) | Obtient le nom de la protection |
| [MIP_CC_ProtectionDescriptor_GetDescriptionSize](functions.md#mip_cc_protectiondescriptor_getdescriptionsize) | Obtient la taille de la mémoire tampon requise pour stocker la description |
| [MIP_CC_ProtectionDescriptor_GetDescription](functions.md#mip_cc_protectiondescriptor_getdescription) | Obtient la description de la protection |
| [MIP_CC_ProtectionDescriptor_GetTemplateId](functions.md#mip_cc_protectiondescriptor_gettemplateid) | Obtient l’ID de modèle |
| [MIP_CC_ProtectionDescriptor_GetLabelId](functions.md#mip_cc_protectiondescriptor_getlabelid) | Obtient l’ID d’étiquette |
| [MIP_CC_ProtectionDescriptor_GetContentId](functions.md#mip_cc_protectiondescriptor_getcontentid) | Obtient l’ID de contenu |
| [MIP_CC_ProtectionDescriptor_DoesContentExpire](functions.md#mip_cc_protectiondescriptor_doescontentexpire) | Obtient une valeur indiquant si le contenu a ou non un délai d’expiration. |
| [MIP_CC_ProtectionDescriptor_GetContentValidUntil](functions.md#mip_cc_protectiondescriptor_getcontentvaliduntil) | Obtient le délai d’expiration de la protection (en secondes depuis l’époque) |
| [MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess](functions.md#mip_cc_protectiondescriptor_doesallowofflineaccess) | Obtient une valeur indiquant si l’accès hors connexion est autorisé |
| [MIP_CC_ProtectionDescriptor_GetReferrerSize](functions.md#mip_cc_protectiondescriptor_getreferrersize) | Obtient la taille de la mémoire tampon requise pour stocker le référent |
| [MIP_CC_ProtectionDescriptor_GetReferrer](functions.md#mip_cc_protectiondescriptor_getreferrer) | Obtient le point d’accès de protection |
| [MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize](functions.md#mip_cc_protectiondescriptor_getdoublekeyurlsize) | Obtient la taille de la mémoire tampon requise pour stocker l’URL de la clé double |
| [MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl](functions.md#mip_cc_protectiondescriptor_getdoublekeyurl) | Obtient l’URL de clé double |
| [MIP_CC_ReleaseProtectionDescriptor](functions.md#mip_cc_releaseprotectiondescriptor) | Libérer les ressources associées à un descripteur de protection |
| [MIP_CC_CreateStringList](functions.md#mip_cc_createstringlist) | Créer une liste de chaînes |
| [MIP_CC_StringList_GetStrings](functions.md#mip_cc_stringlist_getstrings) | Obtenir des chaînes qui composent une liste de chaînes |
| [MIP_CC_ReleaseStringList](functions.md#mip_cc_releasestringlist) | Libérer les ressources associées à une liste de chaînes |
| [mip_cc_dispatch_task_callback_fn](functions.md#mip_cc_dispatch_task_callback_fn) | Définition de fonction de rappel pour la distribution d’une tâche asynchrone |
| [mip_cc_cancel_task_callback_fn](functions.md#mip_cc_cancel_task_callback_fn) | Fonction de rappel pour l’annulation d’une tâche en arrière-plan |
| [MIP_CC_CreateTaskDispatcherDelegate](functions.md#mip_cc_createtaskdispatcherdelegate) | Crée un délégué de répartiteur de tâches qui peut être utilisé pour substituer la gestion des tâches Async par défaut du MIP. |
| [MIP_CC_ExecuteDispatchedTask](functions.md#mip_cc_executedispatchedtask) | Avertit un délégué TaskDispatcher qu’une tâche est planifiée pour s’exécuter maintenant sur le thread actuel |
| [MIP_CC_ReleaseTaskDispatcherDelegate](functions.md#mip_cc_releasetaskdispatcherdelegate) | Libérer les ressources associées à un handle de délégué de tâche de répartiteur |
| [MIP_CC_CreateTelemetryConfiguration](functions.md#mip_cc_createtelemetryconfiguration) | Créer un objet de paramètres utilisé pour créer un profil de protection |
| [MIP_CC_TelemetryConfiguration_SetHostName](functions.md#mip_cc_telemetryconfiguration_sethostname) | Définir un nom d’hôte de télémétrie qui remplacera les paramètres de télémétrie internes |
| [MIP_CC_TelemetryConfiguration_SetLibraryName](functions.md#mip_cc_telemetryconfiguration_setlibraryname) | Définir un remplacement de la bibliothèque partagée de télémétrie |
| [MIP_CC_TelemetryConfiguration_SetHttpDelegate](functions.md#mip_cc_telemetryconfiguration_sethttpdelegate) | Remplacer la pile HTTP de télémétrie par défaut par le propriétaire du client |
| [MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate](functions.md#mip_cc_telemetryconfiguration_settaskdispatcherdelegate) | Remplacer le répartiteur de tâches Async par défaut par le propriétaire du client |
| [MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled](functions.md#mip_cc_telemetryconfiguration_setisnetworkdetectionenabled) | Définit si le composant de télémétrie est autorisé à envoyer un ping au statut réseau sur un thread d’arrière-plan. |
| [MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled](functions.md#mip_cc_telemetryconfiguration_setislocalcachingenabled) | Définit si le composant de télémétrie est autorisé ou non à écrire des caches sur le disque |
| [MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled](functions.md#mip_cc_telemetryconfiguration_setistraceloggingenabled) | Définit si le composant de télémétrie est autorisé ou non à écrire des journaux sur le disque |
| [MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut](functions.md#mip_cc_telemetryconfiguration_setistelemetryoptedout) | Définit si une application ou un utilisateur a refusé la télémétrie facultative |
| [MIP_CC_TelemetryConfiguration_SetCustomSettings](functions.md#mip_cc_telemetryconfiguration_setcustomsettings) | Définit les paramètres de télémétrie personnalisés |
| [MIP_CC_TelemetryConfiguration_AddMaskedProperty](functions.md#mip_cc_telemetryconfiguration_addmaskedproperty) | Définit une propriété de télémétrie sur Mask |
| [MIP_CC_ReleaseTelemetryConfiguration](functions.md#mip_cc_releasetelemetryconfiguration) | Libérer les ressources associées à des paramètres de profil de protection |
| [MIP_CC_ReleaseProtectionEngine](functions.md#mip_cc_releaseprotectionengine) | Libérer les ressources associées à un moteur de protection |
| [MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing](functions.md#mip_cc_protectionengine_createprotectionhandlerforpublishing) | Crée un gestionnaire de protection pour la publication d’un nouveau contenu |
| [MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption](functions.md#mip_cc_protectionengine_createprotectionhandlerforconsumption) | Crée un gestionnaire de protection pour la consommation de contenu existant |
| [MIP_CC_ProtectionEngine_GetEngineIdSize](functions.md#mip_cc_protectionengine_getengineidsize) | Obtient la taille de la mémoire tampon requise pour l’ID du moteur |
| [MIP_CC_ProtectionEngine_GetEngineId](functions.md#mip_cc_protectionengine_getengineid) | Obtient l’ID du moteur |
| [MIP_CC_ProtectionEngine_GetTemplatesSize](functions.md#mip_cc_protectionengine_gettemplatessize) | Obtient le nombre de modèles RMS associés à un moteur de protection |
| [MIP_CC_ProtectionEngine_GetTemplates](functions.md#mip_cc_protectionengine_gettemplates) | Obtenir la collection de modèles disponibles pour un utilisateur |
| [MIP_CC_ProtectionEngine_GetRightsForLabelId](functions.md#mip_cc_protectionengine_getrightsforlabelid) | Obtenir la liste des droits octroyés à un utilisateur pour un ID d’étiquette |
| [MIP_CC_ProtectionEngine_GetClientDataSize](functions.md#mip_cc_protectionengine_getclientdatasize) | Obtient la taille des données clientes associées à un moteur de protection |
| [MIP_CC_ProtectionEngine_GetClientData](functions.md#mip_cc_protectionengine_getclientdata) | Obtenir les données client associées à un moteur de protection |
| [MIP_CC_CreateProtectionEngineSettingsWithIdentity](functions.md#mip_cc_createprotectionenginesettingswithidentity) | Créer un objet de paramètres utilisé pour créer un nouveau moteur de protection |
| [MIP_CC_ProtectionEngineSettings_SetClientData](functions.md#mip_cc_protectionenginesettings_setclientdata) | Définit les données du client qui seront stockées de façon opaque à côté de ce moteur et qui sont conservées entre les sessions |
| [MIP_CC_ProtectionEngineSettings_SetCustomSettings](functions.md#mip_cc_protectionenginesettings_setcustomsettings) | Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités. |
| [MIP_CC_ProtectionEngineSettings_SetSessionId](functions.md#mip_cc_protectionenginesettings_setsessionid) | Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie |
| [MIP_CC_ProtectionEngineSettings_SetCloud](functions.md#mip_cc_protectionenginesettings_setcloud) | Définit le Cloud qui affecte les URL de point de terminaison pour toutes les demandes de service |
| [MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl](functions.md#mip_cc_protectionenginesettings_setcloudendpointbaseurl) | Définit l’URL de base pour toutes les demandes de service |
| [MIP_CC_ReleaseProtectionEngineSettings](functions.md#mip_cc_releaseprotectionenginesettings) | Libérer les ressources associées aux paramètres d’un moteur de protection |
| [MIP_CC_CreateProtectionHandlerPublishingSettings](functions.md#mip_cc_createprotectionhandlerpublishingsettings) | Créer un objet de paramètres utilisé pour créer un gestionnaire de protection pour la publication d’un nouveau contenu |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred](functions.md#mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred) | Définit si l’algorithme de chiffrement déconseillé (BCE) est préféré pour la compatibilité descendante |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed](functions.md#mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed) | Définit si les applications prenant en charge non MIP sont autorisées ou non pour ouvrir le contenu protégé |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson](functions.md#mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson) | Définit si PL est au format JSON (la valeur par défaut est XML) |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail](functions.md#mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail) | Définit l’utilisateur délégué |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail](functions.md#mip_cc_protectionhandlerpublishingsettings_setprelicenseuseremail) | Définit l’utilisateur de pré-licence |
| [MIP_CC_CreateProtectionHandlerConsumptionSettings](functions.md#mip_cc_createprotectionhandlerconsumptionsettings) | Créer un objet de paramètres utilisé pour créer un gestionnaire de protection pour la consommation de contenu existant |
| [MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense](functions.md#mip_cc_createprotectionhandlerconsumptionsettingswithprelicense) | Créer un objet de paramètres utilisé pour créer un gestionnaire de protection pour la consommation de contenu existant |
| [MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly](functions.md#mip_cc_protectionhandlerconsumptionsettings_setisofflineonly) | Définit si la création du gestionnaire de protection autorise ou non les opérations HTTP en ligne |
| [MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail](functions.md#mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail) | Définit l’utilisateur délégué |
| [MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize](functions.md#mip_cc_protectionhandler_getserializedpublishinglicensesize) | Obtient la taille de la licence de publication (en octets) |
| [MIP_CC_ProtectionHandler_GetSerializedPublishingLicense](functions.md#mip_cc_protectionhandler_getserializedpublishinglicense) | Obtient la licence de publication |
| [MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize](functions.md#mip_cc_protectionhandler_getserializedprelicensesize) | Obtient la taille de pré-licence (en octets) |
| [MIP_CC_ProtectionHandler_GetSerializedPreLicense](functions.md#mip_cc_protectionhandler_getserializedprelicense) | Obtient la pré-licence |
| [MIP_CC_ProtectionHandler_GetProtectionDescriptor](functions.md#mip_cc_protectionhandler_getprotectiondescriptor) | Obtient le descripteur de protection |
| [MIP_CC_ProtectionHandler_GetRights](functions.md#mip_cc_protectionhandler_getrights) | Obtient la liste des droits accordés à un utilisateur |
| [MIP_CC_ProtectionHandler_GetProtectedContentSize](functions.md#mip_cc_protectionhandler_getprotectedcontentsize) | Calcule la taille du contenu protégé, la factorisation dans le remplissage, etc. |
| [MIP_CC_ProtectionHandler_GetBlockSize](functions.md#mip_cc_protectionhandler_getblocksize) | Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par un gestionnaire de protection |
| [MIP_CC_ProtectionHandler_GetIssuedUserSize](functions.md#mip_cc_protectionhandler_getissuedusersize) | Obtient la taille de la mémoire tampon requise pour stocker l’utilisateur auquel l’accès au contenu protégé a été accordé |
| [MIP_CC_ProtectionHandler_GetIssuedUser](functions.md#mip_cc_protectionhandler_getissueduser) | Obtient l’utilisateur qui a obtenu l’accès au contenu protégé |
| [MIP_CC_ProtectionHandler_GetOwnerSize](functions.md#mip_cc_protectionhandler_getownersize) | Obtient la taille de la mémoire tampon requise pour stocker le propriétaire du contenu protégé |
| [MIP_CC_ProtectionHandler_GetOwner](functions.md#mip_cc_protectionhandler_getowner) | Obtient le propriétaire du contenu protégé |
| [MIP_CC_ProtectionHandler_GetContentId](functions.md#mip_cc_protectionhandler_getcontentid) | Obtient le contenu IE du contenu protégé |
| [MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm](functions.md#mip_cc_protectionhandler_doesusedeprecatedalgorithm) | Détermine si le gestionnaire de protection utilise un algorithme de chiffrement (ECB) déconseillé pour la compatibilité descendante |
| [MIP_CC_ProtectionHandler_DecryptBuffer](functions.md#mip_cc_protectionhandler_decryptbuffer) | Déchiffrer une mémoire tampon |
| [MIP_CC_ReleaseProtectionHandlerPublishingSettings](functions.md#mip_cc_releaseprotectionhandlerpublishingsettings) | Libérer les ressources associées aux paramètres du gestionnaire de protection |
| [MIP_CC_ReleaseProtectionHandlerConsumptionSettings](functions.md#mip_cc_releaseprotectionhandlerconsumptionsettings) | Libérer les ressources associées aux paramètres du gestionnaire de protection |
| [MIP_CC_ReleaseProtectionHandler](functions.md#mip_cc_releaseprotectionhandler) | Libérer les ressources associées à un gestionnaire de protection |
| [MIP_CC_LoadProtectionProfile](functions.md#mip_cc_loadprotectionprofile) | Charger un profil |
| [MIP_CC_ReleaseProtectionProfile](functions.md#mip_cc_releaseprotectionprofile) | Libérer les ressources associées à un profil de protection |
| [MIP_CC_CreateProtectionProfileSettings](functions.md#mip_cc_createprotectionprofilesettings) | Créer un objet de paramètres utilisé pour créer un profil de protection |
| [MIP_CC_ProtectionProfileSettings_SetSessionId](functions.md#mip_cc_protectionprofilesettings_setsessionid) | Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie |
| [MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses](functions.md#mip_cc_protectionprofilesettings_setcancachelicenses) | Configure si les licences d’utilisateur final (LUF) seront mises en cache localement |
| [MIP_CC_ProtectionProfileSettings_SetHttpDelegate](functions.md#mip_cc_protectionprofilesettings_sethttpdelegate) | Remplacer la pile HTTP par défaut par le propriétaire du client |
| [MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate](functions.md#mip_cc_protectionprofilesettings_settaskdispatcherdelegate) | Remplacer le répartiteur de tâches Async par défaut par le propriétaire du client |
| [MIP_CC_ProtectionProfileSettings_SetCustomSettings](functions.md#mip_cc_protectionprofilesettings_setcustomsettings) | Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités. |
| [MIP_CC_ReleaseProtectionProfileSettings](functions.md#mip_cc_releaseprotectionprofilesettings) | Libérer les ressources associées à des paramètres de profil de protection |
| [MIP_CC_TemplateDescriptor_GetId](functions.md#mip_cc_templatedescriptor_getid) | Obtient l’ID de modèle |
| [MIP_CC_TemplateDescriptor_GetNameSize](functions.md#mip_cc_templatedescriptor_getnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom |
| [MIP_CC_TemplateDescriptor_GetName](functions.md#mip_cc_templatedescriptor_getname) | Obtient le nom du modèle |
| [MIP_CC_TemplateDescriptor_GetDescriptionSize](functions.md#mip_cc_templatedescriptor_getdescriptionsize) | Obtient la taille de la mémoire tampon requise pour stocker la description |
| [MIP_CC_TemplateDescriptor_GetDescription](functions.md#mip_cc_templatedescriptor_getdescription) | Obtient la description du modèle |
| [MIP_CC_ReleaseTemplateDescriptor](functions.md#mip_cc_releasetemplatedescriptor) | Libérer les ressources associées à un descripteur de modèle |
| [MIP_CC_Action_GetType](functions.md#mip_cc_action_gettype) | Obtient le type d’une action |
| [MIP_CC_Action_GetId](functions.md#mip_cc_action_getid) | Obtient l’ID d’une action |
| [MIP_CC_ActionResult_GetActions](functions.md#mip_cc_actionresult_getactions) | Obtenir des actions qui composent un résultat d’action |
| [MIP_CC_ReleaseActionResult](functions.md#mip_cc_releaseactionresult) | Libérer les ressources associées à un résultat d’action |
| [MIP_CC_AddContentFooterAction_GetUIElementNameSize](functions.md#mip_cc_addcontentfooteraction_getuielementnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom de l’élément d’interface utilisateur de l’action Ajouter un pied de page de contenu |
| [MIP_CC_AddContentFooterAction_GetUIElementName](functions.md#mip_cc_addcontentfooteraction_getuielementname) | Obtient le nom de l’élément d’interface utilisateur de l’action « Ajouter un pied de page de contenu » |
| [MIP_CC_AddContentFooterAction_GetTextSize](functions.md#mip_cc_addcontentfooteraction_gettextsize) | Obtient la taille de la mémoire tampon requise pour stocker le texte de l’action « Ajouter un pied de page de contenu » |
| [MIP_CC_AddContentFooterAction_GetText](functions.md#mip_cc_addcontentfooteraction_gettext) | Obtient le texte de l’action « Ajouter un pied de page de contenu » |
| [MIP_CC_AddContentFooterAction_GetFontNameSize](functions.md#mip_cc_addcontentfooteraction_getfontnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom de police de l’action « Ajouter un pied de page de contenu » |
| [MIP_CC_AddContentFooterAction_GetFontName](functions.md#mip_cc_addcontentfooteraction_getfontname) | Obtient le nom de police de l’action « Ajouter un pied de page de contenu » |
| [MIP_CC_AddContentFooterAction_GetFontSize](functions.md#mip_cc_addcontentfooteraction_getfontsize) | Obtient la taille de police de l’entier |
| [MIP_CC_AddContentFooterAction_GetFontColorSize](functions.md#mip_cc_addcontentfooteraction_getfontcolorsize) | Obtient la taille de la mémoire tampon requise pour stocker la couleur de police de l’action « Ajouter un pied de page de contenu » |
| [MIP_CC_AddContentFooterAction_GetFontColor](functions.md#mip_cc_addcontentfooteraction_getfontcolor) | Obtient la couleur de police de l’action « Ajouter un pied de page de contenu » (par exemple, « #000000 ») |
| [MIP_CC_AddContentFooterAction_GetAlignment](functions.md#mip_cc_addcontentfooteraction_getalignment) | Obtient l’alignement |
| [MIP_CC_AddContentFooterAction_GetMargin](functions.md#mip_cc_addcontentfooteraction_getmargin) | Obtient la taille de la marge |
| [MIP_CC_AddContentHeaderAction_GetUIElementNameSize](functions.md#mip_cc_addcontentheaderaction_getuielementnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom de l’élément d’interface utilisateur de l’action « Ajouter un en-tête de contenu » |
| [MIP_CC_AddContentHeaderAction_GetUIElementName](functions.md#mip_cc_addcontentheaderaction_getuielementname) | Obtient un nom d’élément d’interface utilisateur de l’action « Ajouter un en-tête de contenu » |
| [MIP_CC_AddContentHeaderAction_GetTextSize](functions.md#mip_cc_addcontentheaderaction_gettextsize) | Obtient la taille de la mémoire tampon requise pour stocker le texte de l’action « Ajouter un en-tête de contenu » |
| [MIP_CC_AddContentHeaderAction_GetText](functions.md#mip_cc_addcontentheaderaction_gettext) | Obtient le texte de l’action « Ajouter un en-tête de contenu » |
| [MIP_CC_AddContentHeaderAction_GetFontNameSize](functions.md#mip_cc_addcontentheaderaction_getfontnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom de police de l’action « Ajouter un en-tête de contenu » |
| [MIP_CC_AddContentHeaderAction_GetFontName](functions.md#mip_cc_addcontentheaderaction_getfontname) | Obtient le nom de police de l’action « Ajouter un en-tête de contenu » |
| [MIP_CC_AddContentHeaderAction_GetFontSize](functions.md#mip_cc_addcontentheaderaction_getfontsize) | Obtient la taille de police de l’entier |
| [MIP_CC_AddContentHeaderAction_GetFontColorSize](functions.md#mip_cc_addcontentheaderaction_getfontcolorsize) | Obtient la taille de la mémoire tampon requise pour stocker la couleur de police de l’action « Ajouter un en-tête de contenu » |
| [MIP_CC_AddContentHeaderAction_GetFontColor](functions.md#mip_cc_addcontentheaderaction_getfontcolor) | Obtient la couleur de police de l’action « Ajouter un en-tête de contenu » (par exemple, « #000000 ») |
| [MIP_CC_AddContentHeaderAction_GetAlignment](functions.md#mip_cc_addcontentheaderaction_getalignment) | Obtient l’alignement |
| [MIP_CC_AddContentHeaderAction_GetMargin](functions.md#mip_cc_addcontentheaderaction_getmargin) | Obtient la taille de la marge |
| [MIP_CC_AddWatermarkAction_GetUIElementNameSize](functions.md#mip_cc_addwatermarkaction_getuielementnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom de l’élément d’interface utilisateur de l’action « Ajouter un filigrane » |
| [MIP_CC_AddWatermarkAction_GetUIElementName](functions.md#mip_cc_addwatermarkaction_getuielementname) | Obtient le nom de l’élément d’interface utilisateur de l’action « Ajouter un filigrane » |
| [MIP_CC_AddWatermarkAction_GetLayout](functions.md#mip_cc_addwatermarkaction_getlayout) | Obtient la disposition du filigrane |
| [MIP_CC_AddWatermarkAction_GetTextSize](functions.md#mip_cc_addwatermarkaction_gettextsize) | Obtient la taille de la mémoire tampon requise pour stocker le texte de l’action « Ajouter un filigrane » |
| [MIP_CC_AddWatermarkAction_GetText](functions.md#mip_cc_addwatermarkaction_gettext) | Obtient le texte de l’action « Ajouter un filigrane » |
| [MIP_CC_AddWatermarkAction_GetFontNameSize](functions.md#mip_cc_addwatermarkaction_getfontnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom de police de l’action « Ajouter un filigrane » |
| [MIP_CC_AddWatermarkAction_GetFontName](functions.md#mip_cc_addwatermarkaction_getfontname) | Obtient le nom de police de l’action « Ajouter un filigrane » |
| [MIP_CC_AddWatermarkAction_GetFontSize](functions.md#mip_cc_addwatermarkaction_getfontsize) | Obtient la taille de police de l’entier |
| [MIP_CC_AddWatermarkAction_GetFontColorSize](functions.md#mip_cc_addwatermarkaction_getfontcolorsize) | Obtient la taille de la mémoire tampon requise pour stocker la couleur de police de l’action « Ajouter un filigrane » |
| [MIP_CC_AddWatermarkAction_GetFontColor](functions.md#mip_cc_addwatermarkaction_getfontcolor) | Obtient la couleur de police de l’action « Ajouter un filigrane » (par exemple, « #000000 ») |
| [MIP_CC_ReleaseContentLabel](functions.md#mip_cc_releasecontentlabel) | Libérer les ressources associées à une étiquette de contenu |
| [MIP_CC_ContentLabel_GetCreationTime](functions.md#mip_cc_contentlabel_getcreationtime) | Obtient l’heure à laquelle l’étiquette a été appliquée |
| [MIP_CC_ContentLabel_GetAssignmentMethod](functions.md#mip_cc_contentlabel_getassignmentmethod) | Obtient la méthode d’assignation d’étiquette |
| [MIP_CC_ContentLabel_GetExtendedProperties](functions.md#mip_cc_contentlabel_getextendedproperties) | Obtient les propriétés étendues |
| [MIP_CC_ContentLabel_IsProtectionAppliedFromLabel](functions.md#mip_cc_contentlabel_isprotectionappliedfromlabel) | Obtient une valeur indiquant si une protection a été appliquée ou non par une étiquette. |
| [MIP_CC_ContentLabel_GetLabel](functions.md#mip_cc_contentlabel_getlabel) | Obtient les propriétés d’étiquette génériques à partir d’une instance de nom de contenu |
| [MIP_CC_CustomAction_GetNameSize](functions.md#mip_cc_customaction_getnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom d’une action « personnalisée » |
| [MIP_CC_CustomAction_GetName](functions.md#mip_cc_customaction_getname) | Obtient un nom d’action « personnalisé » |
| [MIP_CC_CustomAction_GetProperties](functions.md#mip_cc_customaction_getproperties) | Obtient les propriétés d’une action « personnalisée » |
| [mip_cc_metadata_callback](functions.md#mip_cc_metadata_callback) | Définition de la fonction de rappel pour la récupération du document refléter, filtré par nom/préfixe |
| [MIP_CC_ReleaseLabel](functions.md#mip_cc_releaselabel) | Libérer les ressources associées à une étiquette |
| [MIP_CC_Label_GetId](functions.md#mip_cc_label_getid) | Obtient l’ID d’étiquette |
| [MIP_CC_Label_GetNameSize](functions.md#mip_cc_label_getnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom |
| [MIP_CC_Label_GetName](functions.md#mip_cc_label_getname) | Obtient le nom de l’étiquette |
| [MIP_CC_Label_GetDescriptionSize](functions.md#mip_cc_label_getdescriptionsize) | Obtient la taille de la mémoire tampon requise pour stocker la description |
| [MIP_CC_Label_GetDescription](functions.md#mip_cc_label_getdescription) | Obtient la description de l’étiquette |
| [MIP_CC_Label_GetColorSize](functions.md#mip_cc_label_getcolorsize) | Obtient la taille de la mémoire tampon requise pour stocker la couleur |
| [MIP_CC_Label_GetColor](functions.md#mip_cc_label_getcolor) | Obtient la couleur de l’étiquette |
| [MIP_CC_Label_GetSensitivity](functions.md#mip_cc_label_getsensitivity) | Obtient le niveau de sensibilité de l’étiquette. Plus la valeur est élevée, plus la sensibilité est importante. |
| [MIP_CC_Label_GetTooltipSize](functions.md#mip_cc_label_gettooltipsize) | Obtient la taille de la mémoire tampon requise pour stocker l’info-bulle |
| [MIP_CC_Label_GetTooltip](functions.md#mip_cc_label_gettooltip) | Obtient l’info-bulle de l’étiquette |
| [MIP_CC_Label_GetAutoTooltipSize](functions.md#mip_cc_label_getautotooltipsize) | Obtient la taille de la mémoire tampon requise pour stocker l’info-bulle de classification automatique |
| [MIP_CC_Label_GetAutoTooltip](functions.md#mip_cc_label_getautotooltip) | Obtient l’info-bulle de classification automatique des étiquettes |
| [MIP_CC_Label_IsActive](functions.md#mip_cc_label_isactive) | Obtient une valeur indiquant si une étiquette est active ou non |
| [MIP_CC_Label_GetParent](functions.md#mip_cc_label_getparent) | Obtient l’étiquette parente, le cas échéant. |
| [MIP_CC_Label_GetChildrenSize](functions.md#mip_cc_label_getchildrensize) | Obtient le nombre d’étiquettes enfants |
| [MIP_CC_Label_GetChildren](functions.md#mip_cc_label_getchildren) | Obtient les étiquettes enfants |
| [MIP_CC_Label_GetCustomSettings](functions.md#mip_cc_label_getcustomsettings) | Obtient les paramètres personnalisés définis par la stratégie d’une étiquette |
| [MIP_CC_MetadataAction_GetMetadataToRemove](functions.md#mip_cc_metadataaction_getmetadatatoremove) | Obtient les métadonnées de l’action « Metadata » à supprimer |
| [MIP_CC_MetadataAction_GetMetadataToAdd](functions.md#mip_cc_metadataaction_getmetadatatoadd) | Obtient les métadonnées de l’action « Metadata » à ajouter |
| [MIP_CC_CreateMetadataDictionary](functions.md#mip_cc_createmetadatadictionary) | Créer un dictionnaire de clés/valeurs de chaîne |
| [MIP_CC_MetadataDictionary_GetEntries](functions.md#mip_cc_metadatadictionary_getentries) | Obtenir des entrées de métadonnées qui composent un dictionnaire |
| [MIP_CC_ReleaseMetadataDictionary](functions.md#mip_cc_releasemetadatadictionary) | Libérer les ressources associées à un dictionnaire |
| [MIP_CC_ReleasePolicyEngine](functions.md#mip_cc_releasepolicyengine) | Libérer les ressources associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_GetEngineIdSize](functions.md#mip_cc_policyengine_getengineidsize) | Obtient la taille de la mémoire tampon requise pour l’ID du moteur |
| [MIP_CC_PolicyEngine_GetEngineId](functions.md#mip_cc_policyengine_getengineid) | Obtient l’ID du moteur |
| [MIP_CC_PolicyEngine_GetMoreInfoUrlSize](functions.md#mip_cc_policyengine_getmoreinfourlsize) | Obtient la taille des données clientes associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_GetMoreInfoUrl](functions.md#mip_cc_policyengine_getmoreinfourl) | Obtenir des données client associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_IsLabelingRequired](functions.md#mip_cc_policyengine_islabelingrequired) | Obtient une valeur indiquant si la stratégie stipule qu’un document doit être étiqueté. |
| [MIP_CC_PolicyEngine_GetPolicyFileIdSize](functions.md#mip_cc_policyengine_getpolicyfileidsize) | Obtient la taille des données clientes associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_GetPolicyFileId](functions.md#mip_cc_policyengine_getpolicyfileid) | Obtenir des données client associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_GetSensitivityFileIdSize](functions.md#mip_cc_policyengine_getsensitivityfileidsize) | Obtient la taille des données clientes associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_GetSensitivityFileId](functions.md#mip_cc_policyengine_getsensitivityfileid) | Obtenir des données client associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_HasClassificationRules](functions.md#mip_cc_policyengine_hasclassificationrules) | Obtient une valeur indiquant si la stratégie a des règles automatiques ou de recommandation |
| [MIP_CC_PolicyEngine_GetLastPolicyFetchTime](functions.md#mip_cc_policyengine_getlastpolicyfetchtime) | Obtient l’heure de la dernière récupération de la stratégie |
| [MIP_CC_PolicyEngine_GetSensitivityLabelsSize](functions.md#mip_cc_policyengine_getsensitivitylabelssize) | Obtient le nombre d’étiquettes de sensibilité associées au moteur de stratégie |
| [MIP_CC_PolicyEngine_GetSensitivityLabels](functions.md#mip_cc_policyengine_getsensitivitylabels) | Obtient les étiquettes de sensibilité associées au moteur de stratégie |
| [MIP_CC_PolicyEngine_GetLabelById](functions.md#mip_cc_policyengine_getlabelbyid) | Obtient l’étiquette de sensibilité par ID |
| [MIP_CC_PolicyEngine_GetSensitivityTypesSize](functions.md#mip_cc_policyengine_getsensitivitytypessize) | Obtient le nombre de types de sensibilité associés au moteur de stratégie |
| [MIP_CC_PolicyEngine_GetSensitivityTypes](functions.md#mip_cc_policyengine_getsensitivitytypes) | Obtient les types de sensibilité associés au moteur de stratégie |
| [MIP_CC_PolicyEngine_CreatePolicyHandler](functions.md#mip_cc_policyengine_createpolicyhandler) | Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie |
| [MIP_CC_PolicyEngine_SendApplicationAuditEvent](functions.md#mip_cc_policyengine_sendapplicationauditevent) | Enregistre un événement spécifique de l’application dans le pipeline d’audit |
| [MIP_CC_PolicyEngine_GetTenantIdSize](functions.md#mip_cc_policyengine_gettenantidsize) | Obtient la taille de l’ID de locataire |
| [MIP_CC_PolicyEngine_GetTenantId](functions.md#mip_cc_policyengine_gettenantid) | Obtient l’ID de locataire |
| [MIP_CC_PolicyEngine_GetPolicyDataXmlSize](functions.md#mip_cc_policyengine_getpolicydataxmlsize) | Obtient la taille du fichier XML de données de stratégie |
| [MIP_CC_PolicyEngine_GetPolicyDataXml](functions.md#mip_cc_policyengine_getpolicydataxml) | Obtient le XML des données de stratégie |
| [MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize](functions.md#mip_cc_policyengine_getsensitivitytypesdataxmlsize) | Obtient la taille des données XML des types de sensibilité |
| [MIP_CC_PolicyEngine_GetSensitivityTypesDataXml](functions.md#mip_cc_policyengine_getsensitivitytypesdataxml) | Obtient le XML des données des types de sensibilité |
| [MIP_CC_PolicyEngine_GetClientDataSize](functions.md#mip_cc_policyengine_getclientdatasize) | Obtient la taille des données clientes associées à un moteur de stratégie |
| [MIP_CC_PolicyEngine_GetClientData](functions.md#mip_cc_policyengine_getclientdata) | Obtenir des données client associées à un moteur de stratégie |
| [MIP_CC_CreatePolicyEngineSettingsWithIdentity](functions.md#mip_cc_createpolicyenginesettingswithidentity) | Créer un objet de paramètres utilisé pour créer un tout nouveau moteur de stratégie |
| [MIP_CC_PolicyEngineSettings_SetClientData](functions.md#mip_cc_policyenginesettings_setclientdata) | Définit les données du client qui seront stockées de façon opaque à côté de ce moteur et qui sont conservées entre les sessions |
| [MIP_CC_PolicyEngineSettings_SetCustomSettings](functions.md#mip_cc_policyenginesettings_setcustomsettings) | Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités. |
| [MIP_CC_PolicyEngineSettings_SetSessionId](functions.md#mip_cc_policyenginesettings_setsessionid) | Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie |
| [MIP_CC_PolicyEngineSettings_SetCloud](functions.md#mip_cc_policyenginesettings_setcloud) | Définit le Cloud qui affecte les URL de point de terminaison pour toutes les demandes de service |
| [MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl](functions.md#mip_cc_policyenginesettings_setcloudendpointbaseurl) | Définit l’URL de base pour toutes les demandes de service |
| [MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail](functions.md#mip_cc_policyenginesettings_setdelegateduseremail) | Définit l’utilisateur délégué |
| [MIP_CC_PolicyEngineSettings_SetLabelFilter](functions.md#mip_cc_policyenginesettings_setlabelfilter) | Définit le filtre d’étiquette |
| [MIP_CC_ReleasePolicyEngineSettings](functions.md#mip_cc_releasepolicyenginesettings) | Libérer les ressources associées aux paramètres du moteur de stratégie |
| [MIP_CC_ReleasePolicyHandler](functions.md#mip_cc_releasepolicyhandler) | Libérer les ressources associées à un gestionnaire de stratégie |
| [MIP_CC_PolicyHandler_GetSensitivityLabel](functions.md#mip_cc_policyhandler_getsensitivitylabel) | Obtient l’étiquette actuelle d’un document |
| [MIP_CC_PolicyHandler_ComputeActions](functions.md#mip_cc_policyhandler_computeactions) | Exécute les règles de stratégie en fonction de l’état fourni et détermine les actions correspondantes |
| [MIP_CC_PolicyHandler_NotifyCommittedActions](functions.md#mip_cc_policyhandler_notifycommittedactions) | Appelé par l’application après que des actions calculées ont été appliquées et que des données ont été validées sur le disque |
| [MIP_CC_PolicyProfile_AcquireAuthToken](functions.md#mip_cc_policyprofile_acquireauthtoken) | Déclencher un rappel d’authentification |
| [MIP_CC_LoadPolicyProfile](functions.md#mip_cc_loadpolicyprofile) | Charger un profil |
| [MIP_CC_ReleasePolicyProfile](functions.md#mip_cc_releasepolicyprofile) | Libérer les ressources associées à un profil de stratégie |
| [MIP_CC_CreatePolicyProfileSettings](functions.md#mip_cc_createpolicyprofilesettings) | Créer un objet de paramètres utilisé pour créer un profil de stratégie |
| [MIP_CC_PolicyProfileSettings_SetSessionId](functions.md#mip_cc_policyprofilesettings_setsessionid) | Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie |
| [MIP_CC_PolicyProfileSettings_SetHttpDelegate](functions.md#mip_cc_policyprofilesettings_sethttpdelegate) | Remplacer la pile HTTP par défaut par le propriétaire du client |
| [MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate](functions.md#mip_cc_policyprofilesettings_settaskdispatcherdelegate) | Remplacer le répartiteur de tâches Async par défaut par le propriétaire du client |
| [MIP_CC_PolicyProfileSettings_SetCustomSettings](functions.md#mip_cc_policyprofilesettings_setcustomsettings) | Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités. |
| [MIP_CC_ReleasePolicyProfileSettings](functions.md#mip_cc_releasepolicyprofilesettings) | Libérer les ressources associées à des paramètres de profil de stratégie |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize) | Obtient la taille de la mémoire tampon requise pour stocker l’URL de chiffrement à clé double. |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurl) | Obtient l’URL de chiffrement à clé double |
| [MIP_CC_ProtectByTemplateAction_GetTemplateId](functions.md#mip_cc_protectbytemplateaction_gettemplateid) | Obtient un ID de modèle d’action « protéger par le modèle » |
| [MIP_CC_ProtectByTemplateDkAction_GetTemplateId](functions.md#mip_cc_protectbytemplatedkaction_gettemplateid) | Obtient un ID de modèle d’action « protéger par le modèle avec la double clé » |
| [MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurlsize) | Obtient la taille de la mémoire tampon requise pour stocker l’URL de chiffrement à clé double. |
| [MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurl) | Obtient l’URL de chiffrement à clé double |
| [MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize) | Obtient la taille de la mémoire tampon requise pour stocker l’URL de chiffrement à clé double. |
| [MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl) | Obtient l’URL de chiffrement à clé double |
| [MIP_CC_RemoveContentFooterAction_GetUIElementNames](functions.md#mip_cc_removecontentfooteraction_getuielementnames) | Obtient les noms des éléments d’interface utilisateur de l’action supprimer le pied de page de contenu à supprimer |
| [MIP_CC_RemoveContentHeaderAction_GetUIElementNames](functions.md#mip_cc_removecontentheaderaction_getuielementnames) | Obtient les noms des éléments d’interface utilisateur de l’action supprimer l’en-tête de contenu à supprimer |
| [MIP_CC_RemoveWatermarkAction_GetUIElementNames](functions.md#mip_cc_removewatermarkaction_getuielementnames) | Obtient les noms des éléments d’interface utilisateur de l’action « supprimer le filigrane » à supprimer |
| [MIP_CC_ReleaseSensitivityType](functions.md#mip_cc_releasesensitivitytype) | Libérer les ressources associées à un type de sensibilité |
| [MIP_CC_SensitivityType_GetRulePackageIdSize](functions.md#mip_cc_sensitivitytype_getrulepackageidsize) | Obtient la taille de la mémoire tampon requise pour stocker l’ID de package de règles d’un type de sensibilité |
| [MIP_CC_SensitivityType_GetRulePackageId](functions.md#mip_cc_sensitivitytype_getrulepackageid) | Obtient l’ID de package de règle d’un type de sensibilité |
| [MIP_CC_SensitivityType_GetRulePackageSize](functions.md#mip_cc_sensitivitytype_getrulepackagesize) | Obtient la taille de la mémoire tampon requise pour stocker le package de règles d’un type de sensibilité |
| [MIP_CC_SensitivityType_GetRulePackage](functions.md#mip_cc_sensitivitytype_getrulepackage) | Obtient le package de règles d’un type de sensibilité |
