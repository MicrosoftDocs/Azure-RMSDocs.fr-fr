---
title: class mip::ProtectionHandler
description: Décrit la classe mip::protectionhandler de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 20ac5207e744224d9d8eaef72607708721c55172
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184465"
---
# <a name="class-mipprotectionhandler"></a>class mip::ProtectionHandler 
Gère les actions liées à la protection pour une configuration de protection spécifique.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<Stream\> CreateProtectedStream(const std::shared_ptr\<Stream\>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Créer un flux protégé qui permet de chiffrer/déchiffrer le contenu.
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Chiffrer un tampon.
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Déchiffrer un tampon.
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce [ProtectionHandler](class_mip_protectionhandler.md).
public int64_t GetBlockSize()  |  Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce [ProtectionHandler](class_mip_protectionhandler.md).
public std::vector\<std::string\> GetRights() const  |  Obtient les droits accordés à l’identité/l’utilisateur associé à ce [ProtectionHandler](class_mip_protectionhandler.md).
public bool AccessCheck(const std::string& right) const  |  Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.
public const std::string GetIssuedTo()  |  Obtient l’utilisateur associé au Gestionnaire de protection.
public const std::string GetOwner()  |  Obtient l’adresse e-mail du propriétaire du contenu.
public bool IsIssuedToOwner()  |  Indique si l’utilisateur actuel est le propriétaire du contenu ou non.
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor()  |  Obtient les détails de la protection.
public const std::string GetContentId()  |  Obtient l’identificateur unique du document/contenu.
public bool DoesUseDeprecatedAlgorithms()  |  Indique si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante ou non.
public bool IsAuditedExtractAllowed()  |  Indique si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non.
public const std::vector\<uint8_t\> GetSerializedPublishingLicense()  |  Sérialiser [ProtectionHandler](class_mip_protectionhandler.md) dans une licence de publication (PL)
public const std::vector\<uint8_t\> GetSerializedProtectionInfo()  |  Obtient les informations de protection.
  
## <a name="members"></a>Membres
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream (fonction)
Créer un flux protégé qui permet de chiffrer/déchiffrer le contenu.

Paramètres :  
* **backingStream**: Flux de sauvegarde à partir de laquelle en lecture/écriture 


* **contentStartPosition**: À partir de la position (en octets) dans le flux de sauvegarde où du contenu protégé commence 


* **contentSize**: Taille (en octets) du contenu protégé dans le flux de données de sauvegarde



  
**Retourne**: Flux de données protégé
  
### <a name="encryptbuffer-function"></a>EncryptBuffer (fonction)
Chiffrer un tampon.

Paramètres :  
* **offsetFromStart**: Position relative d’inputBuffer dès le début du contenu en texte clair 


* **inputBuffer**: Mémoire tampon du contenu de texte en clair qui est chiffrée 


* **inputBufferSize**: Taille (en octets) de mémoire tampon d’entrée 


* **outputBuffer**: Mémoire tampon dans laquelle sera copié le contenu chiffré 


* **outputBufferSize**: Taille (en octets) de mémoire tampon de sortie 


* **isFinal**: Si la mémoire tampon d’entrée contient les octets de texte en clair finale ou non



  
**Retourne**: Taille réelle (en octets) du contenu chiffré
  
### <a name="decryptbuffer-function"></a>DecryptBuffer (fonction)
Déchiffrer un tampon.

Paramètres :  
* **offsetFromStart**: Position relative d’inputBuffer dès le début du contenu chiffré 


* **inputBuffer**: Mémoire tampon du contenu chiffré sera déchiffré 


* **inputBufferSize**: Taille (en octets) de mémoire tampon d’entrée 


* **outputBuffer**: Mémoire tampon dans laquelle le contenu déchiffré est copié 


* **outputBufferSize**: Taille (en octets) de mémoire tampon de sortie 


* **isFinal**: Si la mémoire tampon d’entrée contient les octets de cryptée finales ou non



  
**Retourne**: Taille réelle (en octets) du contenu déchiffré
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength (fonction)
Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce [ProtectionHandler](class_mip_protectionhandler.md).

Paramètres :  
* **unprotectedLength**: Taille (en octets) du contenu non protégé 


* **includesFinalBlock**: Décrit si le contenu non protégé en question inclut le dernier bloc ou non. Par exemple, en mode de chiffrement CBC4k, les blocs protégés non finaux sont de la même taille que les blocs non protégés, mais les blocs protégés finaux sont plus grands que leurs équivalents non protégés.



  
**Retourne**: Taille (en octets) du contenu protégé
  
### <a name="getblocksize-function"></a>GetBlockSize (fonction)
Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce [ProtectionHandler](class_mip_protectionhandler.md).

  
**Retourne**: Taille de bloc (en octets)
  
### <a name="getrights-function"></a>GetRights (fonction)
Obtient les droits accordés à l’identité/l’utilisateur associé à ce [ProtectionHandler](class_mip_protectionhandler.md).

  
**Retourne**: Droits octroyés à l’utilisateur
  
### <a name="accesscheck-function"></a>AccessCheck (fonction)
Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.

Paramètres :  
* **droit**: Droit à vérifier



  
**Retourne**: Si le Gestionnaire de protection accorde l’accès d’utilisateur spécifié à la droite ou non
  
### <a name="getissuedto-function"></a>GetIssuedTo (fonction)
Obtient l’utilisateur associé au Gestionnaire de protection.

  
**Retourne**: Utilisateur associé au Gestionnaire de protection
  
### <a name="getowner-function"></a>GetOwner (fonction)
Obtient l’adresse e-mail du propriétaire du contenu.

  
**Retourne**: Adresse e-mail du propriétaire du contenu
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner (fonction)
Indique si l’utilisateur actuel est le propriétaire du contenu ou non.

  
**Retourne**: Si l’utilisateur actuel est le propriétaire du contenu ou non
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (fonction)
Obtient les détails de la protection.

  
**Retourne**: Détails de la protection
  
### <a name="getcontentid-function"></a>GetContentId (fonction)
Obtient l’identificateur unique du document/contenu.

  
**Retourne**: Identificateur unique du contenu
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms (fonction)
Indique si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante ou non.

  
**Retourne**: Si le Gestionnaire de protection utilise déconseillé d’algorithmes de chiffrement ou non
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed (fonction)
Indique si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non.

  
**Retourne**: Si le Gestionnaire de protection accorde utilisateur « audited extract » à droite ou non
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense (fonction)
Sérialiser [ProtectionHandler](class_mip_protectionhandler.md) dans une licence de publication (PL)

  
**Retourne**: Licence de publication sérialisée
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
Obtient les informations de protection.

  
**Retourne**: Informations de protection sérialisée