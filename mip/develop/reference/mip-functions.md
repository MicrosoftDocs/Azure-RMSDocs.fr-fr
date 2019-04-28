---
title: Fonctions
description: Fonctions
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: ced8339fa93ec349644a1f9e386489bb02c8eff0
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173409"
---
# <a name="functions"></a>Fonctions

## <a name="summary"></a>Récapitulatif 

### <a name="namespace-mip"></a>Namespace mip
| Fonctions selon la portée espace de noms   | Descriptions                                |
|--------------------------------|---------------------------------------------|
public std::string GetAssignmentMethodString (méthode de la méthode d’assignation)       |  Convertit la méthode d’assignation enum pour une description de chaîne.
public static std::string GetActionSourceString(ActionSource actionSource)       |  Obtenir le nom de source d’action.
public static std::string GetDataStateString(mip::DataState state)       |  Obtenir le nom de l’état du contenu.
public const std::string& GetCustomSettingPolicyDataName()       |  Nom du paramètre pour spécifier explicitement les données de stratégie.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.
public const std::string& GetCustomSettingSensitivityTypesDataName()       |  Nom du paramètre pour spécifier explicitement les données de sensibilité.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.
public const std::string& GetCustomSettingSensitivityTypesDataFile()       |  Nom du paramètre pour spécifier explicitement la sensibilité de types de chemin d’accès du fichier de données.
public const std::string& GetCustomSettingExternalLabelsEnabled()       |  Nom du paramètre qui permet d’activer la fonctionnalité de « étiquettes externes ».
public __CDECL void MIP_API ReleaseAllResources()       |  Libère toutes les ressources (threads, etc.) avant l’arrêt.
public std::shared_ptr MIP_API\<mip::Stream\> CreateStreamFromStdStream (const std::shared_ptr\<std::istream\>& stdIStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromStdStream(const std::shared_ptr\<std::ostream\>& stdOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromStdStream(const std::shared_ptr\<std::iostream\>& stdIOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.


### <a name="namespace-mipauditmetadatakeys"></a>Namespace mip::auditmetadatakeys
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string Sender()       |  Auditer les clés de métadonnées dans la représentation sous forme de chaîne.
public std::string Recipients()       | _Pas encore documenté._
public std::string LastModifiedBy()       | _Pas encore documenté._
public std::string LastModifiedDate()       | _Pas encore documenté._


### <a name="namespace-miprights"></a>Namespace mip::rights

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

### <a name="namespace-miproles"></a>Namespace mip::roles

 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  Obtient un identificateur de chaîne pour un rôle « observateur ».
public std::string Reviewer()       |  Obtient un identificateur de chaîne pour un rôle « réviseur ».
public std::string Author()       |  Obtient un identificateur de chaîne pour un rôle « auteur ».
public std::string CoOwner()       |  Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

## <a name="namespace-mip"></a>Namespace mip

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString (fonction)
Convertit la méthode d’assignation enum pour une description de chaîne.

Paramètres :  
* **méthode**: méthode d’attribution. 



  
**Retourne**: Description de la méthode d’affectation dans une chaîne.
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString (fonction)
Obtenir le nom de source d’action.

Paramètres :  
* **actionSource**: La source de l’action. 



  
**Retourne**: Représentation sous forme de chaîne de la source de l’action.
  
### <a name="getdatastatestring-function"></a>GetDataStateString (fonction)
Obtenir le nom de l’état du contenu.

Paramètres :  
* **actionSource**: L’état du contenu sur laquelle vous travaillez. 



  
**Retourne**: Représentation sous forme de chaîne de l’état du contenu.
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName function
Nom du paramètre pour spécifier explicitement les données de stratégie.

  
**Retourne**: La clé de paramètres personnalisés.
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName function
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.

  
**Retourne**: La clé de paramètres personnalisés.
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName function
Nom du paramètre pour spécifier explicitement les données de sensibilité.

  
**Retourne**: La clé de paramètres personnalisés.
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile function
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.

  
**Retourne**: La clé de paramètres personnalisés.
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile function
Nom du paramètre pour spécifier explicitement la sensibilité de types de chemin d’accès du fichier de données.

  
**Retourne**: La clé de paramètres personnalisés.
  
### <a name="getcustomsettingexternallabelsenabled-function"></a>GetCustomSettingExternalLabelsEnabled function
Nom du paramètre qui permet d’activer la fonctionnalité de « étiquettes externes ».

  
**Retourne**: La clé de paramètres personnalisés.
  
### <a name="releaseallresources-function"></a>ReleaseAllResources (fonction)
Libère toutes les ressources (threads, etc.) avant l’arrêt.
Cette fonction doit être appelée une seule fois avant l’arrêt du processus. Il fournit MIP la possibilité d’annuler l’initialisation de lui-même dans un moment où ses bibliothèques dépendantes sont malgrés tout être chargé et jointure de thread est toujours possible. Les applications doivent libérer les références à tous les objets MIP (par exemple, les profils, les moteurs, les gestionnaires) avant d’appeler cette fonction.
Si cette fonction n’est pas appelée, MIP sera naturellement déchargé dans le cadre de la destruction du processus standard. Sur certaines plateformes, cela peut entraîner un blocage (par exemple, threads ne peut pas être joint sur win32 en réponse à traiter la destruction) ou de défaillance (par exemple, l’ordre de déchargement DLL pour le chargement différé des bibliothèques sur win32 n'est pas contrôlé par MIP, donc ses bibliothèques dépendantes peuvent ont été déchargée par moment de l’exécution de code d’arrêt MIP, ce qui entraîne des échecs de lecture non valides).
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (fonction)
Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.

Paramètres :  
* **stdIStream**: Sauvegarde std::istream



  
**Retourne**: [Stream](class_mip_stream.md) encapsulant une std::istream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (fonction)
Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.

Paramètres :  
* **stdOStream**: Sauvegarde std::ostream



  
**Retourne**: [Stream](class_mip_stream.md) encapsulant une std::ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (fonction)
Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.

Paramètres :  
* **stdIOStream**: Sauvegarde std::iostream



  
**Retourne**: [Stream](class_mip_stream.md) encapsulant une std::iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer (fonction)
Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.

Paramètres :  
* **mémoire tampon**: Pointeur vers une mémoire tampon



  
**Retourne**: Taille de taille de mémoire tampon
  



## <a name="namespace-mipauditmetadatakeys"></a>Namespace mip::auditmetadatakeys

### <a name="sender-function"></a>Fonction de l’expéditeur
Auditer les clés de métadonnées dans la représentation sous forme de chaîne.
  
### <a name="recipients-function"></a>Fonction de destinataires
_Pas encore documenté._

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy (fonction)
_Pas encore documenté._

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate & gt ; (fonction)
_Pas encore documenté._






## <a name="namespace-miprights"></a>Namespace mip::rights

### <a name="owner-function"></a>Fonction de propriétaire
Obtient un identificateur de chaîne pour un droit « propriétaire ».

  
**Retourne**: Identificateur de chaîne de droite « propriétaire »
  
### <a name="view-function"></a>Vue (fonction)
Obtient un identificateur de chaîne pour un droit « afficher ».

  
**Retourne**: Identificateur de chaîne de « view » vers la droite
  
### <a name="auditedextract-function"></a>AuditedExtract (fonction)
Obtient un identificateur de chaîne pour un droit « extraction auditée ».

  
**Retourne**: Identificateur de chaîne de « audited extract » à droite
  
### <a name="edit-function"></a>Modifier (fonction)
Obtient un identificateur de chaîne pour un droit « modifier ».

  
**Retourne**: Identificateur de chaîne de droite 'modifier'
  
### <a name="export-function"></a>Fonction d’exportation
Obtient un identificateur de chaîne pour un droit « exporter ».

  
**Retourne**: Identificateur de chaîne de « export » vers la droite
  
### <a name="extract-function"></a>Extraire (fonction)
Obtient un identificateur de chaîne pour un droit « extraire ».

  
**Retourne**: Identificateur de chaîne de droite « extraire »
  
### <a name="print-function"></a>Fonction d’impression
Obtient un identificateur de chaîne pour un droit « imprimer ».

  
**Retourne**: Identificateur de chaîne de droite « impression »
  
### <a name="comment-function"></a>Fonction de commentaire
Obtient un identificateur de chaîne pour un droit « commentaire ».

  
**Retourne**: Identificateur de chaîne de « commentaire » vers la droite
  
### <a name="reply-function"></a>Fonction de la réponse
Obtient un identificateur de chaîne pour un droit « répondre ».

  
**Retourne**: Identificateur de chaîne de « réponse » à droite
  
### <a name="replyall-function"></a>ReplyAll (fonction)
Obtient un identificateur de chaîne pour un droit « répondre à tous ».

  
**Retourne**: Identificateur de chaîne de droite « répondre à tous »
  
### <a name="forward-function"></a>Vers l’avant (fonction)
Obtient un identificateur de chaîne pour un droit « transférer ».

  
**Retourne**: Identificateur de chaîne de droit « transfert »
  
### <a name="emailrights-function"></a>EmailRights (fonction)
Obtient une liste de droits qui s’appliquent aux e-mails.

  
**Retourne**: Une liste des droits qui s’appliquent aux e-mails
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights (fonction)
Obtient une liste de droits qui s’appliquent aux documents.

  
**Retourne**: Une liste des droits qui s’appliquent aux documents
  
### <a name="commonrights-function"></a>CommonRights (fonction)
Obtient une liste des droits qui s’appliquent dans tous les scénarios.

  
**Retourne**: Une liste des droits qui s’appliquent dans tous les scénarios


## <a name="namespace-miproles"></a>Namespace mip::roles

### <a name="viewer-function"></a>Fonction de la visionneuse
Obtient un identificateur de chaîne pour un rôle « observateur ».

  
**Retourne**: Identificateur de chaîne pour le rôle de « visionneuse » une visionneuse peut uniquement afficher le contenu. Il ne peut ni le modifier, ni le copier, ni l’imprimer.
  
### <a name="reviewer-function"></a>Fonction du réviseur
Obtient un identificateur de chaîne pour un rôle « réviseur ».

  
**Retourne**: Identificateur de chaîne pour le rôle de « réviseur » un réviseur peut afficher et modifier le contenu. Ils ne peut ni le copier ni l’imprimer.
  
### <a name="author-function"></a>Fonction de l’auteur
Obtient un identificateur de chaîne pour un rôle « auteur ».

  
**Retourne**: Identificateur de chaîne de rôle « author » un auteur peut afficher, modifier, copier et imprimer le contenu.
  
### <a name="coowner-function"></a>Fonction de coOwner
Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

  
**Retourne**: Identificateur de chaîne pour le rôle de « copropriétaire » un copropriétaire a toutes les autorisations