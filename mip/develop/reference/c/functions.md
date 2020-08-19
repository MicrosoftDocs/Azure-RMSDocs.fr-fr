---
title: Fonctions
description: Fonctions.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 4/16/2020
ms.openlocfilehash: 12aa46260b9c1ed2bac5f1e02c1e358292e86835
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564379"
---
# <a name="functions-c"></a>Fonctions (C)

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

définition de la fonction de rappel pour l’acquisition du jeton OAuth2

**Paramètres**

Paramètre | Description
|---|---|
| identité | Adresse e-mail pour laquelle le jeton sera acquis |
| challenge | Défi OAuth2 |
| contexte | Contexte d’application opaque passé à l’API MIP qui a entraîné ce rappel d’authentification |
| tokenBuffer | Sortie Mémoire tampon dans laquelle le jeton sera copié. Si la valeur est null, 'actualTokenSize’sera rempli, mais |
| tokenBufferSize | Taille (en octets) de la mémoire tampon de sortie |
| actualTokenSize | Sortie Taille réelle (en octets) du jeton |

**Retour**: true si le jeton a été récupéré, sinon false

```c
MIP_CC_CALLBACK(mip_cc_auth_callback,
    bool,
    const mip_cc_identity*,
    const mip_cc_oauth2_challenge*,
    const void*,
    uint8_t*,
    const int64_t,
    int64_t*);
```

## <a name="mip_cc_consent_callback"></a>mip_cc_consent_callback

définition de la fonction de rappel pour le consentement de l’utilisateur à accéder au point de terminaison de service externe

**Paramètres**

Paramètre | Description
|---|---|
| url | URL pour laquelle le kit de développement logiciel (SDK) requiert le consentement de l’utilisateur |

**Retour**: réponse du consentement de l’utilisateur

```c
MIP_CC_CALLBACK(mip_cc_consent_callback,
    mip_cc_consent,
    const char*);
```

## <a name="mip_cc_createdictionary"></a>MIP_CC_CreateDictionary

Créer un dictionnaire de clés/valeurs de chaîne

**Paramètres**

Paramètre | Description
|---|---|
| entries | Tableau de paires clé/valeur |
| count | Nombre de paires clé/valeur |
| dictionnaire | Sortie Dictionnaire nouvellement créé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un mip_cc_dictionary doit être libéré en appelant MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CreateDictionary(
    const mip_cc_kv_pair* entries,
    const int64_t count,
    mip_cc_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_dictionary_getentries"></a>MIP_CC_Dictionary_GetEntries

Obtenir des paires clé/valeur qui composent un dictionnaire

**Paramètres**

Paramètre | Description
|---|---|
| dictionnaire | Dictionnaire source |
| entries | Sortie Tableau de paires clé/valeur, mémoire appartenant à mip_cc_dictionary objet |
| count | Sortie Nombre de paires clé/valeur |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la mémoire pour « entrées » appartient à l’objet mip_cc_dictionary, donc elle ne doit pas être libérée indépendamment 

```c
mip_cc_result MIP_CC_Dictionary_GetEntries(
    const mip_cc_dictionary dictionary,
    mip_cc_kv_pair** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasedictionary"></a>MIP_CC_ReleaseDictionary

Libérer les ressources associées à un dictionnaire

**Paramètres**

Paramètre | Description
|---|---|
| dictionnaire | Dictionnaire à libérer |

```c
void MIP_CC_ReleaseDictionary(mip_cc_dictionary dictionary);
```

## <a name="mip_cc_http_send_callback_fn"></a>mip_cc_http_send_callback_fn

Définition de fonction de rappel pour l’émission d’une requête HTTP

**Paramètres**

Paramètre | Description
|---|---|
| request | Requête HTTP devant être exécutée par l’application |
| contexte | Le même contexte opaque passé à l’appel d’API MIP qui a généré cette requête HTTP |

```c
MIP_CC_CALLBACK(mip_cc_http_send_callback_fn,
    void,
    const mip_cc_http_request*,
    const void*);
```

## <a name="mip_cc_http_cancel_callback_fn"></a>mip_cc_http_cancel_callback_fn

Définition de fonction de rappel pour l’annulation d’une requête HTTP

**Paramètres**

Paramètre | Description
|---|---|
| requestId | ID de la requête HTTP à annuler |

```c
MIP_CC_CALLBACK(mip_cc_http_cancel_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_createhttpdelegate"></a>MIP_CC_CreateHttpDelegate

Crée un délégué HTTP qui peut être utilisé pour remplacer la pile HTTP par défaut du MIP

**Paramètres**

Paramètre | Description
|---|---|
| sendCallback | Pointeur de fonction pour l’émission de requêtes HTTP |
| cancelCallback | Pointeur de fonction pour l’annulation des requêtes HTTP |
| httpDelegate | Sortie Handle vers un objet délégué HTTP |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateHttpDelegate(
    const mip_cc_http_send_callback_fn sendCallback,
    const mip_cc_http_cancel_callback_fn cancelCallback,
    mip_cc_http_delegate* httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_notifyhttpdelegateresponse"></a>MIP_CC_NotifyHttpDelegateResponse

Avertit un délégué HTTP qu’une réponse HTTP est prête

**Paramètres**

Paramètre | Description
|---|---|
| httpDelegate | Handle vers un objet délégué HTTP |
| requestId | ID de la requête HTTP associée à cette opération |
| result | État de réussite ou d’échec de l’opération |
| réponse | Réponse HTTP si l’opération a réussi, sinon nullptr |

**Remarque**: cette fonction doit être appelée par l’application lorsqu’une opération http est terminée. L’ID de la réponse HTTP doit correspondre à l’ID de la requête HTTP pour permettre à MIP de corréler une réponse avec sa demande 

```c
void MIP_CC_NotifyHttpDelegateResponse(
    const mip_cc_http_delegate httpDelegate,
    const char* requestId,
    const mip_cc_http_result result,
    const mip_cc_http_response* response);
```

## <a name="mip_cc_releasehttpdelegate"></a>MIP_CC_ReleaseHttpDelegate

Libérer les ressources associées à un descripteur délégué HTTP

**Paramètres**

Paramètre | Description
|---|---|
| httpDelegate | Délégué HTTP à libérer |

```c
void MIP_CC_ReleaseHttpDelegate(mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_logger_init_callback_fn"></a>mip_cc_logger_init_callback_fn

Définition de fonction de rappel pour l’initialisation d’un enregistreur d’événements

**Paramètres**

Paramètre | Description
|---|---|
| storagePath | Chemin d’accès de fichier où les journaux peuvent être stockés |

```c
MIP_CC_CALLBACK(mip_cc_logger_init_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_logger_write_callback_fn"></a>mip_cc_logger_write_callback_fn

Définition de fonction de rappel pour l’écriture d’une instruction de journal

**Paramètres**

Paramètre | Description
|---|---|
| niveau | niveau de journalisation de l’instruction log. |
| message | message de l’instruction log. |
| function | nom de la fonction pour l’instruction de journal. |
| fichier | nom du fichier dans lequel l’instruction du journal a été générée. |
| line | Numéro de ligne où l’instruction de journalisation a été générée. |

```c
MIP_CC_CALLBACK(mip_cc_logger_write_callback_fn,
    void,
    const mip_cc_log_level,
    const char*,
    const char*,
    const char*,
    const int32_t);
```

## <a name="mip_cc_createloggerdelegate"></a>MIP_CC_CreateLoggerDelegate

Crée un délégué d’enregistreur d’événements qui peut être utilisé pour substituer le journal par défaut du MIP.

**Paramètres**

Paramètre | Description
|---|---|
| initCallback | Pointeur de fonction pour l’initialisation |
| flushCallback | Pointeur de fonction pour vider les journaux |
| writeCallback | Pointeur de fonction pour l’écriture d’une instruction de journal |
| loggerDelegate | Sortie Handle vers un objet de délégué d’enregistreur d’événements |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateLoggerDelegate(
    const mip_cc_logger_init_callback_fn initCallback,
    const mip_cc_logger_flush_callback_fn flushCallback,
    const mip_cc_logger_write_callback_fn writeCallback,
    mip_cc_logger_delegate* loggerDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseloggerdelegate"></a>MIP_CC_ReleaseLoggerDelegate

Libérer les ressources associées à un handle de délégué d’enregistreur d’événements

**Paramètres**

Paramètre | Description
|---|---|
| loggerDelegate | délégué d’enregistreur d’événements à libérer |

```c
void MIP_CC_ReleaseLoggerDelegate(mip_cc_logger_delegate loggerDelegate);
```

## <a name="mip_cc_createmipcontext"></a>MIP_CC_CreateMipContext

Créer un contexte MIP pour gérer l’état partagé entre toutes les instances de profil

**Paramètres**

Paramètre | Description
|---|---|
| applicationInfo | Informations sur l’application qui consomme le kit de développement logiciel (SDK) de protection |
| path | Chemin de fichier sous lequel sont stockées les données de journalisation, de télémétrie et autres supports de protection |
| logLevel | Niveau de journalisation minimal pour. miplog |
| isOfflineOnly | Activer/désactiver les opérations réseau (pas toutes les actions prises en charge hors connexion) |
| loggerDelegateOverride | Facultatif Implémentation de substitution d’enregistreur d’événements |
| telemetryOverride | Facultatif Paramètres de télémétrie remplacés. Si la valeur est NULL, les paramètres par défaut seront utilisés. |
| mipContext | Sortie Instance de contexte MIP nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateMipContext(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmipcontextwithcustomfeaturesettings"></a>MIP_CC_CreateMipContextWithCustomFeatureSettings

Créer un contexte MIP pour gérer l’état partagé entre toutes les instances de profil

**Paramètres**

Paramètre | Description
|---|---|
| applicationInfo | Informations sur l’application qui consomme le kit de développement logiciel (SDK) de protection |
| path | Chemin de fichier sous lequel sont stockées les données de journalisation, de télémétrie et autres supports de protection |
| logLevel | Niveau de journalisation minimal pour. miplog |
| isOfflineOnly | Activer/désactiver les opérations réseau (pas toutes les actions prises en charge hors connexion) |
| loggerDelegateOverride | Facultatif Implémentation de substitution d’enregistreur d’événements |
| telemetryOverride | Facultatif Paramètres de télémétrie remplacés. Si la valeur est NULL, les paramètres par défaut seront utilisés. |
| featureSettings | Facultatif Tableau de substitutions de fonctionnalités personnalisées |
| featureSettingsSize | Taille des substitutions de fonctionnalités personnalisées (dans # of Overrides) |
| mipContext | Sortie Instance de contexte MIP nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateMipContextWithCustomFeatureSettings(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    const mip_cc_feature_override* featureSettings,
    const int64_t featureSettingsSize,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemipcontext"></a>MIP_CC_ReleaseMipContext

Libérer les ressources associées à un contexte MIP

**Paramètres**

Paramètre | Description
|---|---|
| mipContext | Contexte MIP à libérer |

```c
void MIP_CC_ReleaseMipContext(mip_cc_mip_context mipContext);
```

## <a name="mip_cc_protectiondescriptor_getprotectiontype"></a>MIP_CC_ProtectionDescriptor_GetProtectionType

Obtient le type de protection, qu’il soit défini ou non par un modèle RMS.

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| protectionType | Sortie Type de protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetProtectionType(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_protection_type* protectionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getownersize"></a>MIP_CC_ProtectionDescriptor_GetOwnerSize

Obtient la taille de la mémoire tampon requise pour stocker le propriétaire

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| Propriétaires | Sortie Taille de la mémoire tampon pour contenir le propriétaire (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwnerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getowner"></a>MIP_CC_ProtectionDescriptor_GetOwner

Obtient le propriétaire de la protection

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| ownerBuffer | Sortie Mémoire tampon dans laquelle le propriétaire sera copié. |
| ownerBufferSize | Taille (en nombre de caractères) du ownerBuffer. |
| actualOwnerSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si ownerBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualOwnerSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwner(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getnamesize"></a>MIP_CC_ProtectionDescriptor_GetNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| Nom | Sortie Taille de la mémoire tampon pour contenir le nom (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetNameSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getname"></a>MIP_CC_ProtectionDescriptor_GetName

Obtient le nom de la protection

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetName(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescriptionsize"></a>MIP_CC_ProtectionDescriptor_GetDescriptionSize

Obtient la taille de la mémoire tampon requise pour stocker la description

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| Description | Sortie Taille de la mémoire tampon pour contenir la description (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescriptionSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescription"></a>MIP_CC_ProtectionDescriptor_GetDescription

Obtient la description de la protection

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| descriptionBuffer | Sortie Mémoire tampon dans laquelle la description sera copiée. |
| descriptionBufferSize | Taille (en nombre de caractères) du descriptionBuffer. |
| actualDescriptionSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si descriptionBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualDescriptionSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescription(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_gettemplateid"></a>MIP_CC_ProtectionDescriptor_GetTemplateId

Obtient l’ID de modèle

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| templateId | Sortie ID de modèle associé à la protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetTemplateId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getlabelid"></a>MIP_CC_ProtectionDescriptor_GetLabelId

Obtient l’ID d’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| ID | Sortie ID d’étiquette associé à la protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetLabelId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentid"></a>MIP_CC_ProtectionDescriptor_GetContentId

Obtient l’ID de contenu

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| contentId | Sortie ID de contenu associé à la protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doescontentexpire"></a>MIP_CC_ProtectionDescriptor_DoesContentExpire

Obtient une valeur indiquant si le contenu a ou non un délai d’expiration.

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| doesContentExpire | Sortie Indique si le contenu expire ou non |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesContentExpire(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesContentExpire,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentvaliduntil"></a>MIP_CC_ProtectionDescriptor_GetContentValidUntil

Obtient le délai d’expiration de la protection (en secondes depuis l’époque)

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| contentValidUntil | Sortie Délai d’expiration du contenu (en secondes depuis l’époque) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentValidUntil(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* contentValidUntil,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doesallowofflineaccess"></a>MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess

Obtient une valeur indiquant si l’accès hors connexion est autorisé

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| doesAllowOfflineAccess | Sortie Indique si l’accès hors connexion est autorisé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesAllowOfflineAccess,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrersize"></a>MIP_CC_ProtectionDescriptor_GetReferrerSize

Obtient la taille de la mémoire tampon requise pour stocker le référent

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| referrerSize | Sortie Taille de la mémoire tampon pour contenir le référent (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* referrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrer"></a>MIP_CC_ProtectionDescriptor_GetReferrer

Obtient le point d’accès de protection

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| referrerBuffer | Sortie Mémoire tampon dans laquelle le référent sera copié. |
| referrerBufferSize | Taille (en nombre de caractères) du referrerBuffer. |
| actualReferrerSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si referrerBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualReferrerSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrer(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* referrerBuffer,
    const int64_t referrerBufferSize,
    int64_t* actualReferrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurlsize"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize

Obtient la taille de la mémoire tampon requise pour stocker l’URL de la clé double

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| url | Sortie Taille de la mémoire tampon pour stocker l’URL de la clé double (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurl"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl

Obtient l’URL de clé double

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| urlBuffer | Sortie Mémoire tampon dans laquelle l’URL sera copiée. |
| urlBufferSize | Taille (en nombre de caractères) du urlBuffer. |
| actualUrlSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si urlBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualUrlSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectiondescriptor"></a>MIP_CC_ReleaseProtectionDescriptor

Libérer les ressources associées à un descripteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur de protection à libérer |

```c
void MIP_CC_ReleaseProtectionDescriptor(mip_cc_protection_descriptor protectionDescriptor);
```

## <a name="mip_cc_createstringlist"></a>MIP_CC_CreateStringList

Créer une liste de chaînes

**Paramètres**

Paramètre | Description
|---|---|
| chaînes | Tableau de chaînes |
| count | Nombre de chaînes |
| stringList | Sortie Liste de chaînes nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un mip_cc_string_list doit être libéré en appelant MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_CreateStringList(
    const char** strings,
    const int64_t count,
    mip_cc_string_list* stringList,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_stringlist_getstrings"></a>MIP_CC_StringList_GetStrings

Obtenir des chaînes qui composent une liste de chaînes

**Paramètres**

Paramètre | Description
|---|---|
| stringList | Liste des chaînes sources |
| chaînes | Sortie Tableau de chaînes, mémoire appartenant à mip_cc_string_list objet |
| count | Sortie Nombre de chaînes |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la mémoire pour « Strings » appartient à l’objet mip_cc_string_list, donc elle ne doit pas être libérée indépendamment 

```c
mip_cc_result MIP_CC_StringList_GetStrings(
    const mip_cc_string_list stringList,
    const char*** strings,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasestringlist"></a>MIP_CC_ReleaseStringList

Libérer les ressources associées à une liste de chaînes

**Paramètres**

Paramètre | Description
|---|---|
| stringList | Liste de chaînes à libérer |

```c
void MIP_CC_ReleaseStringList(mip_cc_string_list stringList);
```

## <a name="mip_cc_dispatch_task_callback_fn"></a>mip_cc_dispatch_task_callback_fn

Définition de fonction de rappel pour la distribution d’une tâche asynchrone

**Paramètres**

Paramètre | Description
|---|---|
| taskId | Identificateur de tâche unique |

```c
MIP_CC_CALLBACK(mip_cc_dispatch_task_callback_fn,
    void,
    const mip_cc_async_task*);
```

## <a name="mip_cc_cancel_task_callback_fn"></a>mip_cc_cancel_task_callback_fn

Fonction de rappel pour l’annulation d’une tâche en arrière-plan

**Paramètres**

Paramètre | Description
|---|---|
| taskId | Identificateur de tâche unique |

**Retourne**la valeur true si la tâche a été annulée avec succès, sinon false.

```c
MIP_CC_CALLBACK(mip_cc_cancel_task_callback_fn,
    bool,
    const char*);
```

## <a name="mip_cc_createtaskdispatcherdelegate"></a>MIP_CC_CreateTaskDispatcherDelegate

Crée un délégué de répartiteur de tâches qui peut être utilisé pour substituer la gestion des tâches Async par défaut du MIP.

**Paramètres**

Paramètre | Description
|---|---|
| dispatchTaskCallback | Pointeur de fonction pour la distribution de tâches asynchrones |
| cancelTaskCallback | Pointeur de fonction pour l’annulation des tâches en arrière-plan |
| cancelAllTasksCallback | Pointeur de fonction pour l’annulation de toutes les tâches en arrière-plan |
| taskDispatcher | Sortie Handle vers un objet délégué de tâche de répartiteur |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateTaskDispatcherDelegate(
    const mip_cc_dispatch_task_callback_fn dispatchTaskCallback,
    const mip_cc_cancel_task_callback_fn cancelTaskCallback,
    const mip_cc_cancel_all_tasks_callback_fn cancelAllTasksCallback,
    mip_cc_task_dispatcher_delegate* taskDispatcher,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_executedispatchedtask"></a>MIP_CC_ExecuteDispatchedTask

Avertit un délégué TaskDispatcher qu’une tâche est planifiée pour s’exécuter maintenant sur le thread actuel

**Paramètres**

Paramètre | Description
|---|---|
| taskDispatcher | Handle vers un objet délégué de tâche de répartiteur |
| taskId | ID de la tâche asynchrone associée à cette opération |

**Remarque**: cette fonction doit être appelée par l’application lorsqu’une tâche est planifiée pour s’exécuter. Cela entraînera une exécution immédiate de la tâche sur le thread actuel. L’ID doit correspondre à celui d’une tâche précédemment distribuée, non annulée. 

```c
void MIP_CC_ExecuteDispatchedTask(const mip_cc_task_dispatcher_delegate taskDispatcher, const char* taskId);
```

## <a name="mip_cc_releasetaskdispatcherdelegate"></a>MIP_CC_ReleaseTaskDispatcherDelegate

Libérer les ressources associées à un handle de délégué de tâche de répartiteur

**Paramètres**

Paramètre | Description
|---|---|
| taskDispatcher | Délégué de répartiteur de tâches à libérer |

```c
void MIP_CC_ReleaseTaskDispatcherDelegate(mip_cc_task_dispatcher_delegate taskDispatcher);
```

## <a name="mip_cc_createtelemetryconfiguration"></a>MIP_CC_CreateTelemetryConfiguration

Créer un objet de paramètres utilisé pour créer un profil de protection

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Sortie Instance de configuration de télémétrie nouvellement créée contenant les paramètres par défaut |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateTelemetryConfiguration(
    mip_cc_telemetry_configuration* telemetryConfig,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethostname"></a>MIP_CC_TelemetryConfiguration_SetHostName

Définir un nom d’hôte de télémétrie qui remplacera les paramètres de télémétrie internes

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| hostName | Nom de l’hôte |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: cette propriété est définie lorsqu’une application cliente utilise le même composant de télémétrie Aria/1Ds et souhaite utiliser ses paramètres de télémétrie internes (Caching, journalisation, priorité, etc.) à la place des paramètres par défaut du MIP. 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHostName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* hostName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setlibraryname"></a>MIP_CC_TelemetryConfiguration_SetLibraryName

Définir un remplacement de la bibliothèque partagée de télémétrie

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| NomBibliothèque | Nom de la DLL qui implémente l’API C du kit de développement logiciel (SDK) Aria/1DS |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: cette propriété est définie lorsqu’un client dispose d’une dll de télémétrie existante qui implémente l’API C du kit de développement logiciel (SDK) Aria/1Ds qui doit être utilisée à la place de mip_ClientTelemetry.dll 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetLibraryName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* libraryName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethttpdelegate"></a>MIP_CC_TelemetryConfiguration_SetHttpDelegate

Remplacer la pile HTTP de télémétrie par défaut par le propriétaire du client

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| httpDelegate | Instance de rappel HTTP implémentée par l’application cliente |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si cette propriété n’est pas définie, le composant de télémétrie utilise la pile http par défaut du MIP. 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHttpDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_settaskdispatcherdelegate"></a>MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate

Remplacer le répartiteur de tâches Async par défaut par le propriétaire du client

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| taskDispatcherDelegate | Instance de rappel de répartiteur de tâches implémentée par l’application cliente |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setisnetworkdetectionenabled"></a>MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled

Définit si le composant de télémétrie est autorisé à envoyer un ping au statut réseau sur un thread d’arrière-plan.

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| isCachingEnabled | Indique si le composant de télémétrie est autorisé à exécuter un test ping sur l’État réseau sur un thread d’arrière-plan |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la valeur par défaut est « true » 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isNetworkDetectionEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setislocalcachingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled

Définit si le composant de télémétrie est autorisé ou non à écrire des caches sur le disque

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| isCachingEnabled | Indique si le composant de télémétrie est autorisé à écrire des caches sur le disque |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la valeur par défaut est « true » 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isCachingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistraceloggingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled

Définit si le composant de télémétrie est autorisé ou non à écrire des journaux sur le disque

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| isTraceLoggingEnabled | Indique si le composant de télémétrie est autorisé à écrire des journaux sur le disque |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la valeur par défaut est « true » 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTraceLoggingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistelemetryoptedout"></a>MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut

Définit si une application ou un utilisateur a refusé la télémétrie facultative

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| isTelemetryOptedOut | Si une application/un utilisateur a refusé la télémétrie facultative |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la valeur par défaut est « false » 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTelemetryOptedOut,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setcustomsettings"></a>MIP_CC_TelemetryConfiguration_SetCustomSettings

Définit les paramètres de télémétrie personnalisés

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| customSettings | Paramètres de télémétrie personnalisés |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetCustomSettings(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_addmaskedproperty"></a>MIP_CC_TelemetryConfiguration_AddMaskedProperty

Définit une propriété de télémétrie sur Mask

**Paramètres**

Paramètre | Description
|---|---|
| telemetryConfig | Configuration de la télémétrie |
| eventName | Nom d'événement |
| propertyName | Nom de la propriété |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_TelemetryConfiguration_AddMaskedProperty(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* eventName,
    const char* propertyName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetelemetryconfiguration"></a>MIP_CC_ReleaseTelemetryConfiguration

Libérer les ressources associées à des paramètres de profil de protection

**Paramètres**

Paramètre | Description
|---|---|
| profileSettings | Paramètres de profil de protection à libérer |

```c
void MIP_CC_ReleaseTelemetryConfiguration(mip_cc_telemetry_configuration telemetryConfig);
```

## <a name="mip_cc_releaseprotectionengine"></a>MIP_CC_ReleaseProtectionEngine

Libérer les ressources associées à un moteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection à libérer |

```c
void MIP_CC_ReleaseProtectionEngine(mip_cc_protection_engine engine);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforpublishing"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing

Crée un gestionnaire de protection pour la publication d’un nouveau contenu

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur sous lequel un gestionnaire sera créé |
| paramètres | Paramètres du gestionnaire de protection |
| contexte | Contexte client qui sera transmis de manière opaque à HttpDelegate et AuthDelegate |
| gestionnaire | Sortie Instance du gestionnaire de protection nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing(
    const mip_cc_protection_engine engine,
    const mip_cc_protection_handler_publishing_settings settings,
    const void* context,
    mip_cc_protection_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforconsumption"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption

Crée un gestionnaire de protection pour la consommation de contenu existant

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur sous lequel un gestionnaire sera créé |
| paramètres | Paramètres du gestionnaire de protection |
| contexte | Contexte client qui sera transmis de manière opaque à HttpDelegate et AuthDelegate |
| gestionnaire | Sortie Instance du gestionnaire de protection nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption(
  const mip_cc_protection_engine engine,
  const mip_cc_protection_handler_consumption_settings settings,
  const void* context,
  mip_cc_protection_handler* handler,
  mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineidsize"></a>MIP_CC_ProtectionEngine_GetEngineIdSize

Obtient la taille de la mémoire tampon requise pour l’ID du moteur

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection |
| idSize | Sortie Taille de la mémoire tampon de stockage de l’ID de moteur (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineIdSize(
    const mip_cc_protection_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineid"></a>MIP_CC_ProtectionEngine_GetEngineId

Obtient l’ID du moteur

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection |
| idBuffer | Sortie Mémoire tampon dans laquelle l’ID sera copié. |
| idBufferSize | Taille (en nombre de caractères) du idBuffer. |
| actualIdSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si idBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualIdSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineId(
    const mip_cc_protection_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplatessize"></a>MIP_CC_ProtectionEngine_GetTemplatesSize

Obtient le nombre de modèles RMS associés à un moteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection |
| contexte | Contexte client qui sera transmis de manière opaque à HttpDelegate et AuthDelegate |
| templatesSize | Sortie Nombre de modèles |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: cette API peut entraîner une opération http indépendante. Envisagez d’utiliser’MIP_CC_ProtectionEngine_GetTemplates’directement avec une mémoire tampon prédéfinie pour éviter les opérations HTTP supplémentaires inutiles. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplatesSize(
    const mip_cc_protection_engine engine,
    const void* context,
    int64_t* templatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplates"></a>MIP_CC_ProtectionEngine_GetTemplates

Obtenir la collection de modèles disponibles pour un utilisateur

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection |
| contexte | Contexte client qui sera transmis de manière opaque à HttpDelegate et AuthDelegate |
| mip_cc_template_descriptor | [Sortie] mémoire tampon pour créer des gestionnaires de modèles. |
| templateBufferSize | Taille (en nombre d’éléments) du templateBuffer. |
| actualTemplatesSize | Sortie Nombre d’ID de modèle écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si templateBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualTemplateSize est défini sur la taille de mémoire tampon minimale requise. Chaque mip_cc_template_descriptor doit être libérée par l’appelant en appelant MIP_CC_ReleaseTemplateDescriptor (). 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplates(
    const mip_cc_protection_engine engine,
    const void* context,
    mip_cc_template_descriptor* templateDescriptors,
    const int64_t templateBufferSize,
    int64_t* actualTemplatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getrightsforlabelid"></a>MIP_CC_ProtectionEngine_GetRightsForLabelId

Obtenir la liste des droits octroyés à un utilisateur pour un ID d’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection |
| contexte | Contexte client qui sera transmis de manière opaque à HttpDelegate et AuthDelegate |
| documentId | ID de document affecté au document |
| ID | ID d’étiquette appliqué au document |
| ownerEmail | Propriétaire du document |
| delagedUserEmail | E-mail de l’utilisateur si l’utilisateur ou l’application d’authentification agit pour le compte d’un autre utilisateur, vide si aucun |
| droits | Sortie Liste des droits accordés à un utilisateur, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable « Rights » doit être libérée par l’appelant en appelant MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetRightsForLabelId(
    const mip_cc_protection_engine engine,
    const void* context,
    const char* documentId,
    const char* labelId,
    const char* ownerEmail,
    const char* delegatedUserEmail,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdatasize"></a>MIP_CC_ProtectionEngine_GetClientDataSize

Obtient la taille des données clientes associées à un moteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection |
| clientDataSize | Sortie Taille des données du client (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientDataSize(
    const mip_cc_protection_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdata"></a>MIP_CC_ProtectionEngine_GetClientData

Obtenir les données client associées à un moteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de protection |
| clientDataBuffer | Sortie Mémoire tampon dans laquelle les données du client seront copiées |
| clientDataBufferSize | Taille (en nombre de caractères) de clientDataBuffer. |
| actualClientDataSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si clientDataBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualClientDataSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientData(
    const mip_cc_protection_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionenginesettingswithidentity"></a>MIP_CC_CreateProtectionEngineSettingsWithIdentity

Créer un objet de paramètres utilisé pour créer un nouveau moteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| identité | Identité qui sera associée à ProtectionEngine |
| ClientData : | Données client personnalisables stockées avec le moteur |
| locale | Paramètres régionaux dans lesquels les résultats de texte seront générés |
| engineSettings | Sortie Instance de paramètres nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateProtectionEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    mip_cc_protection_engine_settings* engineSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setclientdata"></a>MIP_CC_ProtectionEngineSettings_SetClientData

Définit les données du client qui seront stockées de façon opaque à côté de ce moteur et qui sont conservées entre les sessions

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| ClientData : | Données client |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetClientData(
    const mip_cc_protection_engine_settings engineSettings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcustomsettings"></a>MIP_CC_ProtectionEngineSettings_SetCustomSettings

Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités.

**Paramètres**

Paramètre | Description
|---|---|
| engineSettings | Paramètres du moteur |
| customSettings | Paires clé/valeur de paramètres personnalisés |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCustomSettings(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setsessionid"></a>MIP_CC_ProtectionEngineSettings_SetSessionId

Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| sessionID | ID de session qui représente la durée de vie d’un moteur de protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetSessionId(
    const mip_cc_protection_engine_settings engineSettings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloud"></a>MIP_CC_ProtectionEngineSettings_SetCloud

Définit le Cloud qui affecte les URL de point de terminaison pour toutes les demandes de service

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| cloud | Identificateur de Cloud (valeur par défaut = inconnu) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si le Cloud n’est pas spécifié, il sera déterminé par la recherche DNS du domaine d’identité du moteur si possible, sinon revenez au Cloud global. 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloud(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloudendpointbaseurl"></a>MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl

Définit l’URL de base pour toutes les demandes de service

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| cloudEndpointBaseUrl | URL de base (par exemple, « https://api.aadrm.com ») |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: cette valeur est lue uniquement et doit être définie pour Cloud = MIP_CLOUD_CUSTOM 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_protection_engine_settings engineSettings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionenginesettings"></a>MIP_CC_ReleaseProtectionEngineSettings

Libérer les ressources associées aux paramètres d’un moteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| engineSettings | Paramètres du moteur de protection à libérer |

```c
void MIP_CC_ReleaseProtectionEngineSettings(mip_cc_protection_engine_settings engineSettings);
```

## <a name="mip_cc_createprotectionhandlerpublishingsettings"></a>MIP_CC_CreateProtectionHandlerPublishingSettings

Créer un objet de paramètres utilisé pour créer un gestionnaire de protection pour la publication d’un nouveau contenu

**Paramètres**

Paramètre | Description
|---|---|
| Description | Détails de la protection |
| paramètres | Sortie Instance de paramètres nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateProtectionHandlerPublishingSettings(
    const mip_cc_protection_descriptor descriptor,
    mip_cc_protection_handler_publishing_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred

Définit si l’algorithme de chiffrement déconseillé (BCE) est préféré pour la compatibilité descendante

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection |
| isDeprecatedAlgorithmPreferred | Si l’algorithme déconseillé est préféré |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isDeprecatedAlgorithmPreferred,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed

Définit si les applications prenant en charge non MIP sont autorisées ou non pour ouvrir le contenu protégé

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection |
| isAuditedExtractionAllowed | Si des applications prenant en charge non MIP sont autorisées ou non pour ouvrir du contenu protégé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isAuditedExtractionAllowed,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson

Définit si PL est au format JSON (la valeur par défaut est XML)

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection |
| isPublishingFormatJson | Indique si PL doit être au format JSON |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isPublishingFormatJson,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail

Définit l’utilisateur délégué

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection |
| delegatedUserEmail | Adresse e-mail de l’utilisateur délégué |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setprelicenseuseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail

Définit l’utilisateur de pré-licence

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection |
| preLicenseUserEmail | Adresse e-mail de l’utilisateur de pré-licence |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un utilisateur de pré-licence est spécifié lorsqu’une pré-licence doit être extraite lors de la publication 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* preLicenseUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettings"></a>MIP_CC_CreateProtectionHandlerConsumptionSettings

Créer un objet de paramètres utilisé pour créer un gestionnaire de protection pour la consommation de contenu existant

**Paramètres**

Paramètre | Description
|---|---|
| publishingLicenseBuffer | Mémoire tampon contenant la licence de publication brute |
| publishingLicenseBufferSize | Taille de la mémoire tampon de la licence de publication |
| paramètres | Sortie Instance de paramètres nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettings(
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettingswithprelicense"></a>MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense

Créer un objet de paramètres utilisé pour créer un gestionnaire de protection pour la consommation de contenu existant

**Paramètres**

Paramètre | Description
|---|---|
| preLicenseBuffer | Mémoire tampon contenant la mémoire tampon de pré-licence brute |
| preLicenseBufferSize | Taille de la mémoire tampon de pré-licence |
| publishingLicenseBuffer | Mémoire tampon contenant la licence de publication brute |
| publishingLicenseBufferSize | Taille de la mémoire tampon de la licence de publication |
| paramètres | Sortie Instance de paramètres nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense(
    const uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setisofflineonly"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly

Définit si la création du gestionnaire de protection autorise ou non les opérations HTTP en ligne

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection |
| isOfflineOnly | True si les opérations HTTP sont interdites, sinon false |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si la valeur est true, la création du gestionnaire de protection réussit uniquement si le contenu a déjà été déchiffré précédemment et que sa licence non expirée est mise en cache. Un MIP_RESULT_ERROR_NETWORK résultat est retourné si le contenu mis en cache est introuvable. 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly(
    const mip_cc_protection_handler_consumption_settings settings,
    const bool isOfflineOnly,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail

Définit l’utilisateur délégué

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection |
| delegatedUserEmail | Adresse e-mail de l’utilisateur délégué |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_consumption_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize

Obtient la taille de la licence de publication (en octets)

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| publishingLicenseBufferSize | Sortie Taille de la licence de publication (en octets) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize(
    const mip_cc_protection_handler handler,
    int64_t* publishingLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicense"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicense

Obtient la licence de publication

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| publishingLicenseBuffer | Sortie Mémoire tampon dans laquelle la licence de publication sera écrite |
| publishingLicenseBufferSize | Taille de la mémoire tampon de la licence de publication |
| actualPublishingLicenseSize | Sortie Taille réelle de la licence de publication (en octets) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si publishingLicenseBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualPublishingLicenseSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicense(
    const mip_cc_protection_handler handler,
    uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    int64_t* actualPublishingLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize

Obtient la taille de pré-licence (en octets)

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| format | Format de pré-licence |
| preLicenseBufferSize | Sortie Taille de la pré-licence (en octets) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    int64_t* preLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicense"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicense

Obtient la pré-licence

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| format | Format de pré-licence |
| preLicenseBuffer | Sortie Mémoire tampon dans laquelle la pré-licence sera écrite |
| preLicenseBufferSize | Taille de la mémoire tampon de pré-licence |
| actualPreLicenseSize | Sortie Taille réelle de la pré-licence (en octets) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si preLicenseBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualPreLicenseSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicense(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    int64_t* actualPreLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectiondescriptor"></a>MIP_CC_ProtectionHandler_GetProtectionDescriptor

Obtient le descripteur de protection

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| Description | Sortie Descripteur de protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectionDescriptor(
    const mip_cc_protection_handler handler,
    mip_cc_protection_descriptor* descriptor,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getrights"></a>MIP_CC_ProtectionHandler_GetRights

Obtient la liste des droits accordés à un utilisateur

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| droits | Sortie Liste des droits accordés à un utilisateur, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable « Rights » doit être libérée par l’appelant en appelant MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetRights(
    const mip_cc_protection_handler handler,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectedcontentsize"></a>MIP_CC_ProtectionHandler_GetProtectedContentSize

Calcule la taille du contenu protégé, la factorisation dans le remplissage, etc.

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| unprotectedSize | Taille du contenu non protégé/en texte clair (en octets) |
| includesFinalBlock | Décrit si le contenu non protégé en question comprend ou non le dernier bloc. |
| protectedSize | Sortie Taille du contenu protégé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectedContentSize(
    const mip_cc_protection_handler handler,
    const int64_t unprotectedSize,
    const bool includesFinalBlock,
    int64_t* protectedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getblocksize"></a>MIP_CC_ProtectionHandler_GetBlockSize

Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par un gestionnaire de protection

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| blockSize | Sortie Taille de bloc (en octets) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetBlockSize(
    const mip_cc_protection_handler handler,
    int64_t* blockSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissuedusersize"></a>MIP_CC_ProtectionHandler_GetIssuedUserSize

Obtient la taille de la mémoire tampon requise pour stocker l’utilisateur auquel l’accès au contenu protégé a été accordé

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| issuedUserSize | Sortie Taille de la mémoire tampon pour stocker l’utilisateur émis (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUserSize(
    const mip_cc_protection_handler handler,
    int64_t* issuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissueduser"></a>MIP_CC_ProtectionHandler_GetIssuedUser

Obtient l’utilisateur qui a obtenu l’accès au contenu protégé

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| issuedUserBuffer | Sortie Mémoire tampon dans laquelle l’utilisateur émis sera copié. |
| issuedUserBufferSize | Taille (en nombre de caractères) du issuedUserBuffer. |
| actualIssuedUserSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si issuedUserBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualIssuedUserSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUser(
    const mip_cc_protection_handler handler,
    char* issuedUserBuffer,
    const int64_t issuedUserBufferSize,
    int64_t* actualIssuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getownersize"></a>MIP_CC_ProtectionHandler_GetOwnerSize

Obtient la taille de la mémoire tampon requise pour stocker le propriétaire du contenu protégé

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| Propriétaires | Sortie Taille de la mémoire tampon pour stocker l’utilisateur émis (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwnerSize(
    const mip_cc_protection_handler handler,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getowner"></a>MIP_CC_ProtectionHandler_GetOwner

Obtient le propriétaire du contenu protégé

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| ownerBuffer | Sortie Mémoire tampon dans laquelle l’utilisateur émis sera copié. |
| ownerBufferSize | Taille (en nombre de caractères) du ownerBuffer. |
| actualOwnerSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si ownerBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualOwnerSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwner(
    const mip_cc_protection_handler handler,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getcontentid"></a>MIP_CC_ProtectionHandler_GetContentId

Obtient le contenu IE du contenu protégé

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| contentId | Sortie ID de contenu |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_GetContentId(
    const mip_cc_protection_handler handler,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_doesusedeprecatedalgorithm"></a>MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm

Détermine si le gestionnaire de protection utilise un algorithme de chiffrement (ECB) déconseillé pour la compatibilité descendante

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire représentant le contenu protégé |
| doesUseDeprecatedAlgorithm | Sortie Indique si le gestionnaire de protection utilise un algorithme de chiffrement déconseillé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm(
    const mip_cc_protection_handler handler,
    bool* doesUseDeprecatedAlgorithm,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_decryptbuffer"></a>MIP_CC_ProtectionHandler_DecryptBuffer

Déchiffrer une mémoire tampon

**Paramètres**

Paramètre | Description
|---|---|
| offsetFromStart | Position relative de inputBuffer à partir du début du contenu chiffré |
| inputBuffer | Mémoire tampon du contenu chiffré qui sera déchiffré |
| inputBufferSize | Taille (en octets) de la mémoire tampon d’entrée |
| outputBuffer | Sortie Mémoire tampon dans laquelle le contenu déchiffré sera copié |
| outputBufferSize | Taille (en octets) de la mémoire tampon de sortie |
| isFinal | Si la mémoire tampon d’entrée contient les octets chiffrés finaux ou non |
| actualDecryptedSize | Sortie Taille réelle du contenu chiffré (en octets) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionHandler_DecryptBuffer(
    const mip_cc_protection_handler handler,
    const int64_t offsetFromStart,
    const uint8_t* inputBuffer,
    const int64_t inputBufferSize,
    uint8_t* outputBuffer,
    const int64_t outputBufferSize,
    const bool isFinal,
    int64_t *actualDecryptedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionhandlerpublishingsettings"></a>MIP_CC_ReleaseProtectionHandlerPublishingSettings

Libérer les ressources associées aux paramètres du gestionnaire de protection

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection à libérer |

```c
void MIP_CC_ReleaseProtectionHandlerPublishingSettings(mip_cc_protection_handler_publishing_settings settings);
```

## <a name="mip_cc_releaseprotectionhandlerconsumptionsettings"></a>MIP_CC_ReleaseProtectionHandlerConsumptionSettings

Libérer les ressources associées aux paramètres du gestionnaire de protection

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du gestionnaire de protection à libérer |

```c
void MIP_CC_ReleaseProtectionHandlerConsumptionSettings(mip_cc_protection_handler_consumption_settings settings);
```

## <a name="mip_cc_releaseprotectionhandler"></a>MIP_CC_ReleaseProtectionHandler

Libérer les ressources associées à un gestionnaire de protection

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire de protection à libérer |

```c
void MIP_CC_ReleaseProtectionHandler(mip_cc_protection_handler handler);
```

## <a name="mip_cc_loadprotectionprofile"></a>MIP_CC_LoadProtectionProfile

Charger un profil

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du profil |
| profile | Sortie Instance de profil de protection nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_LoadProtectionProfile(
    const mip_cc_protection_profile_settings settings,
    mip_cc_protection_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofile"></a>MIP_CC_ReleaseProtectionProfile

Libérer les ressources associées à un profil de protection

**Paramètres**

Paramètre | Description
|---|---|
| profile | Profil de protection à libérer |

```c
void MIP_CC_ReleaseProtectionProfile(mip_cc_protection_profile profile);
```

## <a name="mip_cc_createprotectionprofilesettings"></a>MIP_CC_CreateProtectionProfileSettings

Créer un objet de paramètres utilisé pour créer un profil de protection

**Paramètres**

Paramètre | Description
|---|---|
| mipContext | Contexte global partagé entre tous les profils |
| cacheStorageType | Configuration du cache de stockage |
| authCallback | Objet de rappel à utiliser pour l’authentification, implémenté par l’application cliente |
| consentCallback | Objet de rappel à utiliser pour le consentement, implémenté par l’application cliente |
| paramètres | Sortie Instance de paramètres nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreateProtectionProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    const mip_cc_consent_callback consentCallback,
    mip_cc_protection_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setsessionid"></a>MIP_CC_ProtectionProfileSettings_SetSessionId

Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du profil |
| sessionID | ID de session qui représente la durée de vie d’un profil de protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetSessionId(
    const mip_cc_protection_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcancachelicenses"></a>MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses

Configure si les licences d’utilisateur final (LUF) seront mises en cache localement

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du profil |
| canCacheLicenses | Indique si le moteur doit mettre en cache une licence lors de l’ouverture du contenu protégé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses(
    const mip_cc_protection_profile_settings settings,
    const bool canCacheLicenses,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_sethttpdelegate"></a>MIP_CC_ProtectionProfileSettings_SetHttpDelegate

Remplacer la pile HTTP par défaut par le propriétaire du client

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres de profil auxquels le délégué HTTP sera affecté |
| httpDelegate | Instance de rappel HTTP implémentée par l’application cliente |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetHttpDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate

Remplacer le répartiteur de tâches Async par défaut par le propriétaire du client

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres de profil auxquels le délégué de répartiteur de tâches sera affecté |
| taskDispatcherDelegate | Instance de rappel de répartiteur de tâches implémentée par l’application cliente |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcustomsettings"></a>MIP_CC_ProtectionProfileSettings_SetCustomSettings

Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités.

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du profil |
| customSettings | Paires clé/valeur de paramètres personnalisés |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCustomSettings(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofilesettings"></a>MIP_CC_ReleaseProtectionProfileSettings

Libérer les ressources associées à des paramètres de profil de protection

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres de profil de protection à libérer |

```c
void MIP_CC_ReleaseProtectionProfileSettings(mip_cc_protection_profile_settings profilsettingseSettings);
```

## <a name="mip_cc_templatedescriptor_getid"></a>MIP_CC_TemplateDescriptor_GetId

Obtient l’ID de modèle

**Paramètres**

Paramètre | Description
|---|---|
| protectionDescriptor | Descripteur associé au contenu protégé |
| templateId | Sortie ID de modèle associé à la protection |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetId(
    const mip_cc_template_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getnamesize"></a>MIP_CC_TemplateDescriptor_GetNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom

**Paramètres**

Paramètre | Description
|---|---|
| templateDescriptor | Descripteur associé au modèle |
| Nom | Sortie Taille de la mémoire tampon pour contenir le nom (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetNameSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getname"></a>MIP_CC_TemplateDescriptor_GetName

Obtient le nom du modèle

**Paramètres**

Paramètre | Description
|---|---|
| templateDescriptor | Descripteur associé au modèle |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si NameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetName(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescriptionsize"></a>MIP_CC_TemplateDescriptor_GetDescriptionSize

Obtient la taille de la mémoire tampon requise pour stocker la description

**Paramètres**

Paramètre | Description
|---|---|
| templateDescriptor | Descripteur associé au modèle |
| Description | Sortie Taille de la mémoire tampon pour contenir la description (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescriptionSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescription"></a>MIP_CC_TemplateDescriptor_GetDescription

Obtient la description du modèle

**Paramètres**

Paramètre | Description
|---|---|
| templateDescriptor | Descripteur associé au modèle |
| descriptionBuffer | Sortie Mémoire tampon dans laquelle la description sera copiée. |
| descriptionBufferSize | Taille (en nombre de caractères) du descriptionBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si descriptionBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualDescriptionSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescription(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetemplatedescriptor"></a>MIP_CC_ReleaseTemplateDescriptor

Libérer les ressources associées à un descripteur de modèle

**Paramètres**

Paramètre | Description
|---|---|
| templateDescriptor | Descripteur de modèle à libérer |

```c
void MIP_CC_ReleaseTemplateDescriptor(mip_cc_template_descriptor templateDescriptor);
```

## <a name="mip_cc_action_gettype"></a>MIP_CC_Action_GetType

Obtient le type d’une action

**Paramètres**

Paramètre | Description
|---|---|
| action | Action |
| actionType | Sortie Type d’action |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Action_GetType(
    const mip_cc_action action,
    mip_cc_action_type* actionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_action_getid"></a>MIP_CC_Action_GetId

Obtient l’ID d’une action

**Paramètres**

Paramètre | Description
|---|---|
| action | Action |
| id | Sortie ID d’action unique |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Action_GetId(
    const mip_cc_action action,
    mip_cc_guid* id,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_actionresult_getactions"></a>MIP_CC_ActionResult_GetActions

Obtenir des actions qui composent un résultat d’action

**Paramètres**

Paramètre | Description
|---|---|
| actionResult | Résultat de l’action source |
| actions | Sortie Tableau d’actions, mémoire détenu par l’objet mip_cc_action_result |
| count | Sortie Nombre de paires clé/valeur |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la mémoire pour « actions » appartient à l’objet mip_cc_action_result, donc elle ne doit pas être libérée indépendamment 

```c
mip_cc_result MIP_CC_ActionResult_GetActions(
    const mip_cc_action_result actionResult,
    mip_cc_action** actions,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseactionresult"></a>MIP_CC_ReleaseActionResult

Libérer les ressources associées à un résultat d’action

**Paramètres**

Paramètre | Description
|---|---|
| actionResult | Résultat de l’action à libérer |

```c
void MIP_CC_ReleaseActionResult(mip_cc_action_result actionResult);
```

## <a name="mip_cc_addcontentfooteraction_getuielementnamesize"></a>MIP_CC_AddContentFooterAction_GetUIElementNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom de l’élément d’interface utilisateur de l’action Ajouter un pied de page de contenu

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| Nom | Sortie Taille de la mémoire tampon devant contenir le nom de l’élément d’interface utilisateur (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getuielementname"></a>MIP_CC_AddContentFooterAction_GetUIElementName

Obtient le nom de l’élément d’interface utilisateur de l’action « Ajouter un pied de page de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom de l’élément d’interface utilisateur sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettextsize"></a>MIP_CC_AddContentFooterAction_GetTextSize

Obtient la taille de la mémoire tampon requise pour stocker le texte de l’action « Ajouter un pied de page de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| Nom | Sortie Taille de la mémoire tampon pour contenir le texte (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettext"></a>MIP_CC_AddContentFooterAction_GetText

Obtient le texte de l’action « Ajouter un pied de page de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| textBuffer | Sortie Mémoire tampon dans laquelle le texte sera copié. |
| textBufferSize | Taille (en nombre de caractères) du textBuffer. |
| actualTextSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si TextBuffer a la valeur null ou est insuffisant, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualTextSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontnamesize"></a>MIP_CC_AddContentFooterAction_GetFontNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom de police de l’action « Ajouter un pied de page de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| Nom | Sortie Taille de la mémoire tampon pour contenir le nom de la police (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontname"></a>MIP_CC_AddContentFooterAction_GetFontName

Obtient le nom de police de l’action « Ajouter un pied de page de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom de la police sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontsize"></a>MIP_CC_AddContentFooterAction_GetFontSize

Obtient la taille de police de l’entier

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| fontSize | Sortie Taille de police |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolorsize"></a>MIP_CC_AddContentFooterAction_GetFontColorSize

Obtient la taille de la mémoire tampon requise pour stocker la couleur de police de l’action « Ajouter un pied de page de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| Coloriser | Sortie Taille de la mémoire tampon pour contenir la couleur de police (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolor"></a>MIP_CC_AddContentFooterAction_GetFontColor

Obtient la couleur de police de l’action « Ajouter un pied de page de contenu » (par exemple, « #000000 »)

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| colorBuffer | Sortie Mémoire tampon dans laquelle la couleur de police sera copiée. |
| colorBufferSize | Taille (en nombre de caractères) du colorBuffer. |
| actualColorSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si colorBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualColorSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getalignment"></a>MIP_CC_AddContentFooterAction_GetAlignment

Obtient l’alignement

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| alignement | Sortie Repère |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getmargin"></a>MIP_CC_AddContentFooterAction_GetMargin

Obtient la taille de la marge

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un pied de page de contenu » |
| Marges | Sortie Taille de la marge (en mm) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementnamesize"></a>MIP_CC_AddContentHeaderAction_GetUIElementNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom de l’élément d’interface utilisateur de l’action « Ajouter un en-tête de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| Nom | Sortie Taille de la mémoire tampon devant contenir le nom de l’élément d’interface utilisateur (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementname"></a>MIP_CC_AddContentHeaderAction_GetUIElementName

Obtient un nom d’élément d’interface utilisateur de l’action « Ajouter un en-tête de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom de l’élément d’interface utilisateur sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettextsize"></a>MIP_CC_AddContentHeaderAction_GetTextSize

Obtient la taille de la mémoire tampon requise pour stocker le texte de l’action « Ajouter un en-tête de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| Nom | Sortie Taille de la mémoire tampon pour contenir le texte (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettext"></a>MIP_CC_AddContentHeaderAction_GetText

Obtient le texte de l’action « Ajouter un en-tête de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| textBuffer | Sortie Mémoire tampon dans laquelle le texte sera copié. |
| textBufferSize | Taille (en nombre de caractères) du textBuffer. |
| actualTextSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si TextBuffer a la valeur null ou est insuffisant, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualTextSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontnamesize"></a>MIP_CC_AddContentHeaderAction_GetFontNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom de police de l’action « Ajouter un en-tête de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| Nom | Sortie Taille de la mémoire tampon pour contenir le nom de la police (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontname"></a>MIP_CC_AddContentHeaderAction_GetFontName

Obtient le nom de police de l’action « Ajouter un en-tête de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom de la police sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontsize"></a>MIP_CC_AddContentHeaderAction_GetFontSize

Obtient la taille de police de l’entier

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| fontSize | Sortie Taille de police |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolorsize"></a>MIP_CC_AddContentHeaderAction_GetFontColorSize

Obtient la taille de la mémoire tampon requise pour stocker la couleur de police de l’action « Ajouter un en-tête de contenu »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| Coloriser | Sortie Taille de la mémoire tampon pour contenir la couleur de police (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolor"></a>MIP_CC_AddContentHeaderAction_GetFontColor

Obtient la couleur de police de l’action « Ajouter un en-tête de contenu » (par exemple, « #000000 »)

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| colorBuffer | Sortie Mémoire tampon dans laquelle la couleur de police sera copiée. |
| colorBufferSize | Taille (en nombre de caractères) du colorBuffer. |
| actualColorSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si colorBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualColorSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getalignment"></a>MIP_CC_AddContentHeaderAction_GetAlignment

Obtient l’alignement

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| alignement | Sortie Repère |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getmargin"></a>MIP_CC_AddContentHeaderAction_GetMargin

Obtient la taille de la marge

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un en-tête de contenu » |
| Marges | Sortie Taille de la marge (en mm) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementnamesize"></a>MIP_CC_AddWatermarkAction_GetUIElementNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom de l’élément d’interface utilisateur de l’action « Ajouter un filigrane »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| Nom | Sortie Taille de la mémoire tampon devant contenir le nom de l’élément d’interface utilisateur (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementname"></a>MIP_CC_AddWatermarkAction_GetUIElementName

Obtient le nom de l’élément d’interface utilisateur de l’action « Ajouter un filigrane »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom de l’élément d’interface utilisateur sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getlayout"></a>MIP_CC_AddWatermarkAction_GetLayout

Obtient la disposition du filigrane

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| disposition | Sortie Disposition de filigrane |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetLayout(
    const mip_cc_action action,
    mip_cc_watermark_layout* layout,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettextsize"></a>MIP_CC_AddWatermarkAction_GetTextSize

Obtient la taille de la mémoire tampon requise pour stocker le texte de l’action « Ajouter un filigrane »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| textSize | Sortie Taille de la mémoire tampon pour contenir le texte (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettext"></a>MIP_CC_AddWatermarkAction_GetText

Obtient le texte de l’action « Ajouter un filigrane »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| textBuffer | Sortie Mémoire tampon dans laquelle le texte sera copié. |
| textBufferSize | Taille (en nombre de caractères) du textBuffer. |
| actualTextSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si TextBuffer a la valeur null ou est insuffisant, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualTextSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontnamesize"></a>MIP_CC_AddWatermarkAction_GetFontNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom de police de l’action « Ajouter un filigrane »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| Nom | Sortie Taille de la mémoire tampon pour contenir le nom de la police (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontname"></a>MIP_CC_AddWatermarkAction_GetFontName

Obtient le nom de police de l’action « Ajouter un filigrane »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom de la police sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontsize"></a>MIP_CC_AddWatermarkAction_GetFontSize

Obtient la taille de police de l’entier

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| fontSize | Sortie Taille de police |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolorsize"></a>MIP_CC_AddWatermarkAction_GetFontColorSize

Obtient la taille de la mémoire tampon requise pour stocker la couleur de police de l’action « Ajouter un filigrane »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| Coloriser | Sortie Taille de la mémoire tampon pour contenir la couleur de police (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolor"></a>MIP_CC_AddWatermarkAction_GetFontColor

Obtient la couleur de police de l’action « Ajouter un filigrane » (par exemple, « #000000 »)

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Ajouter un filigrane » |
| colorBuffer | Sortie Mémoire tampon dans laquelle la couleur de police sera copiée. |
| colorBufferSize | Taille (en nombre de caractères) du colorBuffer. |
| actualColorSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si colorBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualColorSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasecontentlabel"></a>MIP_CC_ReleaseContentLabel

Libérer les ressources associées à une étiquette de contenu

**Paramètres**

Paramètre | Description
|---|---|
| contentLabel | Étiquette à libérer |

```c
void MIP_CC_ReleaseContentLabel(mip_cc_content_label contentLabel);
```

## <a name="mip_cc_contentlabel_getcreationtime"></a>MIP_CC_ContentLabel_GetCreationTime

Obtient l’heure à laquelle l’étiquette a été appliquée

**Paramètres**

Paramètre | Description
|---|---|
| contentLabel | Etiquette |
| creationTime | Sortie Heure à laquelle l’étiquette a été appliquée au document (en secondes depuis l’époque) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ContentLabel_GetCreationTime(
    const mip_cc_content_label contentLabel,
    int64_t* creationTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getassignmentmethod"></a>MIP_CC_ContentLabel_GetAssignmentMethod

Obtient la méthode d’assignation d’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| contentLabel | Etiquette |
| Assignation | Sortie Méthode d’assignation (par exemple, « standard » ou « Privileged ») |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ContentLabel_GetAssignmentMethod(
    const mip_cc_content_label contentLabel,
    mip_cc_label_assignment_method* assignmentMethod,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getextendedproperties"></a>MIP_CC_ContentLabel_GetExtendedProperties

Obtient les propriétés étendues

**Paramètres**

Paramètre | Description
|---|---|
| contentLabel | Etiquette |
| properties | Sortie Dictionnaire de propriétés étendues, mémoire appartenant à l’appelant |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable « Properties » doit être libérée par l’appelant en appelant MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_ContentLabel_GetExtendedProperties(
    const mip_cc_content_label contentLabel,
    mip_cc_metadata_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_isprotectionappliedfromlabel"></a>MIP_CC_ContentLabel_IsProtectionAppliedFromLabel

Obtient une valeur indiquant si une protection a été appliquée ou non par une étiquette.

**Paramètres**

Paramètre | Description
|---|---|
| contentLabel | Etiquette |
| isProtectionAppliedByLabel | Sortie Si le document est protégé et que la protection a été appliquée explicitement par cette étiquette. |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ContentLabel_IsProtectionAppliedFromLabel(
    const mip_cc_content_label contentLabel,
    bool* isProtectionAppliedByLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getlabel"></a>MIP_CC_ContentLabel_GetLabel

Obtient les propriétés d’étiquette génériques à partir d’une instance de nom de contenu

**Paramètres**

Paramètre | Description
|---|---|
| contentLabel | Étiquette |
| label | Sortie Étiquette générique, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable’étiquette’doit être libérée par l’appelant en appelant MIP_CC_ReleaseLabel 

```c
mip_cc_result MIP_CC_ContentLabel_GetLabel(
    const mip_cc_content_label contentLabel,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getnamesize"></a>MIP_CC_CustomAction_GetNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom d’une action « personnalisée »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « personnalisée » |
| Nom | Sortie Taille de la mémoire tampon pour contenir le nom (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CustomAction_GetNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getname"></a>MIP_CC_CustomAction_GetName

Obtient un nom d’action « personnalisé »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « personnalisée » |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_CustomAction_GetName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getproperties"></a>MIP_CC_CustomAction_GetProperties

Obtient les propriétés d’une action « personnalisée »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « personnalisée » |
| properties | Sortie Dictionnaire de propriétés, mémoire détenu par l’appelant |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable « Properties » doit être libérée par l’appelant en appelant MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CustomAction_GetProperties(
    const mip_cc_action action,
    mip_cc_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadata_callback"></a>mip_cc_metadata_callback

Définition de la fonction de rappel pour la récupération du document refléter, filtré par nom/préfixe

**Paramètres**

Paramètre | Description
|---|---|
| noms | Tableau de noms de clé de métadonnées à inclure dans le résultat |
| namesSize | Nombre de valeurs dans le tableau’Names' |
| namePrefixes | Tableau de préfixes de nom de clé de métadonnées à inclure dans le résultat |
| namePrefixesSize | Nombre de valeurs dans le tableau « namesPrefixes » |
| contexte | Contexte d’application passé de manière opaque de l’appel d’API au rappel |
| metadata | Sortie Dictionnaire de clés/valeurs de métadonnées, créé par l’application cliente. Ce dictionnaire sera publié par MIP. |

```c
MIP_CC_CALLBACK(mip_cc_metadata_callback,
    void,
    const char**,
    const int64_t,
    const char**,
    const int64_t,
    const void*,
    mip_cc_metadata_dictionary*);
```

## <a name="mip_cc_releaselabel"></a>MIP_CC_ReleaseLabel

Libérer les ressources associées à une étiquette

**Paramètres**

Paramètre | Description
|---|---|
| label | Étiquette à libérer |

```c
void MIP_CC_ReleaseLabel(mip_cc_label label);
```

## <a name="mip_cc_label_getid"></a>MIP_CC_Label_GetId

Obtient l’ID d’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| ID | Sortie ID d’étiquette |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetId(
    const mip_cc_label label,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getnamesize"></a>MIP_CC_Label_GetNameSize

Obtient la taille de la mémoire tampon requise pour stocker le nom

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| Nom | Sortie Taille de la mémoire tampon pour contenir le nom (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetNameSize(
    const mip_cc_label label,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getname"></a>MIP_CC_Label_GetName

Obtient le nom de l’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| nameBuffer | Sortie Mémoire tampon dans laquelle le nom sera copié. |
| nameBufferSize | Taille (en nombre de caractères) du nameBuffer. |
| actualNameSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si nameBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualNameSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_Label_GetName(
    const mip_cc_label label,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescriptionsize"></a>MIP_CC_Label_GetDescriptionSize

Obtient la taille de la mémoire tampon requise pour stocker la description

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| Description | Sortie Taille de la mémoire tampon pour contenir la description (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetDescriptionSize(
    const mip_cc_label label,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescription"></a>MIP_CC_Label_GetDescription

Obtient la description de l’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| descriptionBuffer | Sortie Mémoire tampon dans laquelle la description sera copiée. |
| descriptionBufferSize | Taille (en nombre de caractères) du descriptionBuffer. |
| actualDescriptionSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si descriptionBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualDescriptionSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_Label_GetDescription(
    const mip_cc_label label,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolorsize"></a>MIP_CC_Label_GetColorSize

Obtient la taille de la mémoire tampon requise pour stocker la couleur

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| Coloriser | Sortie Taille de la mémoire tampon de stockage (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetColorSize(
    const mip_cc_label label,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolor"></a>MIP_CC_Label_GetColor

Obtient la couleur de l’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| colorBuffer | Sortie Mémoire tampon dans laquelle la couleur sera copiée (au format #RRGGBB). |
| colorBufferSize | Taille (en nombre de caractères) du colorBuffer. |
| actualColorSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si colorBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualColorSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_Label_GetColor(
    const mip_cc_label label,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getsensitivity"></a>MIP_CC_Label_GetSensitivity

Obtient le niveau de sensibilité de l’étiquette. Plus la valeur est élevée, plus la sensibilité est importante.

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| sensitivity | Sortie Niveau de sensibilité |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetSensitivity(
    const mip_cc_label label,
    int32_t* sensitivity,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltipsize"></a>MIP_CC_Label_GetTooltipSize

Obtient la taille de la mémoire tampon requise pour stocker l’info-bulle

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| tooltipSize | Sortie Taille de la mémoire tampon pour contenir l’info-bulle (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltip"></a>MIP_CC_Label_GetTooltip

Obtient l’info-bulle de l’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| tooltipBuffer | Sortie Mémoire tampon dans laquelle l’info-bulle sera copiée. |
| tooltipBufferSize | Taille (en nombre de caractères) du tooltipBuffer. |
| actualTooltipSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si tooltipBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualTooltipSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_Label_GetTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltipsize"></a>MIP_CC_Label_GetAutoTooltipSize

Obtient la taille de la mémoire tampon requise pour stocker l’info-bulle de classification automatique

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| tooltipSize | Sortie Taille de la mémoire tampon pour contenir l’info-bulle (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetAutoTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltip"></a>MIP_CC_Label_GetAutoTooltip

Obtient l’info-bulle de classification automatique des étiquettes

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| tooltipBuffer | Sortie Mémoire tampon dans laquelle l’info-bulle sera copiée. |
| tooltipBufferSize | Taille (en nombre de caractères) du tooltipBuffer. |
| actualTooltipSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si tooltipBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualTooltipSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_Label_GetAutoTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_isactive"></a>MIP_CC_Label_IsActive

Obtient une valeur indiquant si une étiquette est active ou non

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| isActive | Sortie Indique si une étiquette est considérée comme active. |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: seules les étiquettes actives peuvent être appliquées. Les étiquettes Inactivte ne peuvent pas être appliquées et sont utilisées uniquement à des fins d’affichage. 

```c
mip_cc_result MIP_CC_Label_IsActive(
    const mip_cc_label label,
    bool* isActive,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getparent"></a>MIP_CC_Label_GetParent

Obtient l’étiquette parente, le cas échéant.

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| parent | Sortie Étiquette parente, le cas échéant, sinon null |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetParent(
    const mip_cc_label label,
    mip_cc_label* parent,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildrensize"></a>MIP_CC_Label_GetChildrenSize

Obtient le nombre d’étiquettes enfants

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| childrenSize | Sortie Nombre d’enfants |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_Label_GetChildrenSize(
    const mip_cc_label label,
    int64_t* childrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildren"></a>MIP_CC_Label_GetChildren

Obtient les étiquettes enfants

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| childrenBuffer | Sortie Mémoire tampon les étiquettes enfants seront copiées dans. Étiquettes des enfants |
| childrenBufferSize | Taille (en nombre d’étiquettes) du childrenBuffer. |
| actualChildrenSize | Sortie Nombre d’étiquettes enfants écrites dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si childrenBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualChildrenSize est défini sur la taille de mémoire tampon minimale requise 

```c
mip_cc_result MIP_CC_Label_GetChildren(
    const mip_cc_label label,
    mip_cc_label* childrenBuffer,
    const int64_t childrenBufferSize,
    int64_t* actualChildrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcustomsettings"></a>MIP_CC_Label_GetCustomSettings

Obtient les paramètres personnalisés définis par la stratégie d’une étiquette

**Paramètres**

Paramètre | Description
|---|---|
| label | Etiquette |
| paramètres | Sortie Dictionnaire de paramètres, appartenant à l’appelant |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable « Settings » doit être libérée par l’appelant en appelant MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_Label_GetCustomSettings(
    const mip_cc_label label,
    mip_cc_dictionary* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoremove"></a>MIP_CC_MetadataAction_GetMetadataToRemove

Obtient les métadonnées de l’action « Metadata » à supprimer

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Metadata » |
| metadataNames | Sortie Noms de clés des métadonnées à supprimer, mémoire détenue par l’appelant |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable’metadataNames’doit être libérée par l’appelant en appelant MIP_CC_ReleaseStringList la @note suppression des métadonnées doit être effectuée avant l’ajout de métadonnées 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToRemove(
    const mip_cc_action action,
    mip_cc_string_list* metadataNames,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoadd"></a>MIP_CC_MetadataAction_GetMetadataToAdd

Obtient les métadonnées de l’action « Metadata » à ajouter

**Paramètres**

Paramètre | Description
|---|---|
| action | action « Metadata » |
| metadata | [Sortie] liste des entrées de métadonnées à ajouter, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable « Metadata » doit être libérée par l’appelant en appelant MIP_CC_ReleaseDictionary la @note suppression des métadonnées doit être effectuée avant l’ajout de métadonnées 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToAdd(
    const mip_cc_action action,
    mip_cc_metadata_dictionary* metadata,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmetadatadictionary"></a>MIP_CC_CreateMetadataDictionary

Créer un dictionnaire de clés/valeurs de chaîne

**Paramètres**

Paramètre | Description
|---|---|
| entries | Tableau d’entrées de métadonnées |
| count | Nombre d’entrées de métadonnées |
| dictionnaire | Sortie Dictionnaire nouvellement créé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un mip_cc_dictionary doit être libéré en appelant MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CreateMetadataDictionary(
    const mip_cc_metadata_entry* entries,
    const int64_t count,
    mip_cc_metadata_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadatadictionary_getentries"></a>MIP_CC_MetadataDictionary_GetEntries

Obtenir des entrées de métadonnées qui composent un dictionnaire

**Paramètres**

Paramètre | Description
|---|---|
| dictionnaire | Dictionnaire source |
| entries | Sortie Tableau d’entrées de métadonnées, mémoire appartenant à mip_cc_dictionary objet |
| count | Sortie Nombre d’entrées de métadonnées |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la mémoire pour « entrées » appartient à l’objet mip_cc_dictionary, donc elle ne doit pas être libérée indépendamment 

```c
mip_cc_result MIP_CC_MetadataDictionary_GetEntries(
    const mip_cc_metadata_dictionary dictionary,
    mip_cc_metadata_entry** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemetadatadictionary"></a>MIP_CC_ReleaseMetadataDictionary

Libérer les ressources associées à un dictionnaire

**Paramètres**

Paramètre | Description
|---|---|
| dictionnaire | Dictionnaire à libérer |

```c
void MIP_CC_ReleaseMetadataDictionary(mip_cc_metadata_dictionary dictionary);
```

## <a name="mip_cc_releasepolicyengine"></a>MIP_CC_ReleasePolicyEngine

Libérer les ressources associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie à libérer |

```c
void MIP_CC_ReleasePolicyEngine(mip_cc_policy_engine engine);
```

## <a name="mip_cc_policyengine_getengineidsize"></a>MIP_CC_PolicyEngine_GetEngineIdSize

Obtient la taille de la mémoire tampon requise pour l’ID du moteur

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| idSize | Sortie Taille de la mémoire tampon de stockage de l’ID de moteur (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineIdSize(
    const mip_cc_policy_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getengineid"></a>MIP_CC_PolicyEngine_GetEngineId

Obtient l’ID du moteur

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| idBuffer | Sortie Mémoire tampon dans laquelle l’ID sera copié. |
| idBufferSize | Taille (en nombre de caractères) du idBuffer. |
| actualIdSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si idBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualIdSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineId(
    const mip_cc_policy_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourlsize"></a>MIP_CC_PolicyEngine_GetMoreInfoUrlSize

Obtient la taille des données clientes associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| moreInfoUrlSize | Sortie Taille des données du client (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrlSize(
    const mip_cc_policy_engine engine,
    int64_t* moreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourl"></a>MIP_CC_PolicyEngine_GetMoreInfoUrl

Obtenir des données client associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| moreInfoUrlBuffer | Sortie Mémoire tampon dans laquelle les données du client seront copiées |
| moreInfoUrlBufferSize | Taille (en nombre de caractères) de moreInfoUrlBuffer. |
| actualMoreInfoUrlSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si moreInfoUrlBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualMoreInfoUrlSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrl(
    const mip_cc_policy_engine engine,
    char* moreInfoUrlBuffer,
    const int64_t moreInfoUrlBufferSize,
    int64_t* actualMoreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_islabelingrequired"></a>MIP_CC_PolicyEngine_IsLabelingRequired

Obtient une valeur indiquant si la stratégie stipule qu’un document doit être étiqueté.

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| isLabelingRequired | Sortie Indique si la stratégie stipule qu’un document doit être étiqueté |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_IsLabelingRequired(
    const mip_cc_policy_engine engine,
    bool* isLabelingRequired,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileidsize"></a>MIP_CC_PolicyEngine_GetPolicyFileIdSize

Obtient la taille des données clientes associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| policyFileIdSize | Sortie Taille des données du client (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* policyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileid"></a>MIP_CC_PolicyEngine_GetPolicyFileId

Obtenir des données client associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| policyFileIdBuffer | Sortie Mémoire tampon dans laquelle les données du client seront copiées |
| policyFileIdBufferSize | Taille (en nombre de caractères) de policyFileIdBuffer. |
| actualPolicyFileIdSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si policyFileIdBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualPolicyFileIdSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileId(
    const mip_cc_policy_engine engine,
    char* policyFileIdBuffer,
    const int64_t policyFileIdBufferSize,
    int64_t* actualPolicyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileidsize"></a>MIP_CC_PolicyEngine_GetSensitivityFileIdSize

Obtient la taille des données clientes associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| sensitivityFileIdSize | Sortie Taille des données du client (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileid"></a>MIP_CC_PolicyEngine_GetSensitivityFileId

Obtenir des données client associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| sensitivityFileIdBuffer | Sortie Mémoire tampon dans laquelle les données du client seront copiées |
| sensitivityFileIdBufferSize | Taille (en nombre de caractères) de sensitivityFileIdBuffer. |
| actualSensitivityFileIdSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si sensitivityFileIdBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualSensitivityFileIdSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileId(
    const mip_cc_policy_engine engine,
    char* sensitivityFileIdBuffer,
    const int64_t sensitivityFileIdBufferSize,
    int64_t* actualSensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_hasclassificationrules"></a>MIP_CC_PolicyEngine_HasClassificationRules

Obtient une valeur indiquant si la stratégie a des règles automatiques ou de recommandation

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| hasClassificationRules | Sortie Indique si la stratégie a des règles automatiques ou de recommandation |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_HasClassificationRules(
    const mip_cc_policy_engine engine,
    bool* hasClassificationRules,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlastpolicyfetchtime"></a>MIP_CC_PolicyEngine_GetLastPolicyFetchTime

Obtient l’heure de la dernière récupération de la stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| lastPolicyFetchTime | Sortie Heure de la dernière extraction de la stratégie (en secondes depuis l’époque) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetLastPolicyFetchTime(
    const mip_cc_policy_engine engine,
    int64_t* lastPolicyFetchTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabelssize"></a>MIP_CC_PolicyEngine_GetSensitivityLabelsSize

Obtient le nombre d’étiquettes de sensibilité associées au moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| labelsSize | Sortie Nombre d’étiquettes |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabelsSize(
    const mip_cc_policy_engine engine,
    int64_t* labelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabels"></a>MIP_CC_PolicyEngine_GetSensitivityLabels

Obtient les étiquettes de sensibilité associées au moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| labelBuffer | Sortie Mémoire tampon dans laquelle les étiquettes seront copiées. Les étiquettes sont détenues par le client |
| labelBufferSize | Taille (en nombre d’étiquettes) du labelBuffer. |
| actualLabelsSize | Sortie Nombre d’étiquettes écrites dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si labelBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualLabelsSize est défini sur la taille de mémoire tampon minimale requise 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabels(
    const mip_cc_policy_engine engine,
    mip_cc_label* labelBuffer,
    const int64_t labelBufferSize,
    int64_t* actualLabelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlabelbyid"></a>MIP_CC_PolicyEngine_GetLabelById

Obtient l’étiquette de sensibilité par ID

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| ID | ID d’étiquette |
| label | Sortie Étiquette de sensibilité. Cette valeur est la propriété de l’appelant et doit être libérée avec MIP_CC_ReleaseLabel. |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetLabelById(
    const mip_cc_policy_engine engine,
    const char* labelId,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypessize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesSize

Obtient le nombre de types de sensibilité associés au moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| sensitivityTypesSize | Sortie Nombre de types de sensibilité |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypes"></a>MIP_CC_PolicyEngine_GetSensitivityTypes

Obtient les types de sensibilité associés au moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| sensitivityTypeBuffer | Sortie Mémoire tampon dans laquelle les types de sensibilité seront copiés. Sensibilité |
| sensitivityTypeBufferSize | Taille (en nombre de types de sensibilité) du sensitivityTypeBuffer. |
| actualSensitivityTypesSize | Sortie Nombre de types de sensibilité écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si sensitivityTypeBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualSensitivityTypesSize est défini sur la taille de mémoire tampon minimale requise 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypes(
    const mip_cc_policy_engine engine,
    mip_cc_sensitivity_type* sensitivityTypeBuffer,
    const int64_t sensitivityTypeBufferSize,
    int64_t* actualSensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_createpolicyhandler"></a>MIP_CC_PolicyEngine_CreatePolicyHandler

Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| isAuditDiscoveryEnabled | Indique si la détection d’audit est activée |
| gestionnaire | Sortie Instance du gestionnaire de stratégie nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_CreatePolicyHandler(
    const mip_cc_policy_engine engine,
    const bool isAuditDiscoveryEnabled,
    mip_cc_policy_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_sendapplicationauditevent"></a>MIP_CC_PolicyEngine_SendApplicationAuditEvent

Enregistre un événement spécifique de l’application dans le pipeline d’audit

**Paramètres**

Paramètre | Description
|---|---|
| niveau | Niveau de l’événement : info/Error/Warning |
| eventType | Description du type d’événement |
| eventData | Données associées à l’événement. |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_SendApplicationAuditEvent(
    const mip_cc_policy_engine engine,
    const char* level,
    const char* eventType,
    const char* eventData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantidsize"></a>MIP_CC_PolicyEngine_GetTenantIdSize

Obtient la taille de l’ID de locataire

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| tenantIdSize | Sortie Taille de l’ID de locataire (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantIdSize(
    const mip_cc_policy_engine engine,
    int64_t* tenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantid"></a>MIP_CC_PolicyEngine_GetTenantId

Obtient l’ID de locataire

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| tenantIdBuffer | Sortie Mémoire tampon dans laquelle l’ID de locataire sera copié. |
| tenantIdBufferSize | Taille (en nombre de caractères) du tenantIdBuffer. |
| actualTenantIdSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si tenantIdBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualTenantIdSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantId(
    const mip_cc_policy_engine engine,
    char* tenantIdBuffer,
    const int64_t tenantIdBufferSize,
    int64_t* actualTenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxmlsize"></a>MIP_CC_PolicyEngine_GetPolicyDataXmlSize

Obtient la taille du fichier XML de données de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| xmlSize | Sortie Taille du fichier XML de données de stratégie (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxml"></a>MIP_CC_PolicyEngine_GetPolicyDataXml

Obtient le XML des données de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| xmlBuffer | Sortie Mémoire tampon dans laquelle le XML sera copié. |
| xmlBufferSize | Taille (en nombre de caractères) du xmlBuffer. |
| actualXmlSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si xmlBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualXmlSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxmlsize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize

Obtient la taille des données XML des types de sensibilité

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| xmlSize | Sortie Taille du fichier XML de données de stratégie (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxml"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXml

Obtient le XML des données des types de sensibilité

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| xmlBuffer | Sortie Mémoire tampon dans laquelle le XML sera copié. |
| xmlBufferSize | Taille (en nombre de caractères) du xmlBuffer. |
| actualXmlSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si xmlBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualXmlSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdatasize"></a>MIP_CC_PolicyEngine_GetClientDataSize

Obtient la taille des données clientes associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| clientDataSize | Sortie Taille des données du client (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientDataSize(
    const mip_cc_policy_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdata"></a>MIP_CC_PolicyEngine_GetClientData

Obtenir des données client associées à un moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| moteur | Moteur de stratégie |
| clientDataBuffer | Sortie Mémoire tampon dans laquelle les données du client seront copiées |
| clientDataBufferSize | Taille (en nombre de caractères) de clientDataBuffer. |
| actualClientDataSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si clientDataBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualClientDataSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientData(
    const mip_cc_policy_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createpolicyenginesettingswithidentity"></a>MIP_CC_CreatePolicyEngineSettingsWithIdentity

Créer un objet de paramètres utilisé pour créer un tout nouveau moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| identité | Identité qui sera associée à PolicyEngine |
| ClientData : | Données client personnalisables stockées avec le moteur |
| locale | Paramètres régionaux dans lesquels les résultats de texte seront générés |
| loadSensitivityTypes | Si les données des types de sensibilité (pour la classification) doivent également être chargées |
| paramètres | Sortie Instance de paramètres nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: « loadSensitivityTypes » doit avoir la valeur « true » uniquement si l’application s’attend à appeler ultérieurement MIP_CC_PolicyEngine_GetSensitivityTypes. Dans le cas contraire, elle doit avoir la valeur false pour éviter une opération HTTP inutile. 

```c
mip_cc_result MIP_CC_CreatePolicyEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    bool loadSensitivityTypes,
    mip_cc_policy_engine_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setclientdata"></a>MIP_CC_PolicyEngineSettings_SetClientData

Définit les données du client qui seront stockées de façon opaque à côté de ce moteur et qui sont conservées entre les sessions

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| ClientData : | Données client |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetClientData(
    const mip_cc_policy_engine_settings settings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcustomsettings"></a>MIP_CC_PolicyEngineSettings_SetCustomSettings

Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités.

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| customSettings | Paires clé/valeur de paramètres personnalisés |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCustomSettings(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setsessionid"></a>MIP_CC_PolicyEngineSettings_SetSessionId

Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| sessionID | ID de session qui représente la durée de vie d’un moteur de stratégie |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetSessionId(
    const mip_cc_policy_engine_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloud"></a>MIP_CC_PolicyEngineSettings_SetCloud

Définit le Cloud qui affecte les URL de point de terminaison pour toutes les demandes de service

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| cloud | Identificateur de Cloud (valeur par défaut = inconnu) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si le Cloud n’est pas spécifié, le Cloud global est utilisé par défaut. 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloud(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloudendpointbaseurl"></a>MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl

Définit l’URL de base pour toutes les demandes de service

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| cloudEndpointBaseUrl | URL de base (par exemple, « https://dataservice.protection.outlook.com ») |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: cette valeur est lue uniquement et doit être définie pour Cloud = MIP_CLOUD_CUSTOM 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_policy_engine_settings settings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setdelegateduseremail"></a>MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail

Définit l’utilisateur délégué

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| delegatedUserEmail | Adresse e-mail de l’utilisateur délégué |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail(
    const mip_cc_policy_engine_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setlabelfilter"></a>MIP_CC_PolicyEngineSettings_SetLabelFilter

Définit le filtre d’étiquette

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur |
| labelFilter | enum représentant le filtre d’étiquette, si la valeur par défaut est hyok, doublekeyencryption |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetLabelFilter(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_label_filter labelFilter,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyenginesettings"></a>MIP_CC_ReleasePolicyEngineSettings

Libérer les ressources associées aux paramètres du moteur de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du moteur de stratégie à libérer |

```c
void MIP_CC_ReleasePolicyEngineSettings(mip_cc_policy_engine_settings settings);
```

## <a name="mip_cc_releasepolicyhandler"></a>MIP_CC_ReleasePolicyHandler

Libérer les ressources associées à un gestionnaire de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire de stratégie à libérer |

```c
void MIP_CC_ReleasePolicyHandler(mip_cc_policy_handler handler);
```

## <a name="mip_cc_policyhandler_getsensitivitylabel"></a>MIP_CC_PolicyHandler_GetSensitivityLabel

Obtient l’étiquette actuelle d’un document

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire de stratégie |
| documentState | État du document |
| contexte | Contexte d’application transféré de manière opaque à tous les rappels |
| contentLabel | Étiquette actuellement appliquée à un document |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyHandler_GetSensitivityLabel(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const void* context,
    mip_cc_content_label* contentLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_computeactions"></a>MIP_CC_PolicyHandler_ComputeActions

Exécute les règles de stratégie en fonction de l’état fourni et détermine les actions correspondantes

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire de stratégie |
| documentState | État du document |
| applicationState | État des actions de l’application |
| contexte | Contexte d’application transféré de manière opaque à tous les rappels |
| actionResult | Sortie Actions qui doivent être effectuées par l’application, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable « actionResult » doit être libérée par l’appelant en appelant MIP_CC_ReleaseActionResult 

```c
mip_cc_result MIP_CC_PolicyHandler_ComputeActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_action_result* actionResult,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_notifycommittedactions"></a>MIP_CC_PolicyHandler_NotifyCommittedActions

Appelé par l’application après que des actions calculées ont été appliquées et que des données ont été validées sur le disque

**Paramètres**

Paramètre | Description
|---|---|
| gestionnaire | Gestionnaire de stratégie |
| documentState | État du document |
| applicationState | État des actions de l’application |
| contexte | Contexte d’application transféré de manière opaque à tous les rappels |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: un appel à cette fonction est nécessaire pour transmettre des données d’audit des étiquettes complètes. 

```c
mip_cc_result MIP_CC_PolicyHandler_NotifyCommittedActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofile_acquireauthtoken"></a>MIP_CC_PolicyProfile_AcquireAuthToken

Déclencher un rappel d’authentification

**Paramètres**

Paramètre | Description
|---|---|
| profile | Profil |
| cloud | Cloud Azure |
| authCallback | Rappel d’authentification qui sera appelé |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: MIP ne met pas en cache ou ne fait rien d’autre avec la valeur retournée par le délégué auth. Cette fonction est recommandée pour les applications qui ne sont pas « connectées » jusqu’à ce que MIP demande un jeton d’authentification. Elle permet à une application d’extraire un jeton avant que MIP en ait réellement besoin. 

```c
mip_cc_result MIP_CC_PolicyProfile_AcquireAuthToken(
    const mip_cc_policy_profile profile,
    const mip_cc_cloud cloud,
    const mip_cc_auth_callback authCallback,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_loadpolicyprofile"></a>MIP_CC_LoadPolicyProfile

Charger un profil

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du profil |
| profile | Sortie Instance de profil de stratégie nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_LoadPolicyProfile(
    const mip_cc_policy_profile_settings settings,
    mip_cc_policy_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofile"></a>MIP_CC_ReleasePolicyProfile

Libérer les ressources associées à un profil de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| profile | Profil de stratégie à libérer |

```c
void MIP_CC_ReleasePolicyProfile(mip_cc_policy_profile profile);
```

## <a name="mip_cc_createpolicyprofilesettings"></a>MIP_CC_CreatePolicyProfileSettings

Créer un objet de paramètres utilisé pour créer un profil de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| mipContext | Contexte global partagé entre tous les profils |
| cacheStorageType | Configuration du cache de stockage |
| authCallback | Objet de rappel à utiliser pour l’authentification, implémenté par l’application cliente |
| paramètres | Sortie Instance de paramètres nouvellement créée |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_CreatePolicyProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    mip_cc_policy_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setsessionid"></a>MIP_CC_PolicyProfileSettings_SetSessionId

Définit l’ID de session qui peut être utilisé pour mettre en corrélation les journaux et la télémétrie

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du profil |
| sessionID | ID de session qui représente la durée de vie d’un profil de stratégie |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetSessionId(
    const mip_cc_policy_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_sethttpdelegate"></a>MIP_CC_PolicyProfileSettings_SetHttpDelegate

Remplacer la pile HTTP par défaut par le propriétaire du client

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres de profil auxquels le délégué HTTP sera affecté |
| httpDelegate | Instance de rappel HTTP implémentée par l’application cliente |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetHttpDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate

Remplacer le répartiteur de tâches Async par défaut par le propriétaire du client

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres de profil auxquels le délégué de répartiteur de tâches sera affecté |
| taskDispatcherDelegate | Instance de rappel de répartiteur de tâches implémentée par l’application cliente |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setcustomsettings"></a>MIP_CC_PolicyProfileSettings_SetCustomSettings

Configure les paramètres personnalisés, utilisés pour la régulation et le test des fonctionnalités.

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres du profil |
| customSettings | Paires clé/valeur de paramètres personnalisés |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetCustomSettings(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofilesettings"></a>MIP_CC_ReleasePolicyProfileSettings

Libérer les ressources associées à des paramètres de profil de stratégie

**Paramètres**

Paramètre | Description
|---|---|
| paramètres | Paramètres de profil de stratégie à libérer |

```c
void MIP_CC_ReleasePolicyProfileSettings(mip_cc_policy_profile_settings profileSettings);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize

Obtient la taille de la mémoire tampon requise pour stocker l’URL de chiffrement à clé double.

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par la stratégie ad hoc avec une clé double » |
| URL | Sortie Taille de la mémoire tampon devant contenir l’URL (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl

Obtient l’URL de chiffrement à clé double

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par la stratégie ad hoc avec une clé double » |
| urlBuffer | Sortie Mémoire tampon dans laquelle l’URL sera copiée. |
| urlBufferSize | Taille (en nombre de caractères) du urlBuffer. |
| actualUrlSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si urlBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualUrlSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplateaction_gettemplateid"></a>MIP_CC_ProtectByTemplateAction_GetTemplateId

Obtient un ID de modèle d’action « protéger par le modèle »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par modèle » |
| templateId | Sortie ID du modèle qui définit les protections |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectByTemplateAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_gettemplateid"></a>MIP_CC_ProtectByTemplateDkAction_GetTemplateId

Obtient un ID de modèle d’action « protéger par le modèle avec la double clé »

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par modèle » |
| templateId | Sortie ID du modèle qui définit les protections |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize

Obtient la taille de la mémoire tampon requise pour stocker l’URL de chiffrement à clé double.

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par un modèle avec une clé double » |
| URL | Sortie Taille de la mémoire tampon devant contenir l’URL (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl

Obtient l’URL de chiffrement à clé double

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par un modèle avec une clé double » |
| urlBuffer | Sortie Mémoire tampon dans laquelle l’URL sera copiée. |
| urlBufferSize | Taille (en nombre de caractères) du urlBuffer. |
| actualUrlSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si urlBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualUrlSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize

Obtient la taille de la mémoire tampon requise pour stocker l’URL de chiffrement à clé double.

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par un point de distribution non transféré avec une clé double » |
| URL | Sortie Taille de la mémoire tampon devant contenir l’URL (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl

Obtient l’URL de chiffrement à clé double

**Paramètres**

Paramètre | Description
|---|---|
| action | action « protéger par un point de distribution non transféré avec une clé double » |
| urlBuffer | Sortie Mémoire tampon dans laquelle l’URL sera copiée. |
| urlBufferSize | Taille (en nombre de caractères) du urlBuffer. |
| actualUrlSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si urlBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualUrlSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentfooteraction_getuielementnames"></a>MIP_CC_RemoveContentFooterAction_GetUIElementNames

Obtient les noms des éléments d’interface utilisateur de l’action supprimer le pied de page de contenu à supprimer

**Paramètres**

Paramètre | Description
|---|---|
| action | action « supprimer le pied de page de contenu » |
| noms | Sortie Noms des éléments d’interface utilisateur à supprimer, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable’Names’doit être libérée par l’appelant en appelant MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentFooterAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentheaderaction_getuielementnames"></a>MIP_CC_RemoveContentHeaderAction_GetUIElementNames

Obtient les noms des éléments d’interface utilisateur de l’action supprimer l’en-tête de contenu à supprimer

**Paramètres**

Paramètre | Description
|---|---|
| action | action « supprimer l’en-tête de contenu » |
| noms | Sortie Noms des éléments d’interface utilisateur à supprimer, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable’Names’doit être libérée par l’appelant en appelant MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentHeaderAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removewatermarkaction_getuielementnames"></a>MIP_CC_RemoveWatermarkAction_GetUIElementNames

Obtient les noms des éléments d’interface utilisateur de l’action « supprimer le filigrane » à supprimer

**Paramètres**

Paramètre | Description
|---|---|
| action | action « supprimer le pied de page du filigrane » |
| noms | Sortie Noms des éléments d’interface utilisateur à supprimer, mémoire dont l’appelant est propriétaire |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: la variable’Names’doit être libérée par l’appelant en appelant MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveWatermarkAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasesensitivitytype"></a>MIP_CC_ReleaseSensitivityType

Libérer les ressources associées à un type de sensibilité

**Paramètres**

Paramètre | Description
|---|---|
| sensitivityType | Type de sensibilité à libérer |

```c
void MIP_CC_ReleaseSensitivityType(mip_cc_sensitivity_type sensitivityType);
```

## <a name="mip_cc_sensitivitytype_getrulepackageidsize"></a>MIP_CC_SensitivityType_GetRulePackageIdSize

Obtient la taille de la mémoire tampon requise pour stocker l’ID de package de règles d’un type de sensibilité

**Paramètres**

Paramètre | Description
|---|---|
| sensitivityType | Type de sensibilité |
| idSize | Sortie Taille de la mémoire tampon de stockage de l’ID de package de la règle (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageIdSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackageid"></a>MIP_CC_SensitivityType_GetRulePackageId

Obtient l’ID de package de règle d’un type de sensibilité

**Paramètres**

Paramètre | Description
|---|---|
| sensitivityType | Type de sensibilité |
| idBuffer | Sortie Mémoire tampon dans laquelle l’ID sera copié. |
| idBufferSize | Taille (en nombre de caractères) du idBuffer. |
| actualIdSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si idBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualIdSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageId(
    const mip_cc_sensitivity_type sensitivityType,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackagesize"></a>MIP_CC_SensitivityType_GetRulePackageSize

Obtient la taille de la mémoire tampon requise pour stocker le package de règles d’un type de sensibilité

**Paramètres**

Paramètre | Description
|---|---|
| sensitivityType | Type de sensibilité |
| rulePackageSize | Sortie Taille de la mémoire tampon de stockage du package de règles (en nombre de caractères) |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* rulePackageSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackage"></a>MIP_CC_SensitivityType_GetRulePackage

Obtient le package de règles d’un type de sensibilité

**Paramètres**

Paramètre | Description
|---|---|
| sensitivityType | Type de sensibilité |
| rulePackageBuffer | Sortie Mémoire tampon dans laquelle le package de règles sera copié. |
| rulePackageBufferSize | Taille (en nombre de caractères) du rulePackageBuffer. |
| actualRulePackageSize | Sortie Nombre de caractères écrits dans la mémoire tampon |
| errorInfo | Sortie Facultatif Informations d’échec si le résultat de l’opération est une erreur |

**Retour**: code de résultat indiquant la réussite ou l’échec

**Remarque**: si rulePackageBuffer a la valeur null ou est insuffisante, MIP_RESULT_ERROR_INSUFFICIENT_BUFFER est retourné et actualRulePackageSize est défini sur la taille de mémoire tampon minimale requise. 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackage(
    const mip_cc_sensitivity_type sensitivityType,
    char* rulePackageBuffer,
    const int64_t rulePackageBufferSize,
    int64_t* actualRulePackageSize,
    mip_cc_error* errorInfo);
```

