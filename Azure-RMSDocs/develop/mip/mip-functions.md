# <a name="functions"></a>Fonctions

 Fonctions (étendue)                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier afin d’exporter les données de stratégie SCC.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nom du paramètre pour spécifier explicitement le chemin d’accès de fichier de données de stratégie.
public const std::string& GetCustomSettingPolicyDataName()       |  Nom du paramètre pour spécifier explicitement les données de stratégie.
**fonctions mip** |
public std::shared_ptr<mip::Stream> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::iostream>& stdIOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::istream>& stdIStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::ostream>& stdOStream)       |  Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.
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

  
## <a name="enumeration-details"></a>Détails de l'énumération
  
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

### <a name="mipstream-istream"></a>mip::Stream (istream)

Crée un [Flux](class_mip_stream.md) à partir d’un a std::istream.

Paramètres :  

* **stdIStream** : sauvegarde std::istream
  
**Renvoie** : [flux](class_mip_stream.md) incluant std::istream dans un wrapper
  
### <a name="mipstream-ostream"></a>mip::Stream (ostream)

Crée un [Flux](class_mip_stream.md) à partir d’un a std::ostream.

Paramètres :  
* **stdIStream** : sauvegarde std::ostream

  
**Renvoie** : [flux](class_mip_stream.md) incluant std::ostream dans un wrapper
  
### <a name="mipstream-iostream"></a>mip::Stream (iostream)

Crée un [Flux](class_mip_stream.md) à partir d’un a std::iostream.

Paramètres :  
* **stdIOStream** : sauvegarde std::iostream
  
**Renvoie** : [flux](class_mip_stream.md) incluant std::iostream dans un wrapper
  
### <a name="mipstream-buffer"></a>mip::Stream (buffer)

Crée un [Flux](class_mip_stream.md) à partir d’une mémoire tampon.

Paramètres :  
* **buffer** : pointeur vers une mémoire tampon

**Renvoie** : taille de mémoire tampon
  
## <a name="functions-miprights"></a>Fonctions (mip::rights)

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
  
### <a name="owner"></a>Propriétaire
Obtient un identificateur de chaîne pour un droit « propriétaire ».

  
**Renvoie** : identificateur de chaîne pour un droit « propriétaire »
  
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

  
**Renvoie** : identificateur de chaîne pour le rôle « auteur » Un auteur peut afficher, modifier, copier et imprimer le contenu.
  
### <a name="coowner"></a>Copropriétaire
Obtient un identificateur de chaîne pour un rôle « copropriétaire ».

  
**Renvoie** : identificateur de chaîne pour un rôle « copropriétaire » Un copropriétaire a toutes les autorisations

### <a name="reviewer"></a>Réviseur
Obtient un identificateur de chaîne pour un rôle « réviseur ».

  
**Renvoie** : identificateur de chaîne pour le rôle « réviseur » Un réviseur peut afficher et modifier le contenu. Ils ne peut ni le copier ni l’imprimer.

### <a name="viewer"></a>Observateur
Obtient un identificateur de chaîne pour un rôle « observateur ».

  
**Renvoie** : identificateur de chaîne pour un rôle « observateur » Un observateur peut uniquement afficher le contenu. Il ne peut ni le modifier, ni le copier, ni l’imprimer.
  
  
