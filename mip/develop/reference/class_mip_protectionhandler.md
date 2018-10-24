---
title: mip ProtectionHandler, classe
description: Informations de référence pour la classe mip ProtectionHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6fbae05030f56d3c9e680e6de9c8177a11b2f1e2
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446751"
---
# <a name="class-mipprotectionhandler"></a>class mip::ProtectionHandler 
Gère les actions liées à la protection pour une configuration de protection spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Créer un flux protégé qui permet de chiffrer/déchiffrer le contenu.
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Chiffrer un tampon.
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Déchiffrer un tampon.
 public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce [ProtectionHandler](class_mip_protectionhandler.md).
 public int64_t GetBlockSize()  |  Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce [ProtectionHandler](class_mip_protectionhandler.md).
public std::vector<std::string> GetRights() const  |  Obtient les droits accordés à l’identité/l’utilisateur associé à ce [ProtectionHandler](class_mip_protectionhandler.md).
 public bool AccessCheck(const std::string& right) const  |  Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.
 public const std::string GetIssuedTo()  |  Obtient l’utilisateur associé au Gestionnaire de protection.
 public const std::string GetOwner()  |  Obtient l’adresse e-mail du propriétaire du contenu.
 public bool IsIssuedToOwner()  |  Indique si l’utilisateur actuel est le propriétaire du contenu ou non.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  Obtient les détails de la protection.
 public const std::string GetContentId()  |  Obtient l’identificateur unique du document/contenu.
 public bool DoesUseDeprecatedAlgorithms()  |  Indique si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante ou non.
 public bool IsAuditedExtractAllowed()  |  Indique si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non.
public const std::vector<uint8_t> GetSerializedPublishingLicense()  |  Sérialiser [ProtectionHandler](class_mip_protectionhandler.md) dans une licence de publication (PL)
  
## <a name="members"></a>Membres
  
### <a name="stream"></a>Flux
Créer un flux protégé qui permet de chiffrer/déchiffrer le contenu.

Paramètres :  
* **backingStream** : flux de sauvegarde à partir duquel lire/écrire 


* **contentStartPosition** : position de départ (en octets) dans le flux de sauvegarde où commence le contenu protégé 


* **contentSize** : taille (en octets) du contenu protégé dans le flux de sauvegarde



  
**Retourne** : le flux protégé
  
### <a name="encryptbuffer"></a>EncryptBuffer
Chiffrer un tampon.

Paramètres :  
* **offsetFromStart** : position relative d’inputBuffer à partir du début du contenu en texte clair 


* **inputBuffer** : mémoire tampon du contenu en texte clair qui sera chiffré 


* **inputBufferSize** : taille (en octets) de la mémoire tampon d’entrée 


* **outputBuffer** : mémoire tampon dans laquelle le contenu chiffré sera copié 


* **outputBufferSize** : taille (en octets) de la mémoire tampon de sortie 


* **isFinal** : valeur indiquant si la mémoire tampon d’entrée contient les octets du texte en clair final ou non



  
**Retourne** : la taille réelle (en octets) du contenu chiffré
  
### <a name="decryptbuffer"></a>DecryptBuffer
Déchiffrer un tampon.

Paramètres :  
* **offsetFromStart** : position relative d’inputBuffer à partir du début du contenu chiffré 


* **inputBuffer** : mémoire tampon du contenu chiffré qui sera déchiffré 


* **inputBufferSize** : taille (en octets) de la mémoire tampon d’entrée 


* **outputBuffer** : mémoire tampon dans laquelle le contenu déchiffré sera copié 


* **outputBufferSize** : taille (en octets) de la mémoire tampon de sortie 


* **isFinal** : valeur indiquant si la mémoire tampon d’entrée contient les octets du texte chiffré final ou non



  
**Retourne** : la taille réelle (en octets) du contenu déchiffré
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce [ProtectionHandler](class_mip_protectionhandler.md).

Paramètres :  
* **unprotectedLength** : taille (en octets) du contenu non protégé 


* **includesFinalBlock** : décrit si le contenu non protégé en question inclut le dernier bloc ou non. Par exemple, en mode de chiffrement CBC4k, les blocs protégés non finaux sont de la même taille que les blocs non protégés, mais les blocs protégés finaux sont plus grands que leurs équivalents non protégés.



  
**Retourne** : la taille (en octets) du contenu protégé
  
### <a name="getblocksize"></a>GetBlockSize
Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce [ProtectionHandler](class_mip_protectionhandler.md).

  
**Retourne** : la taille (en octets) du bloc
  
### <a name="getrights"></a>GetRights
Obtient les droits accordés à l’identité/l’utilisateur associé à ce [ProtectionHandler](class_mip_protectionhandler.md).

  
**Retourne** : droits accordés à l’utilisateur
  
### <a name="accesscheck"></a>AccessCheck
Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.

Paramètres :  
* **right** : droit à vérifier



  
**Retourne** : valeur indiquant si le gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié ou non
  
### <a name="getissuedto"></a>GetIssuedTo
Obtient l’utilisateur associé au Gestionnaire de protection.

  
**Retourne** : l’utilisateur associé au Gestionnaire de protection
  
### <a name="getowner"></a>GetOwner
Obtient l’adresse e-mail du propriétaire du contenu.

  
**Retourne** : l’adresse e-mail du propriétaire du contenu
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Indique si l’utilisateur actuel est le propriétaire du contenu ou non.

  
**Retourne** : valeur indiquant s l’utilisateur actuel est le propriétaire du contenu ou non
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Obtient les détails de la protection.

  
**Retourne** : les détails de la protection
  
### <a name="getcontentid"></a>GetContentId
Obtient l’identificateur unique du document/contenu.

  
**Retourne** : l’identificateur unique du contenu
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Indique si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante ou non.

  
**Retourne** : valeur indiquant si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés ou non
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Indique si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non.

  
**Retourne** : valeur indiquant si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
Sérialiser [ProtectionHandler](class_mip_protectionhandler.md) dans une licence de publication (PL)

  
**Retourne** : licence de publication sérialisée