---
title: Référence du kit de développement logiciel MIP pour C
description: Référence du kit de développement logiciel MIP pour C
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 6269921c14b0ac284aab501253d07bea416ef137
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567353"
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
| [MIP_CC_TemplateDescriptor_GetId](functions.md#mip_cc_templatedescriptor_getid) | Obtient l’ID de modèle |
| [MIP_CC_TemplateDescriptor_GetNameSize](functions.md#mip_cc_templatedescriptor_getnamesize) | Obtient la taille de la mémoire tampon requise pour stocker le nom |
| [MIP_CC_TemplateDescriptor_GetName](functions.md#mip_cc_templatedescriptor_getname) | Obtient le nom du modèle |
| [MIP_CC_TemplateDescriptor_GetDescriptionSize](functions.md#mip_cc_templatedescriptor_getdescriptionsize) | Obtient la taille de la mémoire tampon requise pour stocker la description |
| [MIP_CC_TemplateDescriptor_GetDescription](functions.md#mip_cc_templatedescriptor_getdescription) | Obtient la description du modèle |
| [MIP_CC_ReleaseTemplateDescriptor](functions.md#mip_cc_releasetemplatedescriptor) | Libérer les ressources associées à un descripteur de modèle |
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
| [MIP_CC_ReleasePolicyHandler](functions.md#mip_cc_releasepolicyhandler) | Libérer les ressources associées à un gestionnaire de stratégie |
| [MIP_CC_PolicyHandler_GetSensitivityLabel](functions.md#mip_cc_policyhandler_getsensitivitylabel) | Obtient l’étiquette actuelle d’un document |
| [MIP_CC_PolicyHandler_ComputeActions](functions.md#mip_cc_policyhandler_computeactions) | Exécute les règles de stratégie en fonction de l’état fourni et détermine les actions correspondantes |
| [MIP_CC_PolicyHandler_NotifyCommittedActions](functions.md#mip_cc_policyhandler_notifycommittedactions) | Appelé par l’application après que des actions calculées ont été appliquées et que des données ont été validées sur le disque |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize) | Obtient la taille de la mémoire tampon requise pour stocker l’URL de chiffrement à clé double. |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurl) | Obtient l’URL de chiffrement à clé double |
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
