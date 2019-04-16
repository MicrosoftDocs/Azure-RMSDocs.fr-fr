---
title: SDK MIP des énumérations et structures de référence C++
description: Documentation de référence sur les structures C++ MIP SDK et les énumérations.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: c9e634d436d02b147fc10a734c8c3d5b1fcdec71
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573953"
---
# <a name="enumerations-and-structures"></a>Énumérations et Structures

## <a name="namespace-mip"></a>Namespace mip

 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
enum ActionSource       |  définit ce qui a déclenché l’événement SetLabel
enum ActionType       |  Différents types d’actions.
méthode d’assignation d’enum       |  La méthode d’affectation de l’étiquette sur le document. Si l’affectation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’une opération nécessitant des privilèges (l’équivalent à une opération d’administrateur).
enum Consent       |  Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
enum ContentFormat       |  Format de contenu.
enum ContentMarkAlignment       |  Alignement contenu marque (en-tête de contenu ou un pied de page de contenu).
enum DataState       |  Définit l’état des données de l’application agit.
enum ErrorType       | _Pas encore documenté._
enum HttpRequestType       |  Type de requête HTTP.
enum LogLevel       |  Différents niveaux de journalisation utilisés dans le SDK MIP.
enum ProtectionHandlerCreationOptions       |  Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.
enum ProtectionType       |  Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
enum WatermarkLayout       |  Disposition des filigranes.
struct ApplicationInfo  |  Struct qui inclut des informations spécifiques à l’application.
struct PublishingLicenseContext  |  Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
  
## <a name="enumerations-mip"></a>Énumérations (MIP)

### <a name="actionsource"></a>ActionSource

Définit ce qui a déclenché l’événement SetLabel.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
MANUELLE            | Sélectionnés manuellement par l’utilisateur
AUTOMATIQUE            | Défini par les conditions de stratégie
RECOMMANDÉ            | Défini par l’utilisateur après que l’étiquette a été recommandée par conditions de stratégie
DEFAULT            | La valeur par défaut dans la stratégie
OBLIGATOIRE            | Défini par l’utilisateur après la stratégie appliquée pour définir une étiquette



### <a name="actiontype"></a>ActionType

Différents types d’actions. CUSTOM est le type d’action générique. Les autres types d’actions correspondent à une action spécifique avec une signification particulière.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | Ajouter un pied de page de contenu au type d’action du document.
ADD_CONTENT_HEADER            | Ajouter un en-tête de contenu au type d’action du document.
ADD_WATERMARK            | Ajouter un filigrane au type d’action du document entier.
PERSONNALISÉ            | Type d’action personnalisée.
JUSTIFY            | Type d’action Justifier.
MÉTADONNÉES            | Type d’action Modifier les métadonnées.
PROTECT_ADHOC            | Type d’action Protéger par stratégie ad hoc.
PROTECT_BY_TEMPLATE            | Type d’action Protéger par modèle.
PROTECT_DO_NOT_FORWARD            | Type d’action Protéger en n’effectuant pas de transfert.
REMOVE_CONTENT_FOOTER            | Type d’action Supprimer le pied de page de contenu.
REMOVE_CONTENT_HEADER            | Type d’action Supprimer l’en-tête de contenu.
REMOVE_PROTECTION            | Type d’action Supprimer la protection.
REMOVE_WATERMARK            | Type d’action Supprimer le filigrane.
APPLY_LABEL            | Type d’action Appliquer une étiquette.
RECOMMEND_LABEL            | Type d’action Recommander une étiquette.


### <a name="assignmentmethod"></a>AssignmentMethod

La méthode d’affectation de l’étiquette sur le document. Si l’affectation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’une opération nécessitant des privilèges (l’équivalent à une opération d’administrateur).

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
STANDARD            | [Étiquette](class_mip_label.md) méthode d’attribution est standard
PRIVILÉGIÉ            | [Étiquette](class_mip_label.md) privilégiée de la méthode d’affectation
AUTO            | [Étiquette](class_mip_label.md) méthode d’affectation est automatique


### <a name="consent"></a>Consentement

Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
AcceptAlways            | Consentement, et se souvenir de cette décision
Accepter            | Consentement, une seule fois
Rejeter            | Ne pas donner son consentement


### <a name="contentformat"></a>ContentFormat

Format de contenu.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
DEFAULT            | Format de contenu est le format de fichier standard
E-MAIL            | Format de contenu est le format de courrier électronique

### <a name="contentmarkalignment"></a>ContentMarkAlignment

Alignement contenu marque (en-tête de contenu ou un pied de page de contenu).

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
LEFT            | Marquage de contenu est aligné à gauche
RIGHT            | Marquage de contenu est aligné à droite
DE DONNÉES            | Marquage de contenu est centré.

### <a name="datastate"></a>DataState
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
REST            | Stockées physiquement dans le fichier/bases de données/entrepôts de données inactives
MOTION            | Données parcourant un réseau ou temporairement résidant dans la mémoire de l’ordinateur en lecture ou mise à jour
UTILISATION            | Données actives sous des modifications constantes stockées physiquement dans le fichier/bases de données/entrepôts etc.


### <a name="errortype"></a>ErrorType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | L’appelant a passée une entrée incorrecte.
FILE_IO_ERROR            | Erreur E/S de fichier générale.
NETWORK_ERROR            | Problèmes de réseau d’ordre général ; par exemple, service inaccessible.
TRANSIENT_NETWORK_ERROR            | Problèmes réseau temporaires ; par exemple, la passerelle incorrecte.
INTERNAL_ERROR            | Erreurs internes inattendues.
JUSTIFICATION_REQUIRED            | Une justification doit être fournie pour effectuer l’action sur le fichier.
NOT_SUPPORTED_OPERATION            | L’opération demandée n’est pas encore prise en charge.
PRIVILEGED_REQUIRED            | Impossible de remplacer l’étiquette privilégiée lorsque la méthode de nouvelle étiquette est standard.
ACCESS_DENIED            | L’utilisateur n’a pas pu obtenir l’accès aux services.
CONSENT_DENIED            | Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
POLICY_SYNC_ERROR            | Une tentative de synchronisation des données de stratégie a échoué.
NO_PERMISSIONS            | L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenue ne retiré
NO_AUTH_TOKEN            | L’utilisateur n’a pas pu obtenir l’accès au contenu en raison d’un jeton d’authentification vide.
DISABLED_SERVICE            | L’utilisateur Impossible d’accéder au contenu en raison de désactiver le service
PROXY_AUTH_ERROR            | Échoué de l’authentification de proxy.
NO_POLICY_ERROR            | Aucune stratégie n’est configuré pour l’utilisateur/client
OPERATION_CANCELLED            | Opération annulée
ADHOC_PROTECTION_REQUIRED            | La protection ad hoc doit être définie pour effectuer l’action sur le fichier
  
### <a name="httprequesttype"></a>HttpRequestType

Type de requête HTTP.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Obtenir            | GET
Post            | PUBLIER

  
### <a name="loglevel"></a>LogLevel

Différents niveaux de journalisation utilisés dans le SDK MIP.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Warning            | 
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Aucune            | Aucune
OfflineOnly            | Ne pas autoriser les opérations réseau et de l’interface utilisateur.
AllowAuditedExtraction            | Le contenu peut être ouvert dans une application non compatible avec le SDK de protection
PreferDeprecatedAlgorithms            | Utiliser des algorithmes de chiffrement (ECB) déconseillés pour la compatibilité descendante


### <a name="protectiontype"></a>ProtectionType

Décrit si protection est basée sur un modèle ou un ad-hoc (personnalisé).

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
TemplateBased            | Handle créé à partir d’un modèle
Custom            | Handle créé ad hoc

  
### <a name="watermarklayout"></a>WatermarkLayout

Disposition des filigranes.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
HORIZONTAL            | Disposition du filigrane est horizontale
DIAGONALE            | Disposition du filigrane est en diagonale


## <a name="structures"></a>Structures 

### <a name="mipapplicationinfo"></a>mip::ApplicationInfo 
Struct qui inclut des informations spécifiques à l’application.
  
#### <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificateur d’application comme défini dans le portail AAD, (doit être d’un GUID sans crochets).
public std::string applicationName  |  Nom de l’application (doit contenir uniquement l’exclusion de caractère ASCII valide ';')
public std::string applicationVersion  |  La version de l’application utilisée, (doit contenir uniquement l’exclusion de caractère ASCII valide ';')
  
#### <a name="members"></a>Membres
  
##### <a name="applicationid-struct-member"></a>membres de la structure applicationId
Identificateur d’application comme défini dans le portail AAD, (doit être d’un GUID sans crochets).
  
##### <a name="applicationname-struct-member"></a>membres de la structure applicationName
Nom de l’application (doit contenir uniquement l’exclusion de caractère ASCII valide ';')
  
##### <a name="applicationversion-struct-member"></a>membres de la structure applicationVersion
La version de l’application utilisée, (doit contenir uniquement l’exclusion de caractère ASCII valide ';')  

### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
  
#### <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector\<uint8_t\> licenseInfo  | _Pas encore documenté._
public const std::vector\<uint8_t\> serializedPublishingLicense  | _Pas encore documenté._
public PublishingLicenseContext(const std::vector\<uint8_t\>& licenseInfo, const std::vector\<uint8_t\>& serializedPublishingLicense)  | _Pas encore documenté._
  
#### <a name="members"></a>Membres
  
##### <a name="licenseinfo-struct-member"></a>membres de la structure licenseInfo
_Pas encore documenté._

  
##### <a name="serializedpublishinglicense-struct-member"></a>membres de la structure serializedPublishingLicense
_Pas encore documenté._

  
##### <a name="publishinglicensecontext-function"></a>PublishingLicenseContext function
_Pas encore documenté._
