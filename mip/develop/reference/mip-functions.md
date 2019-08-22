---
title: Fonctions
description: Fonctions
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: 80d13de3778648c2e0230ac37c559b0ca1f62a07
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882795"
---
# <a name="functions"></a>Fonctions

## <a name="summary"></a>Récapitulatif 

### <a name="namespace-mip"></a>Espace de noms MIP
| Fonctions par portée d’espace de noms   | Descriptions                                |
|--------------------------------|---------------------------------------------|
public std:: String GetAssignmentMethodString (méthode assignation)       |  Convertit l’énumération assignation en Description de chaîne.
public static std:: String GetActionSourceString (ActionSource actionSource)       |  Obtient le nom de la source de l’action.
public static std:: String GetDataStateString (MIP::D ataState State)       |  Obtient le nom de l’état du contenu.
public const std::string& GetCustomSettingPolicyDataName()       |  Nom du paramètre pour spécifier explicitement les données de stratégie.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.
public const std::string& GetCustomSettingSensitivityTypesDataName()       |  Nom du paramètre pour spécifier explicitement les données de sensibilité.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.
public const std::string& GetCustomSettingSensitivityTypesDataFile()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès du fichier de données des types de sensibilité.
public const std:: String & GetCustomSettingLabelCustomPropertiesSyncEnabled ()       |  Nom du paramètre qui autorise l’activation de l’étiquette par des propriétés personnalisées et des propriétés personnalisées par des fonctionnalités d’étiquette.
public const std:: map\<FlightingFeature, bool\>& GetDefaultFeatureSettings ()       |  Obtient une valeur indiquant si une fonctionnalité est activée par défaut.
public MIP_API void _ _ cdecl _ ReleaseAllResources ()       |  Libère toutes les ressources (threads, etc.) avant l’arrêt.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: IStream\>& stdIStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: ostream\>& stdOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: iostream\>& stdIOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromBuffer (uint8_t * tampon, const int64_t taille)       |  Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.
public MIP_API std:: Vector\<uint8_t\> readFromStream (const std:: shared_ptr\<MIP:: streaming\>& Stream)       |  Lit tous les octets du flux.

### <a name="namespace-mipauditmetadatakeys"></a>Espace de noms MIP:: auditmetadatakeys
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std:: String Sender ()       |  Clés de métadonnées d’audit dans la représentation sous forme de chaîne.
public std:: String Recipients ()       | _Pas encore documenté._
public std:: String LastModifiedBy ()       | _Pas encore documenté._
public std:: String LastModifiedDate & ()       | _Pas encore documenté._


### <a name="namespace-miprights"></a>Espace de noms MIP:: Rights

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

### <a name="namespace-miproles"></a>Espace de noms MIP:: Roles

 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  Obtient un identificateur de chaîne pour un rôle « observateur ».
public std::string Reviewer()       |  Obtient un identificateur de chaîne pour un rôle « réviseur ».
public std::string Author()       |  Obtient un identificateur de chaîne pour un rôle « auteur ».
public std::string CoOwner()       |  Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

## <a name="namespace-mip"></a>Espace de noms MIP

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString fonction)
Convertit l’énumération assignation en Description de chaîne.

Paramètres :  
* **méthode**: méthode d’assignation. 



  
**Retourne**: Description de chaîne de la méthode d’affectation.
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString fonction)
Obtient le nom de la source de l’action.

Paramètres :  
* **actionSource**: Source de l’action. 



  
**Retourne**: Représentation sous forme de chaîne de la source de l’action.
  
### <a name="getdatastatestring-function"></a>GetDataStateString fonction)
Obtient le nom de l’état du contenu.

Paramètres :  
* **actionSource**: État du contenu sur lequel le travail est effectué. 



  
**Retourne**: Représentation sous forme de chaîne de l’état du contenu.
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName function
Nom du paramètre pour spécifier explicitement les données de stratégie.

  
**Retourne**: Clé de paramètres personnalisés.
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName function
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.

  
**Retourne**: Clé de paramètres personnalisés.
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName function
Nom du paramètre pour spécifier explicitement les données de sensibilité.

  
**Retourne**: Clé de paramètres personnalisés.
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile fonction)
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.

  
**Retourne**: Clé de paramètres personnalisés.
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile fonction)
Nom du paramètre pour spécifier explicitement le chemin d’accès du fichier de données des types de sensibilité.

  
**Retourne**: Clé de paramètres personnalisés.
  
### <a name="getcustomsettingexternallabelsenabled-function"></a>GetCustomSettingExternalLabelsEnabled fonction)
Nom du paramètre qui autorise l’activation de la fonctionnalité «étiquettes externes».

  
**Retourne**: Clé de paramètres personnalisés.
  
### <a name="releaseallresources-function"></a>ReleaseAllResources fonction)
Libère toutes les ressources (threads, etc.) avant l’arrêt.
Cette fonction doit être appelée exactement une fois avant l’arrêt du processus. Elle offre au MIP la possibilité de ne pas s’initialiser dans un moment où ses bibliothèques dépendantes sont toujours chargées et que la jonction de threads est toujours possible. Les applications doivent libérer les références à tous les objets MIP (par exemple, les profils, les moteurs, les gestionnaires) avant d’appeler cette fonction.
Si cette fonction n’est pas appelée, le MIP sera naturellement déchargé dans le cadre de la destruction de processus standard. Sur certaines plateformes, cela peut entraîner un interblocage (par exemple, les threads ne peuvent pas être joints sur Win32 en réponse à la destruction du processus) ou des incidents (par exemple, l’ordre de déchargement de la DLL pour les bibliothèques à chargement différé sur Win32 n’est pas contrôlé par MIP, donc ses bibliothèques dépendantes peuvent ont été déchargées lors de l’exécution du code d’arrêt MIP, ce qui entraîne des échecs de lecture non valides.
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream fonction)
Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.

Paramètres :  
* **stdIStream**: Stockage std:: IStream



  
**Retourne**: [Flux](class_mip_stream.md) d’encapsulation d’un std:: IStream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream fonction)
Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.

Paramètres :  
* **stdOStream**: Stockage std:: ostream



  
**Retourne**: [Flux](class_mip_stream.md) d’encapsulation d’un std:: ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream fonction)
Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.

Paramètres :  
* **stdIOStream**: Stockage std:: iostream



  
**Retourne**: [Flux](class_mip_stream.md) d’encapsulation d’un std:: iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer fonction)
Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.

Paramètres :  
* **mémoire tampon**: Pointeur vers une mémoire tampon



  
**Retourne**: Taille de la mémoire tampon
  



## <a name="namespace-mipauditmetadatakeys"></a>Espace de noms MIP:: auditmetadatakeys

### <a name="sender-function"></a>Fonction d’expéditeur
Clés de métadonnées d’audit dans la représentation sous forme de chaîne.
  
### <a name="recipients-function"></a>Fonction Recipients
_Pas encore documenté._

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy fonction)
_Pas encore documenté._

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate & fonction)
_Pas encore documenté._






## <a name="namespace-miprights"></a>Espace de noms MIP:: Rights

### <a name="owner-function"></a>Fonction owner
Obtient un identificateur de chaîne pour un droit « propriétaire ».

  
**Retourne**: Identificateur de chaîne pour «owner» à droite
  
### <a name="view-function"></a>View, fonction
Obtient un identificateur de chaîne pour un droit « afficher ».

  
**Retourne**: Identificateur de chaîne pour «View» à droite
  
### <a name="auditedextract-function"></a>AuditedExtract fonction)
Obtient un identificateur de chaîne pour un droit « extraction auditée ».

  
**Retourne**: Identificateur de chaîne pour le droit «extraction auditée»
  
### <a name="edit-function"></a>Modifier la fonction
Obtient un identificateur de chaîne pour un droit « modifier ».

  
**Retourne**: Identificateur de chaîne pour le droit’modifier'
  
### <a name="export-function"></a>Fonction d’exportation
Obtient un identificateur de chaîne pour un droit « exporter ».

  
**Retourne**: Identificateur de chaîne pour «Export» à droite
  
### <a name="extract-function"></a>Extraire la fonction
Obtient un identificateur de chaîne pour un droit « extraire ».

  
**Retourne**: Identificateur de chaîne pour «Extract» à droite
  
### <a name="print-function"></a>Print, fonction
Obtient un identificateur de chaîne pour un droit « imprimer ».

  
**Retourne**: Identificateur de chaîne pour «imprimer» à droite
  
### <a name="comment-function"></a>Fonction comment
Obtient un identificateur de chaîne pour un droit « commentaire ».

  
**Retourne**: Identificateur de chaîne pour’commentaire’à droite
  
### <a name="reply-function"></a>Reply, fonction
Obtient un identificateur de chaîne pour un droit « répondre ».

  
**Retourne**: Identificateur de chaîne pour «reply» à droite
  
### <a name="replyall-function"></a>ReplyAll, fonction
Obtient un identificateur de chaîne pour un droit « répondre à tous ».

  
**Retourne**: Identificateur de chaîne pour «répondre à tous» à droite
  
### <a name="forward-function"></a>Fonction Forward
Obtient un identificateur de chaîne pour un droit « transférer ».

  
**Retourne**: Identificateur de chaîne pour’Forward’à droite
  
### <a name="emailrights-function"></a>EmailRights fonction)
Obtient une liste de droits qui s’appliquent aux e-mails.

  
**Retourne**: Liste des droits qui s’appliquent aux courriers électroniques
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights fonction)
Obtient une liste de droits qui s’appliquent aux documents.

  
**Retourne**: Liste des droits qui s’appliquent aux documents
  
### <a name="commonrights-function"></a>CommonRights fonction)
Obtient une liste des droits qui s’appliquent dans tous les scénarios.

  
**Retourne**: Liste des droits qui s’appliquent à tous les scénarios


## <a name="namespace-miproles"></a>Espace de noms MIP:: Roles

### <a name="viewer-function"></a>Fonction de visionneuse
Obtient un identificateur de chaîne pour un rôle « observateur ».

  
**Retourne**: Identificateur de chaîne pour le rôle’observateur’une visionneuse peut uniquement afficher le contenu. Il ne peut ni le modifier, ni le copier, ni l’imprimer.
  
### <a name="reviewer-function"></a>Fonction de réviseur
Obtient un identificateur de chaîne pour un rôle « réviseur ».

  
**Retourne**: Identificateur de chaîne pour le rôle’réviseur’un réviseur peut afficher et modifier le contenu. Ils ne peut ni le copier ni l’imprimer.
  
### <a name="author-function"></a>Author, fonction
Obtient un identificateur de chaîne pour un rôle « auteur ».

  
**Retourne**: Identificateur de chaîne pour le rôle’auteur’un auteur peut afficher, modifier, copier et imprimer le contenu.
  
### <a name="coowner-function"></a>Copropriétaire, fonction
Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

  
**Retourne**: Identificateur de chaîne pour le rôle «copropriétaire» un copropriétaire a toutes les autorisations