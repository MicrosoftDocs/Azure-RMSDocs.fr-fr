---
title: Classes
description: Fonctions
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: 73c56e5a5e2facf31eeadd59b36197dea8bbecc2
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563703"
---
# <a name="functions-c"></a>Fonctions (C++) 

## <a name="namespace-mip"></a>Espace de noms MIP

| Fonctions par portée d’espace de noms   | Descriptions                                |
|--------------------------------|---------------------------------------------|
public std :: String GetAssignmentMethodString (méthode assignation)       |  Convertit l’énumération assignation en Description de chaîne.
public static std :: String GetActionSourceString (ActionSource actionSource)       |  Obtient le nom de la source de l’action.
public static std :: String GetDataStateString (MIP ::D ataState State)       |  Obtient le nom de l’état du contenu.
public const std::string& GetCustomSettingPolicyDataName()       |  Nom du paramètre pour spécifier explicitement les données de stratégie.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.
public const std :: String& GetCustomSettingSensitivityTypesDataName ()       |  Nom du paramètre pour spécifier explicitement les données de sensibilité.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.
public const std :: String& GetCustomSettingSensitivityTypesDataFile ()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès du fichier de données des types de sensibilité.
public const std :: String& GetCustomSettingLabelCustomPropertiesSyncEnabled ()       |  Nom du paramètre qui autorise l’activation de l’étiquette par des propriétés personnalisées et des propriétés personnalisées par des fonctionnalités d’étiquette.
public const std :: String& GetCustomSettingPolicyTtlDays ()       |  Le nom du paramètre qui active la durée de vie de la stratégie de remplacement en jours est par défaut de 30 jours. Les valeurs doivent être définies en tant qu’entiers de chaîne i < 0 signifie une durée de vie infinie.
public const std :: String& GetCustomSettingSensitivityPolicyTtlDays ()       |  Le nom du paramètre qui permet de remplacer la durée de vie de la stratégie de sensibilité en jours est par défaut de 30 jours. Les valeurs doivent être définies en tant qu’entiers de chaîne i < 0 signifie une durée de vie infinie.
public const std :: map \<FlightingFeature, bool\>& GetDefaultFeatureSettings ()       |  Obtient une valeur indiquant si une fonctionnalité est activée par défaut.
public MIP_API std :: shared_ptr \<mip::Stream\> CreateStreamFromStdStream (const std :: shared_ptr \<std::istream\>& stdIStream)       |  Crée un Flux à partir d’un a std::istream.
public MIP_API std :: shared_ptr \<mip::Stream\> CreateStreamFromStdStream (const std :: shared_ptr \<std::ostream\>& stdOStream)       |  Crée un Flux à partir d’un a std::ostream.
public MIP_API std :: shared_ptr \<mip::Stream\> CreateStreamFromStdStream (const std :: shared_ptr \<std::iostream\>& stdIOStream)       |  Crée un Flux à partir d’un a std::iostream.
public MIP_API std :: shared_ptr \<mip::Stream\> CreateStreamFromBuffer (uint8_t * buffer, const int64_t Size)       |  Crée un Flux à partir d’une mémoire tampon.
public MIP_API std :: Vector \<uint8_t\> readFromStream (const std :: shared_ptr \<mip::Stream\>& flux)       |  Lit tous les octets du flux.
& d’opérateur ActionType public (ActionType a, ActionType b)       |  Opérateur and (&) pour l’énumération de type d’action.
opérateur ActionType public ^ (ActionType a, ActionType b)       |  Opérateur Xor (^) pour le type Action enum.

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString fonction)
Convertit l’énumération assignation en Description de chaîne.

Paramètres :  
* **méthode**: méthode d’assignation. 


**Retourne**: description de chaîne de la méthode d’assignation.
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString fonction)
Obtient le nom de la source de l’action.

Paramètres :  
* **actionSource**: source de l’action. 

**Retourne**: une représentation sous forme de chaîne de la source de l’action.
  
### <a name="getdatastatestring-function"></a>GetDataStateString fonction)
Obtient le nom de l’état du contenu.

Paramètres :  
* **actionSource**: état du contenu sur lequel le travail est effectué. 



  
**Retourne**: une représentation sous forme de chaîne de l’état du contenu.
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName fonction)
Nom du paramètre pour spécifier explicitement les données de stratégie.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName fonction)
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName fonction)
Nom du paramètre pour spécifier explicitement les données de sensibilité.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile fonction)
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile fonction)
Nom du paramètre pour spécifier explicitement le chemin d’accès du fichier de données des types de sensibilité.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettinglabelcustompropertiessyncenabled-function"></a>GetCustomSettingLabelCustomPropertiesSyncEnabled fonction)
Nom du paramètre qui autorise l’activation de l’étiquette par des propriétés personnalisées et des propriétés personnalisées par des fonctionnalités d’étiquette.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingpolicyttldays-function"></a>GetCustomSettingPolicyTtlDays fonction)
Le nom du paramètre qui active la durée de vie de la stratégie de remplacement en jours est par défaut de 30 jours. Les valeurs doivent être définies en tant qu’entiers de chaîne i < 0 signifie une durée de vie infinie.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingsensitivitypolicyttldays-function"></a>GetCustomSettingSensitivityPolicyTtlDays fonction)
Le nom du paramètre qui permet de remplacer la durée de vie de la stratégie de sensibilité en jours est par défaut de 30 jours. Les valeurs doivent être définies en tant qu’entiers de chaîne i < 0 signifie une durée de vie infinie.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getdefaultfeaturesettings-function"></a>GetDefaultFeatureSettings fonction)
Obtient une valeur indiquant si une fonctionnalité est activée par défaut.

  
**Retourne**: état par défaut des fonctionnalités de vol
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream fonction)
Crée un Flux à partir d’un a std::istream.

Paramètres :  
* **stdIStream** : sauvegarde std::istream



  
**Retourne**: flux d’encapsulation d’un std :: IStream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream fonction)
Crée un Flux à partir d’un a std::ostream.

Paramètres :  
* **stdIStream** : sauvegarde std::ostream



  
**Retourne**: flux d’encapsulation d’un std :: ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream fonction)
Crée un Flux à partir d’un a std::iostream.

Paramètres :  
* **stdIOStream** : sauvegarde std::iostream



  
**Retourne**: flux d’encapsulation d’un std :: iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer fonction)
Crée un Flux à partir d’une mémoire tampon.

Paramètres :  
* **buffer**: pointeur vers une mémoire tampon



  
**Renvoie** : taille de mémoire tampon
  
### <a name="readfromstream-function"></a>ReadFromStream fonction)
Lit tous les octets du flux.

Paramètres :  
* **pointeur**: vers un flux.



  
**Retourne**: un vecteur d’octets.
  
### <a name="operator-function"></a>opérateur | fonctionnalités
Opérateur Or (|) pour le type Action enum.
  
### <a name="operator-function"></a>fonction& Operator
Opérateur and (&) pour l’énumération de type d’action.
  
### <a name="operator-function"></a>fonction operator ^
Opérateur Xor (^) pour le type Action enum.

## <a name="namespace-mipauditmetadatakeys"></a>espace de noms MIP :: auditmetadatakeys

Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String Sender ()       |  Clés de métadonnées d’audit dans la représentation sous forme de chaîne.
public std :: String Recipients ()       | _Pas encore documenté._
public std :: String LastModifiedBy ()       | _Pas encore documenté._
public std :: String LastModifiedDate & ()       | _Pas encore documenté._
  
### <a name="sender-function"></a>Fonction d’expéditeur
Clés de métadonnées d’audit dans la représentation sous forme de chaîne.
  
### <a name="recipients-function"></a>Fonction Recipients
_Pas encore documenté._

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy fonction)
_Pas encore documenté._

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate & fonction)
_Pas encore documenté._


## <a name="namespace-miprights"></a>joint `mip::rights` 
  
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
public std :: Vector \<std::string\> EmailRights ()       |  Obtient une liste de droits qui s’appliquent aux e-mails.
public std :: Vector \<std::string\> EditableDocumentRights ()       |  Obtient une liste de droits qui s’appliquent aux documents.
public std :: Vector \<std::string\> CommonRights ()       |  Obtient une liste des droits qui s’appliquent dans tous les scénarios.
  
### <a name="owner-function"></a>Fonction owner
Obtient un identificateur de chaîne pour un droit « propriétaire ».

  
**Renvoie** : identificateur de chaîne pour un droit « propriétaire »
  
### <a name="view-function"></a>View, fonction
Obtient un identificateur de chaîne pour un droit « afficher ».

  
**Renvoie** : identificateur de chaîne pour un droit « afficher »
  
### <a name="auditedextract-function"></a>AuditedExtract fonction)
Obtient un identificateur de chaîne pour un droit « extraction auditée ».

  
**Renvoie** : identificateur de chaîne pour un droit « extraction auditée »
  
### <a name="edit-function"></a>Modifier la fonction
Obtient un identificateur de chaîne pour un droit « modifier ».

  
**Renvoie** : identificateur de chaîne pour droit « modifier »
  
### <a name="export-function"></a>Fonction d’exportation
Obtient un identificateur de chaîne pour un droit « exporter ».

  
**Renvoie** : identificateur de chaîne de « export » vers la droite
  
### <a name="extract-function"></a>Extraire une fonction
Obtient un identificateur de chaîne pour un droit « extraire ».

  
**Renvoie** : identificateur de chaîne pour un droit « extraire »
  
### <a name="print-function"></a>Print, fonction
Obtient un identificateur de chaîne pour un droit « imprimer ».

  
**Renvoie** : identificateur de chaîne pour un droit « imprimer »
  
### <a name="comment-function"></a>Fonction comment
Obtient un identificateur de chaîne pour un droit « commentaire ».

  
**Renvoie** : identificateur de chaîne pour un droit « commentaire »
  
### <a name="reply-function"></a>Reply, fonction
Obtient un identificateur de chaîne pour un droit « répondre ».

  
**Renvoie** : identificateur de chaîne pour un droit « répondre »
  
### <a name="replyall-function"></a>ReplyAll, fonction
Obtient un identificateur de chaîne pour un droit « répondre à tous ».

  
**Renvoie** : identificateur de chaîne pour un droit « répondre à tous »
  
### <a name="forward-function"></a>Fonction Forward
Obtient un identificateur de chaîne pour un droit « transférer ».

  
**Renvoie** : identificateur de chaîne pour un droit « transférer »
  
### <a name="emailrights-function"></a>EmailRights fonction)
Obtient une liste de droits qui s’appliquent aux e-mails.

  
**Renvoie** : une liste de droits qui s’appliquent aux e-mails
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights fonction)
Obtient une liste de droits qui s’appliquent aux documents.

  
**Renvoie** : une liste de droits qui s’appliquent aux documents
  
### <a name="commonrights-function"></a>CommonRights fonction)
Obtient une liste des droits qui s’appliquent dans tous les scénarios.

  
**Renvoie** : une liste des droits qui s’appliquent dans tous les scénarios

## <a name="namespace-miproles"></a>joint `mip::roles` 
  
Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  Obtient un identificateur de chaîne pour un rôle « observateur ».
public std::string Reviewer()       |  Obtient un identificateur de chaîne pour un rôle « réviseur ».
public std::string Author()       |  Obtient un identificateur de chaîne pour un rôle « auteur ».
public std::string CoOwner()       |  Obtient un identificateur de chaîne pour un rôle « copropriétaire ».
  
### <a name="viewer-function"></a>Fonction de visionneuse
Obtient un identificateur de chaîne pour un rôle « observateur ».

  
**Renvoie** : identificateur de chaîne pour un rôle « observateur » Un observateur peut uniquement afficher le contenu. Il ne peut ni le modifier, ni le copier, ni l’imprimer.
  
### <a name="reviewer-function"></a>Fonction de réviseur
Obtient un identificateur de chaîne pour un rôle « réviseur ».

  
**Renvoie** : identificateur de chaîne pour le rôle « réviseur » Un réviseur peut afficher et modifier le contenu. Ils ne peut ni le copier ni l’imprimer.
  
### <a name="author-function"></a>Author, fonction
Obtient un identificateur de chaîne pour un rôle « auteur ».

  
**Renvoie** : identificateur de chaîne pour le rôle « auteur » Un auteur peut afficher, modifier, copier et imprimer le contenu.
  
### <a name="coowner-function"></a>Copropriétaire, fonction
Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

  
**Renvoie** : identificateur de chaîne pour un rôle « copropriétaire » Un copropriétaire a toutes les autorisations
