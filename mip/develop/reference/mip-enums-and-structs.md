---
title: SDK MIP pour C++ les structs et les enums de référence
description: Documentation de référence sur C++ les structs et les enums du kit de développement logiciel (SDK) MIP.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2ee3c660a14df74f432870d364002cee86a5ce27
ms.sourcegitcommit: 2917e822a5d1b21bf465f2cb93cfe46937b1faa7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79405012"
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
énumération FeatureId       |  Définit de nouvelles fonctionnalités par nom.
énumération VariableTextMarkingType       |  différents champs dynamiques peuvent être définis dans le message texte de l’application : $ {Item. label} $ {Item.Name} $ {Item. Location} $ {User.Name} $ {User. principal} $ {Event. DateTime} les autres éléments ne sont toujours pas définis : le kit de développement logiciel (SDK) les remplace par les valeurs utilisant ces indicateurs de contrôle.
enum Consent       |  Réponse d’un utilisateur quand le consentement est demandé pour la connexion à un point de terminaison de service.
énumération CacheStorageType       |  Type de stockage pour les caches.
énumération PFileExtensionBehavior       |  Décrit le comportement des extensions PFile.
enum ErrorType       | _Pas encore documenté._
énumération InspectorType       |  Type d’inspecteur en corrélation avec les types de fichiers pris en charge.
énumération BodyType       |  Énumérateur de type de corps.
énumération FlightingFeature       |  Définit de nouvelles fonctionnalités par nom.
enum HttpRequestType       |  Type de requête HTTP.
enum LogLevel       |  Différents niveaux de journalisation utilisés dans le SDK MIP.
enum ProtectionType       |  Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
enum ActionType       |  Différents types d’actions.
énumération LabelState       | _Pas encore documenté._
énumération ActionDataType       | _Pas encore documenté._
énumération ConditionDataType       | _Pas encore documenté._
énumération ContentMarkPlacement       | _Pas encore documenté._
énumération LabelActionDataType       | _Pas encore documenté._
énumération ProtectionActionType       | _Pas encore documenté._
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
CENTER            | Le marquage du contenu est centré

Alignement des marques de contenu (en-tête de contenu ou pied de page de contenu).
  
#### <a name="assignmentmethod-enum"></a>Énumération assignation
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
HIVER            | La méthode d’affectation d’étiquette est standard
AUTORISÉE            | La méthode d’affectation d’étiquette est privilégiée
Auto            | La méthode d’affectation d’étiquette est automatique

Méthode d’assignation de l’étiquette sur le document. Indique si l’assignation de l’étiquette a été effectuée automatiquement, standard ou en tant qu’opération privilégiée (l’équivalent d’une opération d’administrateur).
  
#### <a name="actionsource-enum"></a>Énumération ActionSource
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Manuelle            | Sélectionné manuellement par l’utilisateur
Automatique            | Défini par les conditions de la stratégie
RECOMMANDATIONS            | Défini par l’utilisateur après que l’étiquette a été recommandée par les conditions de la stratégie
VALEURS            | Défini par défaut dans la stratégie

définit ce qui a déclenché l’événement SetLabel
  
#### <a name="datastate-enum"></a>Énumération DataState
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
REST            | Données inactives stockées physiquement dans les bases de données/fichiers/entrepôts
FILMS            | Les données qui traversent un réseau ou qui résident temporairement dans la mémoire de l’ordinateur à lire ou à mettre à jour
FAITES            | Données actives sous modification constante stockées physiquement dans les bases de données/fichiers/entrepôts, etc.

Définit l’état des données sur lequel l’application agit.
  
#### <a name="contentformat-enum"></a>Énumération ContentFormat
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
VALEURS            | Le format du contenu est le format de fichier standard
Messagerie            | Le format du contenu est un format d’e-mail

Format du contenu.
  
#### <a name="labelfiltertype-enum"></a>Énumération LabelFilterType
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Aucune            | Désactiver la filtration d’étiquetage par défaut
CustomProtection            | Filtrer les étiquettes qui peuvent entraîner une protection personnalisée
TemplateProtection            | Les étiquettes de filtre qui peuvent entraîner la non-transfert
DoNotForwardProtection            | Filtrer les étiquettes qui peuvent entraîner la protection d’un modèle
AdhocProtection            | Filtrer les étiquettes qui peuvent entraîner une protection ad hoc
HyokProtection            | Filtrer les étiquettes qui peuvent entraîner une protection hyok
PredefinedTemplateProtection            | Filtrer les étiquettes qui peuvent entraîner une protection prédéfinie des modèles
DoubleKeyProtection            | Les étiquettes de filtre qui peuvent entraîner une protection nécessitant une clé double peuvent être des modèles, ad hoc, FND

Types de filtres d’étiquette, ensemble facultatif de propriétés qui peuvent être utilisées pour filtrer les étiquettes lors de l’appel des étiquettes de sensibilité de la liste.
  
#### <a name="featureid-enum"></a>Énumération FeatureId
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
EncryptOnly            | Vérifier si le serveur prend en charge la fonctionnalité EncryptOnly

Définit de nouvelles fonctionnalités par nom.
  
#### <a name="variabletextmarkingtype-enum"></a>Énumération VariableTextMarkingType
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Default            | Les marques connues sont converties un marquage inconnu est supprimé
Passage            | Les marques connues sont converties le marquage inconnu est passé
Aucune            | Toutes les marques sont transmises

différents champs dynamiques peuvent être définis dans le message texte de l’application : $ {Item. label} $ {Item.Name} $ {Item. Location} $ {User.Name} $ {User. principal} $ {Event. DateTime} les autres éléments ne sont toujours pas définis : le kit de développement logiciel (SDK) les remplace par les valeurs utilisant ces indicateurs de contrôle.
  
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
Mémoire            | Dans le stockage en mémoire
OnDisk            | Sur le stockage sur disque
OnDiskEncrypted            | Sur le stockage sur disque avec chiffrement (si pris en charge par la plateforme)

Type de stockage pour les caches.
  
#### <a name="pfileextensionbehavior-enum"></a>Énumération PFileExtensionBehavior
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Default            | Les extensions deviendront le comportement par défaut du SDK
PFileSuffix            | Les extensions deviendront <EXT>. PFILE
PPrefix            | Les extensions deviendront P<EXT>

Décrit le comportement des extensions PFile.
  
#### <a name="errortype-enum"></a>ErrorType (énumération)
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | L’appelant a passée une entrée incorrecte.
INSUFFICIENT_BUFFER_ERROR            | L’appelant a passé un tampon trop petit.
FILE_IO_ERROR            | Erreur E/S de fichier générale.
NETWORK_ERROR            | Problèmes généraux liés au réseau ; par exemple, service inaccessible.
INTERNAL_ERROR            | Erreurs internes inattendues.
JUSTIFICATION_REQUIRED            | Une justification doit être fournie pour effectuer l’action sur le fichier.
NOT_SUPPORTED_OPERATION            | L’opération demandée n’est pas encore prise en charge.
PRIVILEGED_REQUIRED            | Impossible de remplacer l’étiquette privilégiée lorsque la méthode de nouvelle étiquette est standard.
ACCESS_DENIED            | L’utilisateur n’a pas pu accéder aux services.
CONSENT_DENIED            | Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
NO_PERMISSIONS            | L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué
NO_AUTH_TOKEN            | L’utilisateur n’a pas pu accéder au contenu en raison d’un jeton d’authentification vide.
DISABLED_SERVICE            | L’utilisateur n’a pas pu accéder au contenu en raison de la désactivation du service
PROXY_AUTH_ERROR            | Échec de l’authentification du proxy.
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
Inconnu.            | Inspecteur de fichier inconnu.
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
UrlRedirectCache            | Redirections d’URL de cache pour réduire le nombre d’opérations HTTP
Prélicence            | Activer la vérification de l’API de pré-licence
DoubleKey            | Activer la fonctionnalité de protection double clé pour utiliser une clé de client pour le chiffrement
VariablePolicyTtl            | Activer la durée de vie de la stratégie de variable, désactivation de la stratégie infinie
VariableTextMarking            | Activer le marquage de texte de variable

Définit de nouvelles fonctionnalités par nom.
  
#### <a name="httprequesttype-enum"></a>Énumération HttpRequestType
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Télécharger            | GET
Post            | POST

Type de requête HTTP.
  
#### <a name="loglevel-enum"></a>Énumération LogLevel
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Trace            | 
Informations            | 
Avertissement            | 
Error            | 

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
PROTECT_ADHOC_DK            | Type d’action Protéger par stratégie ad hoc.
PROTECT_BY_TEMPLATE_DK            | Type d’action Protéger par modèle.
PROTECT_DO_NOT_FORWARD_DK            | Type d’action Protéger en n’effectuant pas de transfert.

Différents types d’actions. CUSTOM est le type d’action générique. Les autres types d’actions correspondent à une action spécifique avec une signification particulière.
  
#### <a name="labelstate-enum"></a>Énumération LabelState
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
NoChange            | 
Supprimer            | 
Update            | 
  
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
Default            | 
Sensibilité            | 
  
#### <a name="contentmarkplacement-enum"></a>Énumération ContentMarkPlacement
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
En-tête            | 
Pied de page            | 
  
#### <a name="labelactiondatatype-enum"></a>Énumération LabelActionDataType
Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Recommander            | 
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
