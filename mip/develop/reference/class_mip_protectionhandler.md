---
title: ProtectionHandler de classe
description: 'Documente la classe protectionhandler :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: e38aaf0e4dfee1d10f67f175eb50119fe3aa484d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567131"
---
# <a name="class-protectionhandler"></a>ProtectionHandler de classe 
Gère les actions liées à la protection pour une configuration de protection spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<Stream\> CreateProtectedStream(const std::shared_ptr\<Stream\>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Créer un flux protégé qui permet de chiffrer/déchiffrer le contenu.
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Chiffrer un tampon.
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Déchiffrer un tampon.
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce ProtectionHandler.
public int64_t GetBlockSize()  |  Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce ProtectionHandler.
public std :: Vector \<std::string\> GetRight () const  |  Obtient les droits accordés à l’identité/l’utilisateur associé à ce ProtectionHandler.
public bool AccessCheck(const std::string& right) const  |  Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.
public const std::string GetIssuedTo()  |  Obtient l’utilisateur associé au Gestionnaire de protection.
public const std::string GetOwner()  |  Obtient l’adresse e-mail du propriétaire du contenu.
public bool IsIssuedToOwner()  |  Indique si l’utilisateur actuel est le propriétaire du contenu ou non.
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor()  |  Obtient les détails de la protection.
public const std::string GetContentId()  |  Obtient l’identificateur unique du document/contenu.
public bool DoesUseDeprecatedAlgorithms()  |  Indique si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante ou non.
public bool IsAuditedExtractAllowed()  |  Indique si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non.
public const std :: Vector \<uint8_t\>& GetSerializedPublishingLicense () const  |  Sérialiser ProtectionHandler dans une licence de publication (PL)
public const std :: Vector \<uint8_t\>& GetSerializedPreLicense (format PreLicenseFormat) const  |  Procurez-vous une pré-licence.
public CipherMode GetCipherMode () const  |  Obtient le mode de chiffrement du gestionnaire de protection.
énumération PreLicenseFormat  |  Format de licence préalable.
  
## <a name="members"></a>Membres
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream fonction)
Créer un flux protégé qui permet de chiffrer/déchiffrer le contenu.

Paramètres :  
* **backingStream** : flux de sauvegarde à partir duquel lire/écrire 


* **contentStartPosition** : position de départ (en octets) dans le flux de sauvegarde où commence le contenu protégé 


* **contentSize** : taille (en octets) du contenu protégé dans le flux de sauvegarde



  
**Retourne** : le flux protégé
  
### <a name="encryptbuffer-function"></a>EncryptBuffer fonction)
Chiffrer un tampon.

Paramètres :  
* **offsetFromStart** : position relative d’inputBuffer à partir du début du contenu en texte clair 


* **inputBuffer** : mémoire tampon du contenu en texte clair qui sera chiffré 


* **inputBufferSize** : taille (en octets) de la mémoire tampon d’entrée 


* **outputBuffer** : mémoire tampon dans laquelle le contenu chiffré sera copié 


* **outputBufferSize** : taille (en octets) de la mémoire tampon de sortie 


* **isFinal** : valeur indiquant si la mémoire tampon d’entrée contient les octets du texte en clair final ou non



  
**Retourne** : la taille réelle (en octets) du contenu chiffré
  
### <a name="decryptbuffer-function"></a>DecryptBuffer fonction)
Déchiffrer un tampon.

Paramètres :  
* **offsetFromStart** : position relative d’inputBuffer à partir du début du contenu chiffré 


* **inputBuffer** : mémoire tampon du contenu chiffré qui sera déchiffré 


* **inputBufferSize** : taille (en octets) de la mémoire tampon d’entrée 


* **outputBuffer** : mémoire tampon dans laquelle le contenu déchiffré sera copié 


* **outputBufferSize** : taille (en octets) de la mémoire tampon de sortie 


* **isFinal** : valeur indiquant si la mémoire tampon d’entrée contient les octets du texte chiffré final ou non



  
**Retourne** : la taille réelle (en octets) du contenu déchiffré
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength fonction)
Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce ProtectionHandler.

Paramètres :  
* **unprotectedLength** : taille (en octets) du contenu non protégé 


* **includesFinalBlock** : décrit si le contenu non protégé en question inclut le dernier bloc ou non. Par exemple, en mode de chiffrement CBC4k, les blocs protégés non finaux sont de la même taille que les blocs non protégés, mais les blocs protégés finaux sont plus grands que leurs équivalents non protégés.



  
**Retourne** : la taille (en octets) du contenu protégé
  
### <a name="getblocksize-function"></a>GetBlockSize fonction)
Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce ProtectionHandler.

  
**Retourne** : la taille (en octets) du bloc
  
### <a name="getrights-function"></a>GetRight, fonction
Obtient les droits accordés à l’identité/l’utilisateur associé à ce ProtectionHandler.

  
**Retourne** : droits accordés à l’utilisateur
  
### <a name="accesscheck-function"></a>Fonction AccessCheck
Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.

Paramètres :  
* **right** : droit à vérifier



  
**Retourne** : valeur indiquant si le gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié ou non
  
### <a name="getissuedto-function"></a>GetIssuedTo fonction)
Obtient l’utilisateur associé au Gestionnaire de protection.

  
**Retourne** : l’utilisateur associé au Gestionnaire de protection
  
### <a name="getowner-function"></a>GetOwner fonction)
Obtient l’adresse e-mail du propriétaire du contenu.

  
**Retourne** : l’adresse e-mail du propriétaire du contenu
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner fonction)
Indique si l’utilisateur actuel est le propriétaire du contenu ou non.

  
**Retourne** : valeur indiquant s l’utilisateur actuel est le propriétaire du contenu ou non
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor fonction)
Obtient les détails de la protection.

  
**Retourne** : les détails de la protection
  
### <a name="getcontentid-function"></a>GetContentId fonction)
Obtient l’identificateur unique du document/contenu.

  
**Retourne** : l’identificateur unique du contenu
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms fonction)
Indique si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante ou non.

  
**Retourne** : valeur indiquant si le gestionnaire de protection utilise des algorithmes de chiffrement dépréciés ou non
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed fonction)
Indique si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non.

  
**Retourne** : valeur indiquant si le gestionnaire de protection accorde le droit « extraction auditée » à l’utilisateur ou non
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense fonction)
Sérialiser ProtectionHandler dans une licence de publication (PL)

  
**Retourne** : licence de publication sérialisée
  
### <a name="getserializedprelicense-function"></a>GetSerializedPreLicense fonction)
Procurez-vous une pré-licence.

Paramètres :  
* **format**: format de pré-licence



  
**Retourne**: pré-licence sérialisée une pré-licence permet à un utilisateur de consommer immédiatement du contenu sans effectuer d’appel http supplémentaire. ProtectionHandler doit avoir été créé avec une valeur ProtectionHandler ::P ublishingSettings :: SetPreLicenseUserEmail, sinon un vecteur vide est retourné.
  
### <a name="getciphermode-function"></a>GetCipherMode fonction)
Obtient le mode de chiffrement du gestionnaire de protection.

  
**Retourne**: le mode de chiffrement
  
### <a name="prelicenseformat-enum"></a>Énumération PreLicenseFormat

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Xml            | Format XML/SOAP hérité utilisé par MSIPC
Json            | Format JSON/REST utilisé par le kit de développement logiciel MIP et kit de développement logiciel (SDK) RMS

Format de licence préalable.