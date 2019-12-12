---
title: SDK MIP pour C++ les structs et les enums de référence
description: Documentation de référence sur C++ les structs et les enums du kit de développement logiciel (SDK) MIP.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: a6e5fae2296fb6f966f5f7fb6b73facb867398a2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560449"
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
énumération LabelFilterType       |  Types de filtres d’étiquette, ensemble facultatif de propriétés qui peuvent être utilisées pour filtrer les étiquettes lors de l’appel des étiquettes de sensibilité de la liste.
enum Consent       |  Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
énumération CacheStorageType       |  Type de stockage pour les caches.
énumération PFileExtensionBehavior       |  Décrit le comportement des extensions PFile.
enum ErrorType       | Pas encore documenté.
énumération InspectorType       |  Type d’inspecteur en corrélation avec les types de fichiers pris en charge.
énumération BodyType       |  Énumérateur de type de corps.
énumération FlightingFeature       |  Définit de nouvelles fonctionnalités par nom.
enum HttpRequestType       |  Type de requête HTTP.
enum LogLevel       |  Différents niveaux de journalisation utilisés dans le SDK MIP.
enum ProtectionType       |  Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
enum ActionType       |  Différents types d’actions.
énumération LabelState       | Pas encore documenté.
énumération ActionDataType       | Pas encore documenté.
énumération ConditionDataType       | Pas encore documenté.
énumération ContentMarkPlacement       | Pas encore documenté.
énumération LabelActionDataType       | Pas encore documenté.
énumération ProtectionActionType       | Pas encore documenté.
MIP, struct :: ApplicationInfo  |  Struct qui inclut des informations spécifiques à l’application.
MIP, struct :: TelemetryConfiguration  |  Paramètres de télémétrie personnalisés (rarement utilisés)

### <a name="enumerations"></a>Énumérations

#### <a name="watermarklayout-enum"></a>Énumération WatermarkLayout
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
HORIZONTAL            | La disposition du filigrane est horizontale
RECOUVREMENT            | La disposition du filigrane est diagonale
Disposition des filigranes.
  
#### <a name="contentmarkalignment-enum"></a>Énumération ContentMarkAlignment
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
LEFT            | Le marquage de contenu est aligné à gauche
RIGHT            | Le marquage de contenu est aligné à droite
DE DONNÉES            | Le marquage du contenu est centré
Alignement des marques de contenu (en-tête de contenu ou pied de page de contenu).
  
#### <a name="assignmentmethod-enum"></a>Énumération assignation
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
STANDARD            | La méthode d’affectation d’étiquette est standard
AUTORISÉE            | La méthode d’affectation d’étiquette est privilégiée
AUTO            | La méthode d’affectation d’étiquette est automatique
Méthode d’assignation de l’étiquette sur le document. Indique si l’assignation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’opération privilégiée (l’équivalent d’une opération d’administrateur).
  
#### <a name="actionsource-enum"></a>Énumération ActionSource
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
MANUAL            | Sélectionné manuellement par l’utilisateur
AUTOMATIC            | Défini par les conditions de la stratégie
RECOMMANDATIONS            | Défini par l’utilisateur après que l’étiquette a été recommandée par les conditions de la stratégie
DEFAULT            | Défini par défaut dans la stratégie
définit ce qui a déclenché l’événement SetLabel
  
#### <a name="datastate-enum"></a>Énumération DataState
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
REST            | Données inactives stockées physiquement dans les bases de données/fichiers/entrepôts
FILMS            | Les données qui traversent un réseau ou qui résident temporairement dans la mémoire de l’ordinateur à lire ou à mettre à jour
USE            | Données actives sous modification constante stockées physiquement dans les bases de données/fichiers/entrepôts, etc.
Définit l’état des données sur lequel l’application agit.
  
#### <a name="contentformat-enum"></a>Énumération ContentFormat
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
DEFAULT            | Le format du contenu est le format de fichier standard
E-MAIL            | Le format du contenu est un format d’e-mail
Format du contenu.
  
#### <a name="labelfiltertype-enum"></a>Énumération LabelFilterType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
aucune.            | Désactiver la filtration d’étiquetage par défaut
Personnalisé            | Filtrer les étiquettes qui peuvent entraîner une protection personnalisée
TemplateProtection            | Les étiquettes de filtre qui peuvent entraîner la non-transfert
DoNotForwardProtection            | Filtrer les étiquettes qui peuvent entraîner la protection d’un modèle
AdhocProtection            | Filtrer les étiquettes qui peuvent entraîner une protection ad hoc
HyokProtection            | Filtrer les étiquettes qui peuvent entraîner une protection hyok
PredefinedTemplate            | Filtrer les étiquettes qui peuvent entraîner une protection prédéfinie des modèles
Types de filtres d’étiquette, ensemble facultatif de propriétés qui peuvent être utilisées pour filtrer les étiquettes lors de l’appel des étiquettes de sensibilité de la liste.
  
#### <a name="consent-enum"></a>Énumération de consentement
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
AcceptAlways            | Consentement, et se souvenir de cette décision
Accepter            | Consentement, une seule fois
Rejeter            | Ne pas donner son consentement
Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
  
#### <a name="cachestoragetype-enum"></a>Énumération CacheStorageType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
InMemory            | Dans le stockage en mémoire
OnDisk            | Sur le stockage sur disque
OnDiskEncrypted            | Sur le stockage sur disque avec chiffrement (si pris en charge par la plateforme)
Type de stockage pour les caches.
  
#### <a name="pfileextensionbehavior-enum"></a>Énumération PFileExtensionBehavior
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Par défaut            | Les extensions deviendront le comportement par défaut du SDK
PFileSuffix            | Les extensions deviendront <EXT>. PFILE
PPrefix            | Les extensions deviendront P<EXT>
Décrit le comportement des extensions PFile.
  
#### <a name="errortype-enum"></a>ErrorType (énumération)
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | L’appelant a passée une entrée incorrecte.
FILE_IO_ERROR            | Erreur E/S de fichier générale.
NETWORK_ERROR            | Problèmes généraux liés au réseau ; par exemple, service inaccessible.
TRANSIENT_NETWORK_ERROR            | Problèmes réseau temporaires ; par exemple, passerelle incorrecte.
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
PROXY_AUTH_ERROR            | Échec de l'authentification du proxy.
NO_POLICY            | Aucune stratégie n’est configurée pour l’utilisateur/locataire
OPERATION_CANCELLED            | Opération annulée
ADHOC_PROTECTION_REQUIRED            | La protection ad hoc doit être configurée pour terminer l’action sur le fichier
DEPRECATED_API            | L’appelant a appelé une API déconseillée
TEMPLATE_NOT_FOUND            | L’ID de modèle n’est pas reconnu
LABEL_NOT_FOUND            | ID d’étiquette non reconnu
LABEL_DISABLED            | L’étiquette est désactivée ou inactive
  
#### <a name="inspectortype-enum"></a>Énumération InspectorType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Inconnu            | Inspecteur de fichier inconnu.
Fragment            | Inspecteur de fichier de style MSG, basé sur rpmsg/MSG.
Type d’inspecteur en corrélation avec les types de fichiers pris en charge.
  
#### <a name="bodytype-enum"></a>Énumération BodyType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
UNKNOWN            | Type de corps inconnu
TXT            | Type de corps de style de texte, encodage retourné comme UTF8
HTML            | Type de corps de style HTML, l’encodage est retourné comme UTF8
RTF            | Type de corps de style RTF, format binaire
Énumérateur de type de corps.
  
#### <a name="flightingfeature-enum"></a>Énumération FlightingFeature
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | S’appuyer sur un appel HTTP distinct pour déterminer les points de terminaison de service RMS
AuthInfoCache            | Mettez en cache les défis OAuth2 par domaine/locataire pour réduire les réponses 401 inutiles. Désactiver pour les applications/services qui gèrent leur propre authentification HTTP (comme SPO, Edge)
LinuxEncryptedCache            | Activer la mise en cache chiffrée pour les plateformes Linux (veuillez lire les conditions préalables pour cette fonctionnalité)
SingleDomainName            | Activez le nom d’entreprise unique pour la recherche DNS. par exemple, [https://corprights](https://corprights)
PolicyAuth            | Activez l’authentification HTTP automatique pour les requêtes envoyées au service de stratégie. Désactiver pour les applications/services qui gèrent leur propre authentification HTTP (comme SPO, Edge)
Définit de nouvelles fonctionnalités par nom.
  
#### <a name="httprequesttype-enum"></a>Énumération HttpRequestType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Obtenir            | GET
Post            | POST
Type de requête HTTP.
  
#### <a name="loglevel-enum"></a>Énumération LogLevel
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Trace            | 
Informations            | 
Avertissement            | 
Erreur            | 
Différents niveaux de journalisation utilisés dans le SDK MIP.
  
#### <a name="protectiontype-enum"></a>Énumération ProtectionType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
TemplateBased            | Handle créé à partir d’un modèle
Personnalisé            | Handle créé ad hoc
Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
  
#### <a name="actiontype-enum"></a>ActionType (énumération)
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
Différents types d’actions.
CUSTOM est le type d’action générique. Les autres types d’actions correspondent à une action spécifique avec une signification particulière.
  
#### <a name="labelstate-enum"></a>Énumération LabelState
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
NoChange            | 
Remove            | 
Mettre à jour/Mise à jour            | 
  
#### <a name="actiondatatype-enum"></a>Énumération ActionDataType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Personnalisé            | 
Protection            | 
ContentMarking            | 
AddWatermark            | 
Étiquette            | 
  
#### <a name="conditiondatatype-enum"></a>Énumération ConditionDataType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Par défaut            | 
Sensibilité            | 
  
#### <a name="contentmarkplacement-enum"></a>Énumération ContentMarkPlacement
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Header            | 
Pied de page            | 
  
#### <a name="labelactiondatatype-enum"></a>Énumération LabelActionDataType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Recommend            | 
Appliquer            | 
  
#### <a name="protectionactiontype-enum"></a>Énumération ProtectionActionType
 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Personnalisé            | 
Modèle            | 
DoNotForward            | 
Adhoc            | 
DoNotForwardWithPrompt            | 
Hyok            | 
PredefinedTemplate            | 
RemoveProtection            | 

### <a name="structures"></a>Structures

#### <a name="struct-mipapplicationinfo"></a>MIP, struct :: ApplicationInfo 
Struct qui inclut des informations spécifiques à l’application.
  
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificateur d’application tel qu’il est défini dans le portail AAD, (doit être un GUID sans crochets).
public std::string applicationName  |  Nom de l’application, (doit contenir uniquement des caractères ASCII valides, à l’exception de « ; »)
public std::string applicationVersion  |  Version de l’application utilisée, (ne doit contenir que des caractères ASCII valides, à l’exclusion de « ; »)
  

##### <a name="applicationid-struct-member"></a>applicationId, membre de struct
Identificateur d’application tel qu’il est défini dans le portail AAD, (doit être un GUID sans crochets).
  
##### <a name="applicationname-struct-member"></a>applicationName, membre struct
Nom de l’application, (doit contenir uniquement des caractères ASCII valides, à l’exception de « ; »)
  
##### <a name="applicationversion-struct-member"></a>applicationVersion, membre de struct
Version de l’application utilisée, (ne doit contenir que des caractères ASCII valides, à l’exclusion de « ; »)

#### <a name="struct-miptelemetryconfiguration"></a>MIP, struct :: TelemetryConfiguration 
Paramètres de télémétrie personnalisés (rarement utilisés)
  
Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String hostNameOverride  |  Nom de l’instance de télémétrie de l’hôte. S’il n’est pas défini, MIP agit comme son propre hôte.
public std :: String libraryNameOverride  |  Nom de fichier de la bibliothèque de télémétrie (DLL) de remplacement.
public std :: shared_ptr\<HttpDelegate\> httpDelegateOverride  |  Si cette valeur est définie, la gestion HTTP sera gérée par cette instance
public std :: shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Si cette valeur est définie, la gestion des tâches asynchrones sera gérée par cette instance, taskDispatcherDelegateOverides ne doit pas être partagée, car elle peut contenir des objets de télémétrie et empêcher sa sortie tant que taskDispatcher n’est pas libéré.
public bool isNetworkDetectionEnabled  |  Si cette valeur est définie, le composant de télémétrie effectue un test ping de l’état du réseau sur le thread
public bool isLocalCachingEnabled  |  Si cette valeur est définie, le composant de télémétrie utilisera la mise en cache sur disque
public bool isTraceLoggingEnabled  |  Si cette valeur est définie, le composant de télémétrie écrit les journaux d’avertissements et d’erreurs sur le disque
public bool isTelemetryOptedOut  |  Si cette valeur est définie, seules les données de télémétrie des données de service nécessaires seront envoyées
public bool isFastShutdownEnabled  |  Si cette valeur est définie, aucun événement ne sera chargé lors de l’arrêt, les événements d’audit seront téléchargés immédiatement lors de la journalisation
public std :: Map\<std :: String, std :: String\> customSettings  |  Paramètres de télémétrie personnalisés >
    
##### <a name="hostnameoverride-struct-member"></a>hostNameOverride, membre de struct
Nom de l’instance de télémétrie de l’hôte. S’il n’est pas défini, MIP agit comme son propre hôte.
  
##### <a name="librarynameoverride-struct-member"></a>libraryNameOverride, membre de struct
Nom de fichier de la bibliothèque de télémétrie (DLL) de remplacement.
  
##### <a name="httpdelegate"></a>HttpDelegate
Si cette valeur est définie, la gestion HTTP sera gérée par cette instance
  
##### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
Si cette valeur est définie, la gestion des tâches asynchrones sera gérée par cette instance, taskDispatcherDelegateOverides ne doit pas être partagée, car elle peut contenir des objets de télémétrie et empêcher sa sortie tant que taskDispatcher n’est pas libéré.
  
##### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie effectue un test ping de l’état du réseau sur le thread
  
##### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie utilisera la mise en cache sur disque
  
##### <a name="istraceloggingenabled-struct-member"></a>isTraceLoggingEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie écrit les journaux d’avertissements et d’erreurs sur le disque
  
##### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut, membre de struct
Si cette valeur est définie, seules les données de télémétrie des données de service nécessaires seront envoyées
  
##### <a name="isfastshutdownenabled-struct-member"></a>isFastShutdownEnabled, membre de struct
Si cette valeur est définie, aucun événement ne sera chargé lors de l’arrêt, les événements d’audit seront téléchargés immédiatement lors de la journalisation
  
##### <a name="customsettings-struct-member"></a>customSettings, membre de struct
Paramètres de télémétrie personnalisés >

## <a name="namespace-mipauditmetadatakeys"></a>espace de noms MIP :: auditmetadatakeys
  
### <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String Sender ()       |  Clés de métadonnées d’audit dans la représentation sous forme de chaîne.
public std :: String Recipients ()       | Pas encore documenté.
public std :: String LastModifiedBy ()       | Pas encore documenté.
public std :: String LastModifiedDate & ()       | Pas encore documenté.
  
### <a name="members"></a>Membres
  
#### <a name="sender-function"></a>Fonction d’expéditeur
Clés de métadonnées d’audit dans la représentation sous forme de chaîne.
  
#### <a name="recipients-function"></a>Fonction Recipients
_Pas encore documenté._

  
#### <a name="lastmodifiedby-function"></a>LastModifiedBy fonction)
_Pas encore documenté._

  
#### <a name="lastmodifieddate-function"></a>LastModifiedDate & fonction)
_Pas encore documenté._

## <a name="namespace-miprights"></a>espace de noms MIP :: Rights
  
### <a name="summary"></a>Table des matières
 
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string Owner()       |  Obtient un identificateur de chaîne pour un droit « propriétaire ».
public std::string View()       |  Obtient un identificateur de chaîne pour un droit « afficher ».
public std::string AuditedExtract()       |  Obtient un identificateur de chaîne pour un droit « extraction auditée ».
public std::string Edit()       |  Obtient un identificateur de chaîne pour un droit « modifier ».
public std::string Export()       |  Obtient un identificateur de chaîne pour un droit « exporter ».
public std::string Extract()       |  Obtient un identificateur de chaîne pour un droit « extraire ».
public std::string Print()       |  Obtient un identificateur de chaîne pour un droit « imprimer ».
public std::string Comment()       |  Obtient un identificateur de chaîne pour un droit « commentaire ».
public std::string Reply()       |  Obtient un identificateur de chaîne pour un droit « répondre ».
public std::string ReplyAll()       |  Obtient un identificateur de chaîne pour un droit « répondre à tous ».
public std::string Forward()       |  Obtient un identificateur de chaîne pour un droit « transférer ».
public std::vector\<std::string\> EmailRights()       |  Obtient une liste de droits qui s’appliquent aux e-mails.
public std::vector\<std::string\> EditableDocumentRights()       |  Obtient une liste de droits qui s’appliquent aux documents.
public std::vector\<std::string\> CommonRights()       |  Obtient une liste des droits qui s’appliquent dans tous les scénarios.
  
### <a name="members"></a>Membres
  
#### <a name="owner-function"></a>Fonction owner
Obtient un identificateur de chaîne pour un droit « propriétaire ».

  
**Renvoie** : identificateur de chaîne pour un droit « propriétaire »
  
#### <a name="view-function"></a>View, fonction
Obtient un identificateur de chaîne pour un droit « afficher ».

  
**Renvoie** : identificateur de chaîne pour un droit « afficher »
  
#### <a name="auditedextract-function"></a>AuditedExtract fonction)
Obtient un identificateur de chaîne pour un droit « extraction auditée ».

  
**Renvoie** : identificateur de chaîne pour un droit « extraction auditée »
  
#### <a name="edit-function"></a>Modifier la fonction
Obtient un identificateur de chaîne pour un droit « modifier ».

  
**Renvoie** : identificateur de chaîne pour droit « modifier »
  
#### <a name="export-function"></a>Fonction d’exportation
Obtient un identificateur de chaîne pour un droit « exporter ».

  
**Renvoie** : identificateur de chaîne de « export » vers la droite
  
#### <a name="extract-function"></a>fonction Extract
Obtient un identificateur de chaîne pour un droit « extraire ».

  
**Renvoie** : identificateur de chaîne pour un droit « extraire »
  
#### <a name="print-function"></a>Print, fonction
Obtient un identificateur de chaîne pour un droit « imprimer ».

  
**Renvoie** : identificateur de chaîne pour un droit « imprimer »
  
#### <a name="comment-function"></a>Fonction comment
Obtient un identificateur de chaîne pour un droit « commentaire ».

  
**Renvoie** : identificateur de chaîne pour un droit « commentaire »
  
#### <a name="reply-function"></a>Reply, fonction
Obtient un identificateur de chaîne pour un droit « répondre ».

  
**Renvoie** : identificateur de chaîne pour un droit « répondre »
  
#### <a name="replyall-function"></a>ReplyAll, fonction
Obtient un identificateur de chaîne pour un droit « répondre à tous ».

  
**Renvoie** : identificateur de chaîne pour un droit « répondre à tous »
  
#### <a name="forward-function"></a>Fonction Forward
Obtient un identificateur de chaîne pour un droit « transférer ».

  
**Renvoie** : identificateur de chaîne pour un droit « transférer »
  
#### <a name="emailrights-function"></a>EmailRights fonction)
Obtient une liste de droits qui s’appliquent aux e-mails.

  
**Renvoie** : une liste de droits qui s’appliquent aux e-mails
  
#### <a name="editabledocumentrights-function"></a>EditableDocumentRights fonction)
Obtient une liste de droits qui s’appliquent aux documents.

  
**Renvoie** : une liste de droits qui s’appliquent aux documents
  
#### <a name="commonrights-function"></a>CommonRights fonction)
Obtient une liste des droits qui s’appliquent dans tous les scénarios.

  
**Renvoie** : une liste des droits qui s’appliquent dans tous les scénarios

## <a name="namespace-miproles"></a>espace de noms MIP :: Roles
  
### <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  Obtient un identificateur de chaîne pour un rôle « observateur ».
public std::string Reviewer()       |  Obtient un identificateur de chaîne pour un rôle « réviseur ».
public std::string Author()       |  Obtient un identificateur de chaîne pour un rôle « auteur ».
public std::string CoOwner()       |  Obtient un identificateur de chaîne pour un rôle « copropriétaire ».
  
### <a name="members"></a>Membres
  
#### <a name="viewer-function"></a>Fonction de visionneuse
Obtient un identificateur de chaîne pour un rôle « observateur ».

  
**Renvoie** : identificateur de chaîne pour un rôle « observateur » Un observateur peut uniquement afficher le contenu. Il ne peut ni le modifier, ni le copier, ni l’imprimer.
  
#### <a name="reviewer-function"></a>Fonction de réviseur
Obtient un identificateur de chaîne pour un rôle « réviseur ».

  
**Renvoie** : identificateur de chaîne pour le rôle « réviseur » Un réviseur peut afficher et modifier le contenu. Ils ne peut ni le copier ni l’imprimer.
  
#### <a name="author-function"></a>Author, fonction
Obtient un identificateur de chaîne pour un rôle « auteur ».

  
**Renvoie** : identificateur de chaîne pour le rôle « auteur » Un auteur peut afficher, modifier, copier et imprimer le contenu.
  
#### <a name="coowner-function"></a>Copropriétaire, fonction
Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

  
**Renvoie** : identificateur de chaîne pour un rôle « copropriétaire » Un copropriétaire a toutes les autorisations

