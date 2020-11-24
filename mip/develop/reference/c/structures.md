---
title: Structures
description: Celles.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 2939a4c64ab3e1a47704811875c6a7e941bcfe3c
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567342"
---
# <a name="structures"></a>Structures

## <a name="mip_cc_application_info"></a>mip_cc_application_info

Struct qui contient des informations spécifiques à l’application 

| Champ | Description |
|---|---|
| applicationId | Identificateur d’application tel qu’il est défini dans le portail AAD, (doit être un GUID sans crochets).  |
| applicationName | Nom de l’application, (doit contenir uniquement des caractères ASCII valides, à l’exception de « ; »)  |
| applicationVersion | Version de l’application utilisée, (ne doit contenir que des caractères ASCII valides, à l’exclusion de « ; »)   |


```c
typedef struct {
  const char* applicationId;      
  const char* applicationName;    
  const char* applicationVersion; 
} mip_cc_application_info;

```

## <a name="mip_cc_oauth2_challenge"></a>mip_cc_oauth2_challenge

Informations fournies par un serveur pour générer un jeton OAuth2

| Champ | Description |
|---|---|
| authority | Autorité OAuth2  |
| resource | Ressource OAuth2  |
| scope | Étendue OAuth2  |


```c
typedef struct {
  const char* authority; 
  const char* resource;  
  const char* scope;     
} mip_cc_oauth2_challenge;

```

## <a name="mip_cc_handle"></a>mip_cc_handle

Descripteur opaque vers l’objet MIP

| Champ | Description |
|---|---|
| typeId | Nombre magique identifiant de manière unique des types de descripteurs spécifiques  |
| Données | Données de handle brutes  |


```c
typedef struct {
  uint32_t typeId; 
  void* data;      
} mip_cc_handle;

```

## <a name="mip_cc_guid"></a>mip_cc_guid

GUID

```c
typedef struct {
  char guid[37];
} mip_cc_guid;

```

## <a name="mip_cc_kv_pair"></a>mip_cc_kv_pair

Paire clé/valeur

| Champ | Description |
|---|---|
| key | Clé :  |
| value | Valeur  |


```c
typedef struct {
  const char* key;   
  const char* value; 
} mip_cc_kv_pair;

```

## <a name="mip_cc_error"></a>mip_cc_error

Informations sur l'erreur

```c
typedef struct {
  mip_cc_result result;
  char description[ERROR_STRING_BUFFER_SIZE];

  // MIP_RESULT_ERROR_NETWORK details
  mip_cc_network_error_category networkError_Category;
  int32_t networkError_ResponseCode;

  // MIP_RESULT_ERROR_NO_PERMISSIONS details
  char noPermissionsError_Owner[ERROR_STRING_BUFFER_SIZE];
  char noPermissionsError_Referrer[ERROR_STRING_BUFFER_SIZE];

  // MIP_RESULT_ERROR_SERVICE_DISABLED details
  mip_cc_service_disabled_error_extent serviceDisabledError_Extent;
} mip_cc_error;

```

## <a name="mip_cc_http_header"></a>mip_cc_http_header

En-tête de requête/réponse HTTP

| Champ | Description |
|---|---|
| name | Nom/clé de l’en-tête  |
| value | Valeur de l’en-tête  |


```c
typedef struct {
  const char* name;  
  const char* value; 
} mip_cc_http_header;

```

## <a name="mip_cc_http_request"></a>mip_cc_http_request

Demande HTTP

| Champ | Description |
|---|---|
| id | ID de demande unique--corrélé avec la même propriété dans mip_cc_http_response  |
| type | Type de requête HTTP (par exemple, obtenir vs. poster)  |
| url | URL de la requête HTTP  |
| bodySize | Taille du corps de la requête HTTP en octets  |
| body | Mémoire tampon qui a le corps de la requête HTTP  |
| headersCount | Nombre d’en-têtes de requête HTTP  |
| headers | Mémoire tampon contenant les en-têtes de requête HTTP  |


```c
typedef struct {
  const char* id;                    
  mip_cc_http_request_type type;     
  const char* url;                   
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_request;

```

## <a name="mip_cc_http_response"></a>mip_cc_http_response

Réponse HTTP

| Champ | Description |
|---|---|
| id | ID de demande unique--corrélé avec la même propriété dans mip_cc_http_request  |
| statusCode | Code d’état de réponse HTTP  |
| bodySize | Taille du corps de la réponse HTTP en octets  |
| body | Mémoire tampon qui présente le corps de la réponse HTTP  |
| headersCount | Nombre d’en-têtes de réponse HTTP  |
| headers | Mémoire tampon contenant les en-têtes de réponse HTTP  |


```c
typedef struct {
  const char* id;                    
  int32_t statusCode;                
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_response;

```

## <a name="mip_cc_identity"></a>mip_cc_identity

Struct qui contient les informations d’identification de l’utilisateur

| Champ | Description |
|---|---|
| email | Adresse e-mail de l’utilisateur  |
| name | Nom convivial, utilisé pour le marquage du contenu.  |


```c
typedef struct {
  const char* email;          
  const char* name;           
} mip_cc_identity;

```

## <a name="mip_cc_feature_override"></a>mip_cc_feature_override

Définit l’état activé/désactivé d’une fonctionnalité unique

| Champ | Description |
|---|---|
| fonctionnalité | Nom de la fonctionnalité  |
| value | État activé/désactivé  |


```c
typedef struct {
  mip_cc_flighting_feature feature; 
  bool value;                       
} mip_cc_feature_override;

```

## <a name="mip_cc_user_rights"></a>mip_cc_user_rights

Un groupe d’utilisateurs et les droits qui leur sont associés

| Champ | Description |
|---|---|
| users | Liste des utilisateurs  |
| usersCount | Nombre d’utilisateurs  |
| droits | Liste des droits  |
| rightsCount | Nombre de droits  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** rights; 
  int64_t rightsCount; 
} mip_cc_user_rights;

```

## <a name="mip_cc_user_roles"></a>mip_cc_user_roles

Un groupe d’utilisateurs et les rôles qui leur sont associés

| Champ | Description |
|---|---|
| users | Liste des utilisateurs  |
| usersCount | Nombre d’utilisateurs  |
| roles | Liste des rôles  |
| rolesCount | Nombre de rôles  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** roles; 
  int64_t rolesCount; 
} mip_cc_user_roles;

```

## <a name="mip_cc_async_task"></a>mip_cc_async_task

Définit une demande de dispatch de tâche asynchrone unique

| Champ | Description |
|---|---|
| id | ID de la tâche  |
| delayMs | Différer jusqu’à l’exécution de la tâche (en millisecondes)  |
| executeOnIndependentThread | Indique si cette tâche doit s’exécuter sur un thread complètement indépendant ou si elle peut réutiliser un thread partagé  |


```c
typedef struct {
  const char* id;                   
  int64_t delayMs;                  
  bool executeOnIndependentThread;  
} mip_cc_async_task;

```

## <a name="mip_cc_application_action_state"></a>mip_cc_application_action_state

Représente l’état actuel de l’application lors de l’exécution d’une opération associée à une étiquette

| Champ | Description |
|---|---|
| actionState | Décrit si/comment une application tente de modifier l’état de l’étiquette.  |
| newLabel | Si « actionType » est « UPDATE » : nouvelle étiquette.  |
| newLabelExtendedProperties | Si « actionType » est « UPDATE » : propriétés supplémentaires à écrire dans les métadonnées.  |
| newLabelAssignmentMethod | Si « actionType » est « UPDATE » : méthode d’assignation de la nouvelle étiquette.  |
| isDowngradeJustified | Si « actionType » est « UPDATE » : indique si l’utilisateur a fait l’impossibilité de passer à une version antérieure.  |
| downgradeJustification | Si « actionType » est « UPDATE » : texte de justification de passage à une version antérieure fourni par l’utilisateur.  |
| supportedActions | Masque d’énumération décrivant les actions liées aux étiquettes qu’une application est en mesure d’effectuer.  |


```c
typedef struct {
  mip_cc_label_action_state actionState;                    
  mip_cc_label newLabel;                                    
  mip_cc_dictionary newLabelExtendedProperties;             
  mip_cc_label_assignment_method newLabelAssignmentMethod;  
  bool isDowngradeJustified;                                
  const char* downgradeJustification;                       
  mip_cc_label_action_type supportedActions;                
} mip_cc_application_action_state;

```

## <a name="mip_cc_document_state"></a>mip_cc_document_state

Définition de fonction de rappel pour la récupération du document refléter, filtrée par nom/préfixe.

| Champ | Description |
|---|---|
| dataState | État des données de document lorsque l’application interagit avec elle. |
| contentMetadataCallback | Rappel des métadonnées du document. |
| protectionDescriptor | Descripteur de protection si le document est actuellement protégé, sinon null.  |
| contentFormat | Format du document (fichier ou courrier électronique).  |
| auditMetadata | Métadonnées spécifiques à l’application facultatives qui sont utilisées lors de l’envoi de rapports d’audit. Valeurs reconnues : 'sender' : adresse e-mail de l’expéditeur ; « Recipients » : tableau JSON des destinataires du courrier électronique ; 'LastModifiedBy' : adresse de messagerie de l’utilisateur qui a modifié un document pour la dernière fois ; 'LastModifiedDate & ' : date de la dernière modification d’un document  |
| contentMetadataVersion | Version des métadonnées du document, la valeur par défaut doit être 0.  |
| contentMetadataVersionFormat | Décrit le mode de traitement du contrôle de version des métadonnées.  |

```c
typedef struct {

  const char* contentId;


  mip_cc_data_state dataState;

  mip_cc_metadata_callback contentMetadataCallback;

  mip_cc_protection_descriptor protectionDescriptor;

  mip_cc_content_format contentFormat;

  mip_cc_dictionary auditMetadata;

  uint32_t contentMetadataVersion;

  mip_cc_metadata_version_format contentMetadataVersionFormat;

} mip_cc_document_state;

```

## <a name="mip_cc_metadata_entry"></a>mip_cc_metadata_entry

Entrée de métadonnées

| Champ | Description |
|---|---|
| key | Entrée de clé |
| value | Entrée de valeur  |
| Version | L’entrée de version doit être initialisée à 0, sauf si elle est connue |


```c
typedef struct {
  const char* key;        
  const char* value;      
  uint32_t version;       
} mip_cc_metadata_entry;

```

