# <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 enum Consent       |  Représente la décision d’un utilisateur de donner son consentement pour se connecter à un point de terminaison de service.
 struct ApplicationInfo  |  ID d’application tel que défini dans le portail Azure AD.
**mip** |
 enum ActionType       |  Différents types d’actions.
 enum ErrorType       | _Pas encore documenté._
 enum LogLevel       |  Différents niveaux de journal utilisés dans le SDK MIP.
 enum ProtectionHandlerCreationOptions       |  Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.
 enum ProtectionType       |  Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)

  
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
  
Les valeurs **ActionType** prennent en charge les opérateurs suivants :

* Opérateur Or (|) pour le type [Action](class_mip_action.md) enum.  
* Opérateur And (&) pour le type [Action](class_mip_action.md) enum.  
* Opérateur Xor (^) pour le type [Action](class_mip_action.md) enum.  

### <a name="errortype"></a>ErrorType

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | L’appelant a passée une entrée incorrecte.
FILE_IO_ERROR            | Erreur E/S de fichier générale.
NETWORK_ERROR            | Problèmes de réseau d’ordre général ; par exemple, service inaccessible.
INTERNAL_ERROR            | Erreurs internes inattendues. Par exemple, dans le protocole client-serveur (réponse inattendue reçue).
JUSTIFICATION_REQUIRED            | Une justification doit être fournie pour effectuer l’action sur le fichier.
NOT_SUPPORTED_OPERATION            | L’opération demandée n’est pas encore prise en charge.
PRIVILEGED_REQUIRED            | Impossible de remplacer l’étiquette privilégiée lorsque la méthode de nouvelle étiquette est standard.
ACCESS_DENIED            | L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué, etc.
  
### <a name="loglevel"></a>LogLevel

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Trace            | 
Informations            | 
Avertissement            | 
Erreur            | 
Différents niveaux de journal utilisés dans le SDK MIP.
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Aucune            | Aucune
OfflineOnly            | Ne pas autoriser les opérations réseau et de l’interface utilisateur.
AllowAuditedExtraction            | Le contenu peut être ouvert dans une application non compatible avec le SDK de protection
PreferDeprecatedAlgorithms            | Utiliser des algorithmes de chiffrement (ECB) déconseillés pour la compatibilité descendante
Indicateurs de bits qui déterminent le comportement de création de stratégie supplémentaire.
  
### <a name="protectiontype"></a>ProtectionType

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
TemplateBased            | Handle créé à partir d’un modèle
Personnalisé            | Handle créé ad hoc
Décrit si protection est basée sur un modèle ou si elle est ad-hoc (personnalisée)
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Opérateur OR au niveau du bit ProtectionHandlerCreationOptions.

Paramètres : 
 
* **a** : valeur gauche 

* **b** : valeur droite
  
**Retourne** : OR au niveau du bit des paramètres
  


## <a name="structures"></a>Structures

### <a name="applicationinfo"></a>ApplicationInfo 
Identificateur d’application tel que défini dans le portail Azure AD.
  
 Champs                        | Descriptions                                
--------------------------------|---------------------------------------------
 public std::string applicationId  | ID d’application dans le portail Azure AD.
 public std::string friendlyName  | Nom convivial de l’application, comme spécifié dans le portail.
  
