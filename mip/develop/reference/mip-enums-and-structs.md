---
title: SDK MIP pour C++ les structs et les enums de référence
description: Documentation de référence sur C++ les structs et les enums du kit de développement logiciel (SDK) MIP.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6efe7910769dffe809e0661475f9adc8226b37b3
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884908"
---
# <a name="enumerations-and-structures"></a>Énumérations et structures

## <a name="namespace-mip"></a>Espace de noms MIP

 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
énumération WatermarkLayout       |  Disposition des filigranes.
énumération ContentMarkAlignment       |  Alignement des marques de contenu (en-tête de contenu ou pied de page de contenu).
énumération assignation       |  Méthode d’assignation de l’étiquette sur le document. Indique si l’assignation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’opération privilégiée (l’équivalent d’une opération d’administrateur).
énumération ActionSource       |  définit ce qui a déclenché l’événement SetLabel
énumération DataState       |  Définit l’état des données sur lequel l’application agit.
énumération ContentFormat       |  Format du contenu.
enum Consent       |  Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
énumération CacheStorageType       |  Type de stockage pour les caches.
enum ErrorType       | _Pas encore documenté._
énumération InspectorType       |  Type d’inspecteur en corrélation avec les types de fichiers pris en charge.
énumération BodyType       |  Énumérateur de type de corps.
énumération FlightingFeature       |  Définit de nouvelles fonctionnalités par nom.
enum HttpRequestType       |  Type de requête HTTP.
enum LogLevel       |  Différents niveaux de journalisation utilisés dans le SDK MIP.
enum ProtectionHandlerCreationOptions       |  Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.
enum ProtectionType       |  Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
enum ActionType       |  Différents types d’actions.
énumération LabelState       | _Pas encore documenté._
énumération ActionDataType       | _Pas encore documenté._
énumération ConditionDataType       | _Pas encore documenté._
énumération ContentMarkPlacement       | _Pas encore documenté._
énumération LabelActionDataType       | _Pas encore documenté._
énumération ProtectionActionType       | _Pas encore documenté._
MIP, struct:: ApplicationInfo  |  Struct qui inclut des informations spécifiques à l’application.
MIP, struct:: TelemetryConfiguration  |  Paramètres de télémétrie personnalisés (rarement utilisés)


## <a name="enumerations-mip"></a>Énumérations (MIP)

### <a name="watermarklayout-enum"></a>Énumération WatermarkLayout

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
HORIZONTAL            | La disposition du filigrane est horizontale
RECOUVREMENT            | La disposition du filigrane est diagonale

Disposition des filigranes.
  
### <a name="contentmarkalignment-enum"></a>Énumération ContentMarkAlignment

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
LEFT            | Le marquage de contenu est aligné à gauche
RIGHT            | Le marquage de contenu est aligné à droite
DE DONNÉES            | Le marquage du contenu est centré

Alignement des marques de contenu (en-tête de contenu ou pied de page de contenu).
  
### <a name="assignmentmethod-enum"></a>Énumération assignation

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
HIVER            | La méthode d’affectation d' [étiquette](class_mip_label.md) est standard
AUTORISÉE            | La méthode d’affectation d' [étiquette](class_mip_label.md) est privilégiée
AUTO            | La méthode d’affectation d' [étiquette](class_mip_label.md) est automatique

Méthode d’assignation de l’étiquette sur le document. Indique si l’assignation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’opération privilégiée (l’équivalent d’une opération d’administrateur).
  
### <a name="actionsource-enum"></a>Énumération ActionSource

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
MANUELLE            | Sélectionné manuellement par l’utilisateur
AUTOMATIQUE            | Défini par les conditions de la stratégie
RECOMMANDATIONS            | Défini par l’utilisateur après que l’étiquette a été recommandée par les conditions de la stratégie
DEFAULT            | Défini par défaut dans la stratégie

Définit ce qui a déclenché l’événement SetLabel
  
### <a name="datastate-enum"></a>Énumération DataState

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
REST            | Données inactives stockées physiquement dans les bases de données/fichiers/entrepôts
FILMS            | Les données qui traversent un réseau ou qui résident temporairement dans la mémoire de l’ordinateur à lire ou à mettre à jour
FAITES            | Données actives sous modification constante stockées physiquement dans les bases de données/fichiers/entrepôts, etc.

Définit l’état des données sur lequel l’application agit.
  
### <a name="contentformat-enum"></a>Énumération ContentFormat

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
DEFAULT            | Le format du contenu est le format de fichier standard
E-MAIL            | Le format du contenu est un format d’e-mail

Format du contenu.
  
### <a name="consent-enum"></a>Énumération de consentement

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
AcceptAlways            | Consentement, et se souvenir de cette décision
Accepter            | Consentement, une seule fois
Rejeter            | Ne pas donner son consentement

Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
  
### <a name="cachestoragetype-enum"></a>Énumération CacheStorageType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
InMemory            | Dans le stockage en mémoire
OnDisk            | Sur le stockage sur disque
OnDiskEncrypted            | Sur le stockage sur disque avec chiffrement (si pris en charge par la plateforme)

Type de stockage pour les caches.
  
### <a name="errortype-enum"></a>ErrorType (énumération)

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | L’appelant a passée une entrée incorrecte.
FILE_IO_ERROR            | Erreur E/S de fichier générale.
NETWORK_ERROR            | Problèmes généraux liés au réseau; par exemple, service inaccessible.
TRANSIENT_NETWORK_ERROR            | Problèmes réseau temporaires; par exemple, passerelle incorrecte.
INTERNAL_ERROR            | Erreurs internes inattendues.
JUSTIFICATION_REQUIRED            | Une justification doit être fournie pour effectuer l’action sur le fichier.
NOT_SUPPORTED_OPERATION            | L’opération demandée n’est pas encore prise en charge.
PRIVILEGED_REQUIRED            | Impossible de remplacer l’étiquette privilégiée lorsque la méthode de nouvelle étiquette est standard.
ACCESS_DENIED            | L’utilisateur n’a pas pu accéder aux services.
CONSENT_DENIED            | Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
POLICY_SYNC_ERROR            | Une tentative de synchronisation des données de stratégie a échoué.
NO_PERMISSIONS            | L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué
NO_AUTH_TOKEN            | L’utilisateur n’a pas pu accéder au contenu en raison d’un jeton d’authentification vide.
DISABLED_SERVICE            | L’utilisateur n’a pas pu accéder au contenu en raison de la désactivation du service
PROXY_AUTH_ERROR            | Échec de l’authentification du proxy.
NO_POLICY            | Aucune stratégie n’est configurée pour l’utilisateur/locataire
OPERATION_CANCELLED            | Opération annulée
ADHOC_PROTECTION_REQUIRED            | La protection ad hoc doit être configurée pour terminer l’action sur le fichier
DEPRECATED_API            | L’appelant a appelé une API déconseillée
TEMPLATE_NOT_FOUND            | L’ID de modèle n’est pas reconnu
LABEL_NOT_FOUND            | [Étiquette](class_mip_label.md) L’ID n’est pas reconnu
LABEL_DISABLED            | L' [étiquette](class_mip_label.md) est désactivée ou inactive
  
### <a name="inspectortype-enum"></a>Énumération InspectorType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Inconnu            | Inspecteur de fichier inconnu.
Fragment            | Inspecteur de fichier de style MSG, basé sur rpmsg/MSG.

Type d’inspecteur en corrélation avec les types de fichiers pris en charge.
  
### <a name="bodytype-enum"></a>Énumération BodyType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
UNKNOWN            | Type de corps inconnu
TXT            | Type de corps de style de texte, encodage retourné comme UTF8
HTML            | Type de corps de style HTML, l’encodage est retourné comme UTF8
RTF            | Type de corps de style RTF, format binaire

Énumérateur de type de corps.
  
### <a name="flightingfeature-enum"></a>Énumération FlightingFeature

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | S’appuyer sur un appel HTTP distinct pour déterminer les points de terminaison de service RMS
AuthInfoCache            | Mettez en cache les défis OAuth2 par domaine/locataire pour réduire les réponses 401 inutiles. Désactiver pour les applications/services qui gèrent leur propre authentification HTTP (par exemple, SPO)
LinuxEncryptedCache            | Activer la mise en cache chiffrée pour les plateformes Linux (veuillez lire les conditions préalables pour cette fonctionnalité)

Définit de nouvelles fonctionnalités par nom.
  
### <a name="httprequesttype-enum"></a>Énumération HttpRequestType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Obtenir            | GET
Post            | PUBLIER

Type de requête HTTP.
  
### <a name="loglevel-enum"></a>Énumération LogLevel

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Warning            | 
Error            | 

Différents niveaux de journalisation utilisés dans le SDK MIP.
  
### <a name="protectionhandlercreationoptions-enum"></a>Énumération ProtectionHandlerCreationOptions

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Aucun            | Aucun
OfflineOnly            | Ne pas autoriser les opérations d’interface utilisateur et de réseau
AllowAuditedExtraction            | Le contenu peut être ouvert dans une application non compatible avec le SDK de protection
PreferDeprecatedAlgorithms            | Utiliser des algorithmes de chiffrement (ECB) déconseillés pour la compatibilité descendante

Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.

> Déconseillé Cette énumération sera bientôt dépréciée lorsque CreateProtectionHandlerFromDescriptor et CreateProtectionHandlerFromPublishingLicense seront supprimés
  
### <a name="protectiontype-enum"></a>Énumération ProtectionType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
TemplateBased            | Handle créé à partir d’un modèle
Personnalisé            | Handle créé ad hoc

Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
  
### <a name="actiontype-enum"></a>ActionType (énumération)

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

Différents types d’actions. CUSTOM est le type d’action générique. Les autres types d’actions correspondent à une action spécifique avec une signification particulière.
  
### <a name="labelstate-enum"></a>Énumération LabelState

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
NoChange            | 
Supprimer            | 
Mettre à jour            | 
  
### <a name="actiondatatype-enum"></a>Énumération ActionDataType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Personnalisé            | 
Protection            | 
ContentMarking            | 
AddWatermark            | 
Etiquette            | 
  
### <a name="conditiondatatype-enum"></a>Énumération ConditionDataType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Default            | 
Sensibilité            | 
  
### <a name="contentmarkplacement-enum"></a>Énumération ContentMarkPlacement

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Header            | 
Pied            | 
  
### <a name="labelactiondatatype-enum"></a>Énumération LabelActionDataType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Recommander            | 
Appliquer            | 
  
### <a name="protectionactiontype-enum"></a>Énumération ProtectionActionType

Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Personnalisé            | 
Modèle            | 
DoNotForward            | 
Planifié            | 
DoNotForwardWithPrompt            | 
Hyok            | 
PredefinedTemplate            | 
RemoveProtection            | 
  


## <a name="structures"></a>Structures 

### <a name="mipapplicationinfo"></a>mip::ApplicationInfo 
Struct qui inclut des informations spécifiques à l’application.
  
#### <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificateur d’application tel qu’il est défini dans le portail AAD, (doit être un GUID sans crochets).
public std::string applicationName  |  Nom de l’application, (doit uniquement containValid le caractère ASCII en excluant «;»)
public std::string applicationVersion  |  Version de l’application utilisée, (doit uniquement containValid le caractère ASCII en excluant'; ')
  
#### <a name="members"></a>Membres
  
##### <a name="applicationid-struct-member"></a>applicationId, membre de struct
Identificateur d’application tel qu’il est défini dans le portail AAD, (doit être un GUID sans crochets).
  
##### <a name="applicationname-struct-member"></a>applicationName, membre struct
Nom de l’application, (doit uniquement containValid le caractère ASCII en excluant «;»)
  
##### <a name="applicationversion-struct-member"></a>applicationVersion, membre de struct
Version de l’application utilisée, (doit uniquement containValid le caractère ASCII en excluant'; ')

### <a name="miptelemetryconfiguration"></a>MIP:: TelemetryConfiguration 
Paramètres de télémétrie personnalisés (rarement utilisés)
  
#### <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std:: String hostNameOverride  |  Nom de l’instance de télémétrie de l’hôte. S’il n’est pas défini, MIP agit comme son propre hôte.
public std:: String libraryNameOverride  |  Nom de fichier de la bibliothèque de télémétrie (DLL) de remplacement.
public std:: shared_ptr\<HttpDelegate\> httpDelegateOverride  |  Si cette valeur est définie, la gestion HTTP sera gérée par cette instance
public std:: shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Si cette valeur est définie, la gestion des tâches Async sera gérée par cette instance
public bool isNetworkDetectionEnabled  |  Si cette valeur est définie, le composant de télémétrie effectue un test ping de l’état du réseau sur le thread
public bool isLocalCachingEnabled  |  Si cette valeur est définie, le composant de télémétrie utilisera la mise en cache sur disque
public bool isTelemetryOptedOut  |  Si cette valeur est définie, seules les données de télémétrie des données de service nécessaires seront envoyées
  
#### <a name="members"></a>Membres
  
##### <a name="hostnameoverride-struct-member"></a>hostNameOverride, membre de struct
Nom de l’instance de télémétrie de l’hôte. S’il n’est pas défini, MIP agit comme son propre hôte.
  
##### <a name="librarynameoverride-struct-member"></a>libraryNameOverride, membre de struct
Nom de fichier de la bibliothèque de télémétrie (DLL) de remplacement.
  
##### <a name="httpdelegate"></a>HttpDelegate
Si cette valeur est définie, la gestion HTTP sera gérée par cette instance
  
##### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
Si cette valeur est définie, la gestion des tâches Async sera gérée par cette instance
  
##### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie effectue un test ping de l’état du réseau sur le thread
  
##### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie utilisera la mise en cache sur disque
  
##### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut, membre de struct
Si cette valeur est définie, seules les données de télémétrie des données de service nécessaires seront envoyées