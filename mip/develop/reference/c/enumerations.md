---
title: Énumérations
description: Énumérations
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: f1ad15819d10bcded670fe519db07667b7e7331e
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73591616"
---
# <a name="enumerations"></a>Énumérations

## <a name="mip_cc_cache_storage_type"></a>mip_cc_cache_storage_type

Type de stockage pour les caches

| Champ | Description |
|---|---|
|  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0         | Stockage en mémoire  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1           | Stockage sur disque  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2  | Stockage sur disque avec chiffrement (si pris en charge par la plateforme)  |


```c
typedef enum {
  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0,        
  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1,          
  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2 
} mip_cc_cache_storage_type;

```

## <a name="mip_cc_content_format"></a>mip_cc_content_format

Format du contenu

| Champ | Description |
|---|---|
|  MIP_CONTENT_FORMAT_DEFAULT = 0  | Format de fichier standard  |
|  MIP_CONTENT_FORMAT_EMAIL = 1    | Adresse de messagerie  |


```c
typedef enum {
  MIP_CONTENT_FORMAT_DEFAULT = 0, 
  MIP_CONTENT_FORMAT_EMAIL = 1,   
} mip_cc_content_format;

```

## <a name="mip_cc_label_assignment_method"></a>mip_cc_label_assignment_method

Décrit comment une nouvelle étiquette est appliquée

| Champ | Description |
|---|---|
|  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0    | Les attributions d’étiquettes standard ne remplacent pas une attribution privilégiée antérieure.  |
|  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1  | Une attribution d’étiquette privilégiée ne sera pas remplacée par les futures attributions standard.  |
|  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2        | Réservé. Ne pas utiliser.  |


```c
typedef enum {
  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0,   
  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1, 
  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2,       
} mip_cc_label_assignment_method;

```

## <a name="mip_cc_content_mark_alignment"></a>mip_cc_content_mark_alignment

Alignement des marques de contenu (en-tête de contenu ou pied de page de contenu)

| Champ | Description |
|---|---|
|  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0    | Le marquage de contenu est aligné à gauche  |
|  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1   | Le marquage de contenu est aligné à droite  |
|  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2  | Le marquage du contenu est centré  |


```c
typedef enum {
  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0,   
  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1,  
  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2, 
} mip_cc_content_mark_alignment;

```

## <a name="mip_cc_watermark_layout"></a>mip_cc_watermark_layout

Disposition des filigranes

| Champ | Description |
|---|---|
|  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0  | La disposition du filigrane est horizontale  |
|  MIP_WATERMARK_LAYOUT_DIAGONAL = 1    | La disposition du filigrane est diagonale  |


```c
typedef enum {
  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0, 
  MIP_WATERMARK_LAYOUT_DIAGONAL = 1,   
} mip_cc_watermark_layout;

```

## <a name="mip_cc_consent"></a>mip_cc_consent

Réponse d’un utilisateur quand un consentement est demandé pour se connecter à un point de terminaison de service non reconnu

| Champ | Description |
|---|---|
|  MIP_CONSENT_ACCEPT_ALWAYS = 0  | Consentement et mémoriser cette décision  |
|  MIP_CONSENT_ACCEPT = 1         | Consentement une seule fois  |
|  MIP_CONSENT_REJECT = 2          | Ne pas donner son consentement  |


```c
typedef enum {
  MIP_CONSENT_ACCEPT_ALWAYS = 0, 
  MIP_CONSENT_ACCEPT = 1,        
  MIP_CONSENT_REJECT = 2         
} mip_cc_consent;

```

## <a name="mip_cc_flighting_feature"></a>mip_cc_flighting_feature

Définit de nouvelles fonctionnalités par nom

| Champ | Description |
|---|---|
|  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0      | S’appuyer sur un appel HTTP distinct pour déterminer les points de terminaison de service RMS (false par défaut) |
|  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1        | Mettez en cache les défis OAuth2 par domaine/locataire pour réduire les réponses 401 inutiles. Désactiver pour les applications/services qui gèrent leur propre authentification HTTP (true par défaut)  |
|  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2  | Activer la mise en cache chiffrée pour les plateformes Linux (false par défaut)  |
|  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3     | Activez le nom d’entreprise unique pour la recherche DNS. Exemple : https://corprights  |
|  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4            | Activez l’authentification HTTP automatique pour les requêtes envoyées au service de stratégie. Désactiver pour les applications/services qui gèrent leur propre authentification HTTP (true par défaut)  |


```c
typedef enum {
  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0,     
  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1,       
  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2, 
  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3,    
  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4,           
} mip_cc_flighting_feature;

```

## <a name="mip_cc_http_request_type"></a>mip_cc_http_request_type

Type de requête HTTP

| Champ | Description |
|---|---|
|  HTTP_REQUEST_TYPE_GET = 0   | HTTP-RÉCUPÉRATION  |
|  HTTP_REQUEST_TYPE_POST = 1  | HTTP APRÈS  |


```c
typedef enum {
  HTTP_REQUEST_TYPE_GET = 0,  
  HTTP_REQUEST_TYPE_POST = 1, 
} mip_cc_http_request_type;

```

## <a name="mip_cc_http_result"></a>mip_cc_http_result

État de réussite/d’échec de l’opération HTTP

| Champ | Description |
|---|---|
|  HTTP_RESULT_OK = 0       | L’opération HTTP a été effectuée avec succès  |
|  HTTP_RESULT_FAILURE = 1  | Échec de l’opération HTTP (par exemple, expiration du délai d’attente, défaillance réseau, etc.)  |


```c
typedef enum {
  HTTP_RESULT_OK = 0,      
  HTTP_RESULT_FAILURE = 1, 
} mip_cc_http_result;

```

## <a name="mip_cc_log_level"></a>mip_cc_log_level

Niveau de journalisation

| Champ | Description |
|---|---|
|  MIP_LOG_LEVEL_TRACE = 0   | Trace  |
|  MIP_LOG_LEVEL_INFO        | Informations  |
|  MIP_LOG_LEVEL_WARNING     | Avertissement  |
|  MIP_LOG_LEVEL_ERROR       | Erreur  |


```c
typedef enum {
  MIP_LOG_LEVEL_TRACE = 0,  
  MIP_LOG_LEVEL_INFO,       
  MIP_LOG_LEVEL_WARNING,    
  MIP_LOG_LEVEL_ERROR,      
} mip_cc_log_level;

```

## <a name="mip_cc_protection_type"></a>mip_cc_protection_type

Description précisant si la protection est définie par un modèle ou ad hoc

| Champ | Description |
|---|---|
|  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0  | Basé sur un modèle RMS  |
|  MIP_PROTECTION_TYPE_CUSTOM = 1          | Protection ad hoc personnalisée  |


```c
typedef enum {
  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0, 
  MIP_PROTECTION_TYPE_CUSTOM = 1,         
} mip_cc_protection_type;

```

## <a name="mip_cc_result"></a>mip_cc_result

Résultat de réussite ou d’échec de l’API

| Champ | Description |
|---|---|
|  MIP_RESULT_ERROR_UNKNOWN                    | Erreur inconnue  |
|  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER        | La mémoire tampon fournie par l’application est trop petite  |
|  MIP_RESULT_ERROR_BAD_INPUT                  | L’application a passé une entrée incorrecte  |
|  MIP_RESULT_ERROR_FILE_IO_ERROR              | Erreur d’e/s de fichier générale  |
|  MIP_RESULT_ERROR_NETWORK                    | Erreur réseau générale (par exemple, service inaccessible)  |
|  MIP_RESULT_ERROR_TRANSIENT_NETWORK          | Erreur réseau temporaire (par exemple, passerelle incorrecte)  |
|  MIP_RESULT_ERROR_INTERNAL                   | Erreur interne inattendue  |
|  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED     | Une justification doit être fournie pour effectuer l’action sur le fichier.  |
|  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION    | Opeation n’est pas pris en charge  |
|  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED        | Impossible de remplacer l’étiquette privilégiée quand elle est avec la méthode standard  |
|  MIP_RESULT_ERROR_ACCESS_DENIED              | L’utilisateur n’a pas les droits d’accès au service  |
|  MIP_RESULT_ERROR_CONSENT_DENIED             | Une opération nécessitant le consentement de l’utilisateur n’a pas été accordée  |
|  MIP_RESULT_ERROR_POLICY_SYNC                | Une tentative de synchronisation des données de stratégie a échoué  |
|  MIP_RESULT_ERROR_NO_PERMISSIONS             | L’utilisateur n’a pas pu accéder au contenu (par exemple, aucune autorisation, contenu révoqué)  |
|  MIP_RESULT_ERROR_NO_AUTH_TOKEN              | L’utilisateur n’a pas pu accéder au contenu en raison d’un jeton d’authentification vide  |
|  MIP_RESULT_ERROR_SERVICE_DISABLED           | L’utilisateur n’a pas pu accéder au contenu en raison de la désactivation du service  |
|  MIP_RESULT_ERROR_PROXY_AUTH                 | Échec de l’authentification du proxy  |
|  MIP_RESULT_ERROR_NO_POLICY                  | Aucune stratégie n’est configurée pour l’utilisateur/locataire  |
|  MIP_RESULT_ERROR_OPERATION_CANCELLED        | Opération annulée  |
|  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED  | La protection ad hoc doit être configurée pour terminer l’action sur le fichier  |
|  MIP_RESULT_ERROR_DEPRECATED_API             | L’appelant a appelé une API déconseillée  |
|  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND         | L’ID de modèle n’est pas reconnu  |
|  MIP_RESULT_ERROR_LABEL_NOT_FOUND            | ID d’étiquette non reconnu  |
|  MIP_RESULT_ERROR_LABEL_DISABLED             | L’étiquette est désactivée ou inactive  |


```c
typedef enum {
  MIP_RESULT_SUCCESS = 0,

  // MIP C API errors
  MIP_RESULT_ERROR_UNKNOWN,                   
  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER,       

  // MIP C++ exceptions
  MIP_RESULT_ERROR_BAD_INPUT,                 
  MIP_RESULT_ERROR_FILE_IO_ERROR,             
  MIP_RESULT_ERROR_NETWORK,                   
  MIP_RESULT_ERROR_TRANSIENT_NETWORK,         
  MIP_RESULT_ERROR_INTERNAL,                  
  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED,    
  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION,   
  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED,       
  MIP_RESULT_ERROR_ACCESS_DENIED,             
  MIP_RESULT_ERROR_CONSENT_DENIED,            
  MIP_RESULT_ERROR_POLICY_SYNC,               
  MIP_RESULT_ERROR_NO_PERMISSIONS,            
  MIP_RESULT_ERROR_NO_AUTH_TOKEN,             
  MIP_RESULT_ERROR_SERVICE_DISABLED,          
  MIP_RESULT_ERROR_PROXY_AUTH,                
  MIP_RESULT_ERROR_NO_POLICY,                 
  MIP_RESULT_ERROR_OPERATION_CANCELLED,       
  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED, 
  MIP_RESULT_ERROR_DEPRECATED_API,            
  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND,        
  MIP_RESULT_ERROR_LABEL_NOT_FOUND,           
  MIP_RESULT_ERROR_LABEL_DISABLED,            
} mip_cc_result;

```

## <a name="mip_cc_action_type"></a>mip_cc_action_type

Masque de bits de type action

| Champ | Description |
|---|---|
|  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | Ajouter un pied de page de contenu au type d’action du document. |
|  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | Ajouter un en-tête de contenu au type d’action du document. |
|  MIP_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | Ajouter un filigrane au type d’action du document entier. |
|  MIP_ACTION_TYPE_CUSTOM = 1 < < 3                  | Type d’action personnalisée. |
|  MIP_ACTION_TYPE_JUSTIFY = 1 < < 4                 | Type d’action Justifier. |
|  MIP_ACTION_TYPE_METADATA = 1 < < 5                | Type d’action Modifier les métadonnées. |
|  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | Type d’action Protéger par stratégie ad hoc. |
|  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | Type d’action Protéger par modèle. |
|  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | Type d’action Protéger en n’effectuant pas de transfert. |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | Type d’action Supprimer le pied de page de contenu. |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | Type d’action Supprimer l’en-tête de contenu. |
|  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | Type d’action Supprimer la protection. |
|  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | Type d’action Supprimer le filigrane. |
|  MIP_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | Type d’action Appliquer une étiquette. |
|  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | Type d’action Recommander une étiquette. |


```c
typedef enum {
  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_action_type;

```

## <a name="mip_cc_label_action_state"></a>mip_cc_label_action_state

Décrit ce que l’application tente de faire en ce qui concerne l’étiquette actuelle

| Champ | Description |
|---|---|
|  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0  | L’étiquette actuelle ne doit pas changer.  |
|  MIP_LABEL_ACTION_STATE_REMOVE = 1     | L’étiquette actuelle doit être supprimée.  |
|  MIP_LABEL_ACTION_STATE_UPDATE = 2     | L’étiquette actuelle doit être modifiée.  |


```c
typedef enum {
  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0, 
  MIP_LABEL_ACTION_STATE_REMOVE = 1,    
  MIP_LABEL_ACTION_STATE_UPDATE = 2,    
} mip_cc_label_action_state;

```

## <a name="mip_cc_label_action_type"></a>mip_cc_label_action_type

Actions liées aux étiquettes qu’une application comprend et prend en charge

| Champ | Description |
|---|---|
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | Ajouter un pied de page de contenu au type d’action du document.  |
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | Ajouter un en-tête de contenu au type d’action du document.  |
|  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | Ajouter un filigrane au type d’action du document entier.  |
|  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 < < 3                  | Type d’action personnalisée.  |
|  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 < < 4                 | Type d’action Justifier.  |
|  MIP_LABEL_ACTION_TYPE_METADATA = 1 < < 5                | Type d’action Modifier les métadonnées.  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | Type d’action Protéger par stratégie ad hoc.  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | Type d’action Protéger par modèle.  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | Type d’action Protéger en n’effectuant pas de transfert.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | Type d’action Supprimer le pied de page de contenu.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | Type d’action Supprimer l’en-tête de contenu.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | Type d’action Supprimer la protection.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | Type d’action Supprimer le filigrane.  |
|  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | Type d’action Appliquer une étiquette.  |
|  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | Type d’action Recommander une étiquette.  |


```c
typedef enum {
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_LABEL_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_label_action_type;

```

## <a name="mip_cc_data_state"></a>mip_cc_data_state

Définit l’état des données lorsqu’une application agit sur celle-ci

| Champ | Description |
|---|---|
|  MIP_DATA_STATE_REST = 0    | Données inactives stockées physiquement dans les bases de données/fichiers/entrepôts  |
|  MIP_DATA_STATE_MOTION = 1  | Les données qui traversent un réseau ou qui résident temporairement dans la mémoire de l’ordinateur à lire ou à mettre à jour  |
|  MIP_DATA_STATE_USE = 2     | Données actives sous modification constante stockées physiquement dans les bases de données/fichiers/entrepôts, etc.  |


```c
typedef enum {
  MIP_DATA_STATE_REST = 0,   
  MIP_DATA_STATE_MOTION = 1, 
  MIP_DATA_STATE_USE = 2,    
} mip_cc_data_state;

```

