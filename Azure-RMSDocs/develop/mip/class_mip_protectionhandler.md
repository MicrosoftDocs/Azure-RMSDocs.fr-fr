# <a name="class-mipprotectionhandler"></a>class mip::ProtectionHandler 
Effectue des actions liées à la protection pour une configuration de protection spécifique (par exemple, utilisateurs, droits, rôles, etc.)
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, uint64_t contentStartPosition, uint64_t contentSize)  |  Créer un flux protégé, qui permet de chiffrer/déchiffrer le contenu.
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Chiffrer un tampon.
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Déchiffrer un tampon.
 public uint64_t GetProtectedContentLength(uint64_t size)  |  Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce [ProtectionHandler](class_mip_protectionhandler.md).
 public uint64_t GetBlockSize()  |  Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce [ProtectionHandler](class_mip_protectionhandler.md).
 public bool AccessCheck(const std::string& right) const  |  Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.
 public const std::string GetIssuedTo()  |  Obtient l’utilisateur associé au Gestionnaire de protection.
 public const std::string GetOwner()  |  Obtient l’adresse e-mail du propriétaire du contenu.
 public bool IsIssuedToOwner()  |  Obtient une valeur qui détermine si l’utilisateur actuel est le propriétaire du contenu.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  Obtient les détails de la protection.
 public const std::string GetContentId()  |  Obtient l’identificateur unique du document/contenu.
 public bool DoesUseDeprecatedAlgorithms()  |  Détermine si le Gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante.
 public bool IsAuditedExtractAllowed()  |  Détermine si le Gestionnaire de protection accorde le droit « audited extract » à l’utilisateur.
public const std::vector<uint8_t> GetSerializedPublishingLicense()  |  Sérialiser [ProtectionHandler](class_mip_protectionhandler.md) dans une licence de publication (PL)
  
## <a name="members"></a>Membres
  
### <a name="stream"></a>Flux
Créer un flux protégé, qui permet de chiffrer/déchiffrer le contenu.

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


* **isFinal** : détermine si la mémoire tampon d’entrée contient les octets du texte en clair final



  
**Retourne** : la taille réelle (en octets) du contenu chiffré
  
### <a name="decryptbuffer"></a>DecryptBuffer
Déchiffrer un tampon.

Paramètres :  
* **offsetFromStart** : position relative d’inputBuffer à partir du début du contenu chiffré 


* **inputBuffer** : mémoire tampon du contenu chiffré qui sera déchiffré 


* **inputBufferSize** : taille (en octets) de la mémoire tampon d’entrée 


* **outputBuffer** : mémoire tampon dans laquelle le contenu déchiffré sera copié 


* **outputBufferSize** : taille (en octets) de la mémoire tampon de sortie 


* **isFinal** : détermine si la mémoire tampon d’entrée contient les octets du texte chiffré final



  
**Retourne** : la taille réelle (en octets) du contenu déchiffré
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
Calcule la taille (en octets) du contenu s’il devait être chiffré avec ce [ProtectionHandler](class_mip_protectionhandler.md).

Paramètres :  
* **contentLength** : la taille (en octets) du contenu non protégé



  
**Retourne** : la taille (en octets) du contenu protégé
  
### <a name="getblocksize"></a>GetBlockSize
Obtient la taille de bloc (en octets) pour le mode de chiffrement utilisé par ce [ProtectionHandler](class_mip_protectionhandler.md).

  
**Retourne** : la taille (en octets) du bloc
  
### <a name="accesscheck"></a>AccessCheck
Vérifie si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié.

Paramètres :  
* **right** : droit à vérifier



  
**Retourne** : détermine si le Gestionnaire de protection accorde à l’utilisateur l’accès au droit spécifié
  
### <a name="getissuedto"></a>GetIssuedTo
Obtient l’utilisateur associé au Gestionnaire de protection.

  
**Retourne** : l’utilisateur associé au Gestionnaire de protection
  
### <a name="getowner"></a>GetOwner
Obtient l’adresse e-mail du propriétaire du contenu.

  
**Retourne** : l’adresse e-mail du propriétaire du contenu
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Obtient une valeur qui détermine si l’utilisateur actuel est le propriétaire du contenu.

  
**Retourne** : une valeur indiquant si l’utilisateur actuel est ou non le propriétaire du contenu.
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Obtient les détails de la protection.

  
**Retourne** : les détails de la protection
  
### <a name="getcontentid"></a>GetContentId
Obtient l’identificateur unique du document/contenu.

  
**Retourne** : l’identificateur unique du contenu
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Détermine si le Gestionnaire de protection utilise des algorithmes de chiffrement dépréciés (ECB) pour la compatibilité descendante.

  
**Retourne** : détermine si le Gestionnaire de protection utilise des algorithmes de chiffrement dépréciés
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Détermine si le Gestionnaire de protection accorde le droit « audited extract » à l’utilisateur.

  
**Retourne** : détermine si le Gestionnaire de protection accorde le droit « audited extract » à l’utilisateur
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
Sérialiser [ProtectionHandler](class_mip_protectionhandler.md) dans une licence de publication (PL)

  
**Retourne** : licence de publication sérialisée