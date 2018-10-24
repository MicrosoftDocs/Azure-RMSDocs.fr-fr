---
title: Résumé
description: Résumé
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5af209d5a627263399c8c60f474495dcadab24a0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446496"
---
# <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
**common** |
enum Consent       |  Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
struct ApplicationInfo  |  Struct qui inclut des informations spécifiques à l’application.
**mip** |
enum ErrorType       | _Pas encore documenté._
enum HttpRequestType       |  Type de requête HTTP.
enum LogLevel       |  Différents niveaux de journalisation utilisés dans le SDK MIP.
enum ProtectionHandlerCreationOptions       |  Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.
enum ProtectionType       |  Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
enum ActionType       |  Différents types d’actions.
struct mip::PublishingLicenseContext | Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.

  
## <a name="enumerations-common"></a>Énumérations (courantes)
  
### <a name="consent"></a>Consent
Représente la décision d’un utilisateur de donner son consentement pour se connecter à un point de terminaison de service.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
AcceptAlways            | Consentement, et se souvenir de cette décision
Accepter            | Consentement, une seule fois
Rejeter            | Ne pas donner son consentement
  
## <a name="enumerations-mip"></a>Énumérations (MIP)

### <a name="actiontype"></a>ActionType

Différents types d’actions.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | Ajouter un pied de page de contenu au type d’action du document.
ADD_CONTENT_HEADER            | Ajouter un en-tête de contenu au type d’action du document.
ADD_WATERMARK            | Ajouter un filigrane au type d’action du document entier.
PERSONNALISÉ            | Type d’action personnalisée.
JUSTIFY            | Type d’action Justifier.
METADATA            | Type d’action Modifier les métadonnées.
PROTECT_ADHOC            | Type d’action Protéger par stratégie ad hoc.
PROTECT_BY_TEMPLATE            | Type d’action Protéger par modèle.
PROTECT_DO_NOT_FORWARD            | Type d’action Protéger en n’effectuant pas de transfert.
REMOVE_CONTENT_FOOTER            | Type d’action Supprimer le pied de page de contenu.
REMOVE_CONTENT_HEADER            | Type d’action Supprimer l’en-tête de contenu.
REMOVE_PROTECTION            | Type d’action Supprimer la protection.
REMOVE_WATERMARK            | Type d’action Supprimer le filigrane.
APPLY_LABEL            | Type d’action Appliquer une étiquette.
RECOMMEND_LABEL            | Type d’action Recommander une étiquette.

CUSTOM est le type d’action générique. Les autres types d’actions correspondent à une action spécifique avec une signification particulière.

Les valeurs ActionType peuvent être combinées à l’aide des opérateurs suivants :

- Opérateur And (&) pour [Action](class_mip_action.md) (`operator &(ActionType a, ActionType b)`)
- Opérateur Or logique (Xor) (^) pour [Action](class_mip_action.md). (`operator ^(ActionType a, ActionType b)`)


### <a name="errortype"></a>ErrorType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | L’appelant a passée une entrée incorrecte.
FILE_IO_ERROR            | Erreur E/S de fichier générale.
NETWORK_ERROR            | Problèmes de réseau d’ordre général ; par exemple, service inaccessible.
TRANSIENT_NETWORK_ERROR            | Problèmes réseau temporaires, par exemple une passerelle incorrecte.
INTERNAL_ERROR            | Erreurs internes inattendues. Par exemple, dans le protocole client-serveur (réponse inattendue reçue).
JUSTIFICATION_REQUIRED            | Une justification doit être fournie pour effectuer l’action sur le fichier.
NOT_SUPPORTED_OPERATION            | L’opération demandée n’est pas encore prise en charge.
PRIVILEGED_REQUIRED            | Impossible de remplacer l’étiquette privilégiée lorsque la méthode de nouvelle étiquette est standard.
ACCESS_DENIED            | L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué, etc.
CONSENT_DENIED            | Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
  
### <a name="httprequesttype"></a>HttpRequestType
Type de requête HTTP.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Get            | GET
Post            | POST
  
### <a name="loglevel"></a>LogLevel

Différents niveaux de journalisation utilisés dans le SDK MIP.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Trace            | 
Informations            | 
Avertissement            | 
Erreur            | 
Différents niveaux de journal utilisés dans le SDK MIP.
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Aucune            | Aucune
OfflineOnly            | Ne pas autoriser les opérations réseau et de l’interface utilisateur.
AllowAuditedExtraction            | Le contenu peut être ouvert dans une application non compatible avec le SDK de protection
PreferDeprecatedAlgorithms            | Utiliser des algorithmes de chiffrement (ECB) déconseillés pour la compatibilité descendante


### <a name="protectiontype"></a>ProtectionType
Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
TemplateBased            | Handle créé à partir d’un modèle
Personnalisé            | Handle créé ad hoc

  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions
Opérateur OR au niveau du bit ProtectionHandlerCreationOptions.

Paramètres :  
* **a** : valeur gauche 

* **b** : valeur droite

### <a name="releaseallresources"></a>ReleaseAllResources
Libère toutes les ressources (threads, etc.) avant l’arrêt.
Si les bibliothèques dynamiques MIP sont chargées en différé par une application, cette fonction doit être appelée avant que l’application ne décharge explicitement ces bibliothèques MIP pour éviter un blocage. Par exemple, sur win32, cette fonction doit être appelée avant tout appel pour décharger explicitement les DLL MIP via FreeLibrary ou \__FUnloadDelayLoadedDLL2. Les applications doivent libérer les références à tous les objets MIP (par exemple, les profils, les moteurs, les gestionnaires) avant d’appeler cette fonction.
  
**Retourne** : OR au niveau du bit des paramètres
  
## <a name="structures"></a>Structures

### <a name="applicationinfo"></a>ApplicationInfo 
Struct qui inclut des informations spécifiques à l’application.

 Champs                        | Descriptions                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Identificateur d’application tel que défini dans le portail Azure AD.
 public std::string applicationName  |  Nom de l'application
 public std::string applicationVersion  |  Version de l’application utilisée
  
### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
  
 Champs                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector<uint8_t> licenseInfo  | _Pas encore documenté._
public const std::vector<uint8_t> serializedPublishingLicense  | _Pas encore documenté._
public PublishingLicenseContext(const std::vector<uint8_t>& licenseInfo, const std::vector<uint8_t>& serializedPublishingLicense)  | _Pas encore documenté._
  
