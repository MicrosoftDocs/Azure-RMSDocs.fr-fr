# <a name="class-mipuserpolicy"></a>mip::UserPolicy, classe 
Représente la stratégie associée au contenu protégé.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public bool AccessCheck(const std::string& right) const  |  Vérifie si la stratégie accorde à l’utilisateur l’accès au droit spécifié.
 public UserPolicyType GetType()  |  Obtient le type de stratégie.
 public std::string GetName()  |  Obtient le nom de la stratégie.
 public std::string GetDescription()  |  Obtient la description de la stratégie.
public std::shared_ptr<TemplateDescriptor> GetTemplateDescriptor()  |  Obtient le [TemplateDescriptor](class_mip_templatedescriptor.md) pour une [UserPolicy](class_mip_userpolicy.md) basée sur des modèles.
public std::shared_ptr<PolicyDescriptor> GetPolicyDescriptor()  |  Obtient le [PolicyDescriptor](class_mip_policydescriptor.md) pour une [UserPolicy](class_mip_userpolicy.md) ad hoc.
 public std::string GetOwner()  |  Obtient l’adresse e-mail du propriétaire du contenu.
 public std::string GetIssuedTo()  |  Obtient l’utilisateur associé à la stratégie de protection.
 public bool IsIssuedToOwner()  |  Obtient une valeur qui détermine si l’utilisateur actuel est le propriétaire du contenu.
 public std::string GetContentId()  |  Obtient l’identificateur unique du document/contenu.
 public const mip::AppDataHashMap GetEncryptedAppData()  |  Obtient les données propres à l’application qui ont été chiffrées.
 public const mip::AppDataHashMap GetSignedAppData()  |  Obtient les données spécifiques de l’application qui ont été signées.
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil()  |  Obtient l’heure d’expiration de la stratégie.
 public bool DoesUseDeprecatedAlgorithms()  |  Obtient une valeur qui détermine si la stratégie utilise des algorithmes de chiffrement dépréciés pour la compatibilité descendante.
 public bool IsAuditedExtractAllowed()  |  Obtient une valeur qui détermine si la stratégie accorde le droit « audited extract » à l’utilisateur.
public const std::vector<unsigned char> GetSerializedPolicy()  |  Sérialiser [UserPolicy](class_mip_userpolicy.md) dans une licence de publication
public std::shared_ptr<rmscore::core::ProtectionPolicy> GetImpl()  |  Obtient l’implémentation de la classe dérivée interne de [UserPolicy](class_mip_userpolicy.md).
  
## <a name="members"></a>Membres
  
### <a name="accesscheck"></a>AccessCheck
Vérifie si la stratégie accorde à l’utilisateur l’accès au droit spécifié.

Paramètres :  
* **right** : droit à vérifier



  
**Retourne** : une valeur indiquant si la stratégie accorde ou non à l’utilisateur l’accès au droit spécifié
  
### <a name="userpolicytype"></a>UserPolicyType
Obtient le type de stratégie.

  
**Retourne** : le type de stratégie
  
### <a name="getname"></a>GetName
Obtient le nom de la stratégie.

  
**Retourne** : le nom de la stratégie
  
### <a name="getdescription"></a>GetDescription
Obtient la description de la stratégie.

  
**Retourne** : la description de la stratégie
  
### <a name="templatedescriptor"></a>TemplateDescriptor
Obtient le [TemplateDescriptor](class_mip_templatedescriptor.md) pour une [UserPolicy](class_mip_userpolicy.md) basée sur des modèles.

  
**Retourne** : [TemplateDescriptor](class_mip_templatedescriptor.md) si [UserPolicy](class_mip_userpolicy.md) est basé sur un modèle ; sinon, nullptr
  
### <a name="policydescriptor"></a>PolicyDescriptor
Obtient le [PolicyDescriptor](class_mip_policydescriptor.md) pour une [UserPolicy](class_mip_userpolicy.md) ad hoc.

  
**Retourne** : [PolicyDescriptor](class_mip_policydescriptor.md) si [UserPolicy](class_mip_userpolicy.md) est ad hoc ; sinon, nullptr
  
### <a name="getowner"></a>GetOwner
Obtient l’adresse e-mail du propriétaire du contenu.

  
**Retourne** : l’adresse e-mail du propriétaire du contenu
  
### <a name="getissuedto"></a>GetIssuedTo
Obtient l’utilisateur associé à la stratégie de protection.

  
**Retourne** : l’utilisateur associé à la stratégie de protection
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Obtient une valeur qui détermine si l’utilisateur actuel est le propriétaire du contenu.

  
**Retourne** : une valeur indiquant si l’utilisateur actuel est ou non le propriétaire du contenu.
  
### <a name="getcontentid"></a>GetContentId
Obtient l’identificateur unique du document/contenu.

  
**Retourne** : l’identificateur unique du contenu
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtient les données propres à l’application qui ont été chiffrées.
Une [UserPolicy](class_mip_userpolicy.md) peut contenir un dictionnaire des données propres à l’application qui ont été chiffrées par le service RMS. Ces données chiffrées ne dépendent pas des données signées accessibles par [UserPolicy::GetSignedAppData](class_mip_userpolicy.md#getsignedappdata)
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtient les données spécifiques de l’application qui ont été signées.
Une [UserPolicy](class_mip_userpolicy.md) peut contenir un dictionnaire des données propres à l’application qui ont été signées par le service RMS. Ces données signées ne dépendent pas des données chiffrées accessibles par [UserPolicy::GetEncryptedAppData](class_mip_userpolicy.md#getencryptedappdata)
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtient l’heure d’expiration de la stratégie.

  
**Retourne** : l’heure d’expiration de la stratégie
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Obtient une valeur qui détermine si la stratégie utilise des algorithmes de chiffrement dépréciés pour la compatibilité descendante.

  
**Retourne** : une valeur indiquant si la stratégie utilise ou non des algorithmes de chiffrement dépréciés
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Obtient une valeur qui détermine si la stratégie accorde le droit « audited extract » à l’utilisateur.

  
**Retourne** : une valeur indiquant si la stratégie accorde ou non le droit d’extraction avec audit (« audited extract ») à l’utilisateur
  
### <a name="getserializedpolicy"></a>GetSerializedPolicy
Sérialiser [UserPolicy](class_mip_userpolicy.md) dans une licence de publication

  
**Retourne** : [UserPolicy](class_mip_userpolicy.md) sérialisée
  
### <a name="getimpl"></a>GetImpl
Obtient l’implémentation de la classe dérivée interne de [UserPolicy](class_mip_userpolicy.md).

  
**Retourne** : une implémentation de la classe dérivée de [UserPolicy](class_mip_userpolicy.md) (interne uniquement)