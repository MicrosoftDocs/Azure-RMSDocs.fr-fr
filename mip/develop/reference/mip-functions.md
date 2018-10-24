---
title: Fonctions
description: Fonctions
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3bb9cd594022085c24c45bde428cb11f6734caab
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446513"
---
# <a name="functions"></a>Fonctions

| Fonctions (étendue)              | Descriptions                                |
|--------------------------------|---------------------------------------------|
**common** |
public const std::string& GetCustomSettingPolicyDataName()       |  Nom du paramètre pour spécifier explicitement les données de stratégie.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.
 **fonctions mip** |
public std::shared_ptr<mip::Stream> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::iostream>& stdIOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::istream>& stdIStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::ostream>& stdOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.
public void ReleaseAllResources()       |  Libère toutes les ressources (threads, etc.) avant l’arrêt.
**fonctions MIP::Rights**|
public std::string AuditedExtract()       |  Obtient un identificateur de chaîne pour un droit « extraction auditée ».
public std::string Comment()       |  Obtient un identificateur de chaîne pour un droit « commentaire ».
public std::vector<std::string> CommonRights()       |  Obtient une liste des droits qui s’appliquent dans tous les scénarios.
public std::string Edit()       |  Obtient un identificateur de chaîne pour un droit « modifier ».
public std::vector<std::string> EditableDocumentRights()       |  Obtient une liste de droits qui s’appliquent aux documents.
public std::vector<std::string> EmailRights()       |  Obtient une liste de droits qui s’appliquent aux e-mails.
public std::string Export()       |  Obtient un identificateur de chaîne pour un droit « exporter ».
public std::string Extract()       |  Obtient un identificateur de chaîne pour un droit « extraire ».
public std::string Forward()       |  Obtient un identificateur de chaîne pour un droit « transférer ».
public std::string Owner()       |  Obtient un identificateur de chaîne pour un droit « propriétaire ».
public std::string Print()       |  Obtient un identificateur de chaîne pour un droit « imprimer ».
public std::string Reply()       |  Obtient un identificateur de chaîne pour un droit « répondre ».
public std::string ReplyAll()       |  Obtient un identificateur de chaîne pour un droit « répondre à tous ».
public std::string View()       |  Obtient un identificateur de chaîne pour un droit « afficher ».
**fonctions mip::Roles**|
public std::string Author()       |  Obtient un identificateur de chaîne pour un rôle « auteur ».
public std::string CoOwner()       |  Obtient un identificateur de chaîne pour un rôle « copropriétaire ».
public std::string Reviewer()       |  Obtient un identificateur de chaîne pour un rôle « réviseur ».
public std::string Viewer()       |  Obtient un identificateur de chaîne pour un rôle « observateur ».

  
## <a name="functions-common"></a>Fonctions (communes)

### <a name="getcustomsettingpolicydataname"></a>GetCustomSettingPolicyDataName
Nom du paramètre pour spécifier explicitement les données de stratégie.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingexportpolicyfilename"></a>GetCustomSettingExportPolicyFileName
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.

  
**Renvoie** : la clé des paramètres personnalisés.
  
### <a name="getcustomsettingpolicydatafile"></a>GetCustomSettingPolicyDataFile
Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.

  
**Renvoie** : la clé des paramètres personnalisés.

## <a name="functions-mip"></a>Fonctions (mip)

### <a name="mipcreatestreamfrombufferbuffer"></a>mip::CreateStreamFromBuffer(buffer)

Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon

**Retourne** : **taille** de mémoire tampon
  

### <a name="mipcreatestreamfromstdstreamistream"></a>mip::CreateStreamFromStdStream(istream)

Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.

Paramètres :  

* **stdIStream** : sauvegarde std::istream
  
**Retourne** : [flux](class_mip_stream.md) wrappant std::istream
  
### <a name="mipcreatestreamfromstdstreamiostream"></a>mip::CreateStreamFromStdStream(iostream)

Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.

Paramètres :  
* **stdIOStream** : sauvegarde std::iostream
  
**Retourne** : [flux](class_mip_stream.md) wrappant std::iostream 
  
### <a name="mipcreatestreamfromstdstreamostream"></a>mip::CreateStreamFromStdStream(ostream)

Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.

Paramètres :  
* **stdIStream** : sauvegarde std::ostream
  
**Retourne** : [flux](class_mip_stream.md) wrappant un std::ostream
  
### <a name="mipreleaseallresources"></a>mip::ReleaseAllResources

Libère toutes les ressources (threads, etc.) avant l’arrêt.  

Si les bibliothèques dynamiques MIP sont chargées en différé par une application, cette fonction doit être appelée avant que l’application ne décharge explicitement ces bibliothèques MIP pour éviter un blocage. Par exemple, sur win32, cette fonction doit être appelée avant tout appel pour décharger explicitement les DLL MIP via FreeLibrary ou \__FUnloadDelayLoadedDLL2. Les applications doivent libérer les références à tous les objets MIP (par exemple, les profils, les moteurs, les gestionnaires) avant d’appeler cette fonction.

## <a name="functions-miprights"></a>Fonctions (mip::rights)

### <a name="owner"></a>Propriétaire
Obtient un identificateur de chaîne pour un droit « propriétaire ».

  
**Renvoie** : identificateur de chaîne pour un droit « propriétaire »
  
### <a name="auditedextract"></a>AuditedExtract
Obtient un identificateur de chaîne pour un droit « extraction auditée ».

  
**Renvoie** : identificateur de chaîne pour un droit « extraction auditée »
  
### <a name="comment"></a>Comment
Obtient un identificateur de chaîne pour un droit « commentaire ».

  
**Renvoie** : identificateur de chaîne pour un droit « commentaire »
  
### <a name="commonrights"></a>CommonRights
Obtient une liste des droits qui s’appliquent dans tous les scénarios.

  
**Renvoie** : une liste des droits qui s’appliquent dans tous les scénarios

### <a name="edit"></a>Modifier
Obtient un identificateur de chaîne pour un droit « modifier ».

  
**Renvoie** : identificateur de chaîne pour droit « modifier »
  
### <a name="editabledocumentrights"></a>EditableDocumentRights
Obtient une liste de droits qui s’appliquent aux documents.

  
**Renvoie** : une liste de droits qui s’appliquent aux documents
  
### <a name="emailrights"></a>EmailRights
Obtient une liste de droits qui s’appliquent aux e-mails.

  
**Renvoie** : une liste de droits qui s’appliquent aux e-mails
  
### <a name="export"></a>Exportation
Obtient un identificateur de chaîne pour un droit « exporter ».

  
**Renvoie** : identificateur de chaîne de « export » vers la droite
  
### <a name="extract"></a>Extract
Obtient un identificateur de chaîne pour un droit « extraire ».

  
**Renvoie** : identificateur de chaîne pour un droit « extraire »
  
### <a name="forward"></a>Forward
Obtient un identificateur de chaîne pour un droit « transférer ».

  
**Renvoie** : identificateur de chaîne pour un droit « transférer »
  
### <a name="print"></a>Print
Obtient un identificateur de chaîne pour un droit « imprimer ».

  
**Renvoie** : identificateur de chaîne pour un droit « imprimer »
  
### <a name="reply"></a>Reply
Obtient un identificateur de chaîne pour un droit « répondre ».

  
**Renvoie** : identificateur de chaîne pour un droit « répondre »
  
### <a name="replyall"></a>ReplyAll
Obtient un identificateur de chaîne pour un droit « répondre à tous ».

  
**Renvoie** : identificateur de chaîne pour un droit « répondre à tous »
  
### <a name="view"></a>View
Obtient un identificateur de chaîne pour un droit « afficher ».

  
**Renvoie** : identificateur de chaîne pour un droit « afficher »
  

## <a name="functions-miproles"></a>Fonctions (mip::roles)

### <a name="author"></a>Auteur
Obtient un identificateur de chaîne pour un rôle « auteur ».

Un auteur peut afficher, modifier, copier et imprimer le contenu.
  
**Retourne** : identificateur de chaîne pour un rôle « auteur »
  
### <a name="coowner"></a>Copropriétaire
Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

Un copropriétaire a toutes les autorisations
  
**Retourne** : identificateur de chaîne pour un rôle « copropriétaire »

### <a name="reviewer"></a>Réviseur
Obtient un identificateur de chaîne pour un rôle « réviseur ».

Un réviseur peut afficher et modifier le contenu. Ils ne peut ni le copier ni l’imprimer.
  
**Retourne** : identificateur de chaîne pour un rôle « réviseur »
  
### <a name="viewer"></a>Observateur
Obtient un identificateur de chaîne pour un rôle « observateur ».

Un observateur peut uniquement afficher le contenu. Il ne peut ni le modifier, ni le copier, ni l’imprimer.
  
**Retourne** : identificateur de chaîne pour un rôle « observateur »
  
