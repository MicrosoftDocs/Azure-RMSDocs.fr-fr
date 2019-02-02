---
title: SDK MIP des énumérations et structures de référence C++
description: Documentation de référence sur les structures C++ MIP SDK et les énumérations.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d3ca101d3141f2a1e36fcfec11e805907c125b8e
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651766"
---
# <a name="summary"></a>Récapitulatif

 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
**Namespace `mip` :** |
enum ActionSource       |  définit ce qui a déclenché l’événement SetLabel
enum ActionType       |  Différents types d’actions.
méthode d’assignation d’enum       |  La méthode d’affectation de l’étiquette sur le document. Si l’affectation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’une opération nécessitant des privilèges (l’équivalent à une opération d’administrateur).
enum Consent       |  Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
enum ContentFormat       |  Format de contenu.
enum ContentMarkAlignment       |  Alignement contenu marque (en-tête de contenu ou un pied de page de contenu).
enum ContentState       |  Définit l’état des données de l’application agit.
enum ErrorType       | _Pas encore documenté._
enum HttpRequestType       |  Type de requête HTTP.
enum LogLevel       |  Différents niveaux de journalisation utilisés dans le SDK MIP.
enum ProtectionHandlerCreationOptions       |  Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.
enum ProtectionType       |  Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
enum WatermarkLayout       |  Disposition des filigranes.
struct ApplicationInfo  |  Struct qui inclut des informations spécifiques à l’application.
struct PublishingLicenseContext | Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
  
## <a name="enumerations-mip"></a>Énumérations (`mip`)

### <a name="actionsource-enum"></a>ActionSource enum

Définit ce qui a déclenché l’événement SetLabel

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
MANUELLE            | Sélectionnés manuellement par l’utilisateur
AUTOMATIQUE            | Défini par les conditions de stratégie
RECOMMANDÉ            | Défini par l’utilisateur après que l’étiquette a été recommandée par conditions de stratégie
PAR DÉFAUT            | La valeur par défaut dans la stratégie
OBLIGATOIRE            | Défini par l’utilisateur après la stratégie appliquée pour définir une étiquette


### <a name="actiontype-enum"></a>ActionType enum

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

### <a name="assignmentmethod-enum"></a>Méthode d’assignation enum

La méthode d’affectation de l’étiquette sur le document. Si l’affectation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’une opération nécessitant des privilèges (l’équivalent à une opération d’administrateur).

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
STANDARD            | [Étiquette](class_mip_label.md) méthode d’attribution est standard
PRIVILÉGIÉ            | [Étiquette](class_mip_label.md) privilégiée de la méthode d’affectation
AUTO            | [Étiquette](class_mip_label.md) méthode d’affectation est automatique


### <a name="consent-enum"></a>Consentement de l’enum

Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
AcceptAlways            | Consentement, et se souvenir de cette décision
Accepter            | Consentement, une seule fois
Rejeter            | Ne pas donner son consentement


### <a name="contentformat-enum"></a>ContentFormat enum

Format de contenu.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
PAR DÉFAUT            | Format de contenu est le format de fichier standard
E-MAIL            | Format de contenu est le format de courrier électronique

### <a name="contentmarkalignment-enum"></a>ContentMarkAlignment enum

Alignement contenu marque (en-tête de contenu ou un pied de page de contenu).

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
GAUCHE            | Marquage de contenu est aligné à gauche
OUI            | Marquage de contenu est aligné à droite
CENTRE            | Marquage de contenu est centré.

### <a name="contentstate-enum"></a>ContentState enum

Définit l’état des données de l’application agit.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
REST            | Stockées physiquement dans le fichier/bases de données/entrepôts de données inactives
MOTION            | Données parcourant un réseau ou temporairement résidant dans la mémoire de l’ordinateur en lecture ou mise à jour
UTILISATION            | Données actives sous des modifications constantes stockées physiquement dans le fichier/bases de données/entrepôts etc.

### <a name="errortype-enum"></a>ErrorType enum

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
  
### <a name="httprequesttype-enum"></a>HttpRequestType enum

Type de requête HTTP.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Obtenir            | GET
Post            | PUBLIER

  
### <a name="loglevel-enum"></a>LogLevel enum

Différents niveaux de journalisation utilisés dans le SDK MIP.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
trace            | 
Info            | 
Warning            | 
Erreur            | 

  
### <a name="protectionhandlercreationoptions-enum"></a>ProtectionHandlerCreationOptions enum

Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Aucune            | Aucune
OfflineOnly            | Ne pas autoriser les opérations réseau et de l’interface utilisateur.
AllowAuditedExtraction            | Le contenu peut être ouvert dans une application non compatible avec le SDK de protection
PreferDeprecatedAlgorithms            | Utiliser des algorithmes de chiffrement (ECB) déconseillés pour la compatibilité descendante
  
### <a name="protectiontype-enum"></a>ProtectionType enum

Décrit si protection est basée sur un modèle ou un ad-hoc (personnalisé).

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
TemplateBased            | Handle créé à partir d’un modèle
Custom            | Handle créé ad hoc
  
### <a name="watermarklayout-enum"></a>WatermarkLayout enum

Disposition des filigranes.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
HORIZONTAL            | Disposition du filigrane est horizontale
DIAGONALE            | Disposition du filigrane est en diagonale


## <a name="structures"></a>Structures 

### `mip::ApplicationInfo` 

Struct qui inclut des informations spécifiques à l’application.
  
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Identificateur d’application comme défini dans le portail AAD, (doit être d’un GUID sans crochets).
 public std::string applicationName  |  Nom de l’application (doit contenir uniquement l’exclusion de caractère ASCII valide ';')
 public std::string applicationVersion  |  La version de l’application utilisée, (doit contenir uniquement l’exclusion de caractère ASCII valide ';')
  
### `mip::PublishingLicenseContext` 

Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
  
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector\<uint8_t\> licenseInfo  | _Pas encore documenté._
public const std::vector\<uint8_t\> serializedPublishingLicense  | _Pas encore documenté._
public PublishingLicenseContext(const std::vector\<uint8_t\>& licenseInfo, const std::vector\<uint8_t\>& serializedPublishingLicense)  | _Pas encore documenté._
  
