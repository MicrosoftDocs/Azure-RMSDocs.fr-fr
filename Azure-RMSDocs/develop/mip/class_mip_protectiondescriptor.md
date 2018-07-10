# <a name="class-mipprotectiondescriptor"></a>class mip::ProtectionDescriptor 
Représente une stratégie ad hoc associée à du contenu protégé.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  Obtient le type de protection, issue du modèle de kit SDK de la protection ou pas.
 public const std::string& GetName() const  |  Obtient le nom de la stratégie.
 public const std::string& GetDescription() const  |  Obtient la description de la stratégie.
 public const std::string& GetTemplateId() const  |  Obtient l’ID du modèle de protection.
public const std::vector<UserRights>& GetUserRights() const  |  Obtient la collection de mappages utilisateurs-droits.
public const std::vector<UserRoles>& GetUserRoles() const  |  Obtient la collection de mappages utilisateurs-rôles.
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil() const  |  Obtient l’heure d’expiration de la stratégie.
 public bool DoesAllowOfflineAccess() const  |  Obtient une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.
 public const std::string& GetReferrer() const  |  Obtient l’adresse du référent de stratégie.
public const std::map<std::string, std::string>& GetEncryptedAppData() const  |  Obtient les données propres à l’application qui ont été chiffrées.
public const std::map<std::string, std::string>& GetSignedAppData() const  |  Obtient les données spécifiques de l’application qui ont été signées.
  
## <a name="members"></a>Membres
  
### <a name="protectiontype"></a>ProtectionType
Obtient le type de protection, issue du modèle de kit SDK de la protection ou pas.

  
**Retourne** : le type de protection
  
### <a name="getname"></a>GetName
Obtient le nom de la stratégie.

  
**Retourne** : le nom de la stratégie
  
### <a name="getdescription"></a>GetDescription
Obtient la description de la stratégie.

  
**Retourne** : la description de la stratégie
  
### <a name="gettemplateid"></a>GetTemplateId
Obtient l’ID du modèle de protection.

  
**Retourne** : l’ID du modèle
  
### <a name="userrights"></a>UserRights
Obtient la collection de mappages utilisateurs-droits.

  
**Retourne** : une collection de mappages utilisateurs-droits. La valeur de la propriété [UserRights](class_mip_userrights.md) est vide si l’utilisateur actif n’a pas accès aux informations sur les droits d’utilisateur (c’est-à-dire s’il n’est pas le propriétaire et qu’il ne dispose pas du droit VIEWRIGHTSDATA).
  
### <a name="userroles"></a>UserRoles
Obtient la collection de mappages utilisateurs-rôles.

  
**Retourne** : la collection de mappages utilisateurs-rôles
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtient l’heure d’expiration de la stratégie.

  
**Retourne** : l’heure d’expiration de la stratégie
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Obtient une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.

  
**Retourne** : une valeur indiquant si la stratégie autorise ou non l’accès au contenu hors connexion (par défaut = true)
  
### <a name="getreferrer"></a>GetReferrer
Obtient l’adresse du référent de stratégie.

  
**Retourne** : adresse du référent de la stratégie. Le référent est un URI qui peut être affiché à l’utilisateur en cas d’échec de l’acquisition de la stratégie. L’URI contient des informations indiquant de quelle façon cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
Obtient les données propres à l’application qui ont été chiffrées.

  
**Retourne** : données spécifiques à l’application Un [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire de données spécifiques à l’application qui ont été chiffrées par le service de protection. Ces données chiffrées sont indépendantes des données signées accessibles via [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata)
  
### <a name="getsignedappdata"></a>GetSignedAppData
Obtient les données spécifiques de l’application qui ont été signées.

  
**Retourne** : des données spécifiques à l’application. Un [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire des données spécifiques à l’application qui ont été signées par le service de protection. Ces données signées ne dépendent pas des données chiffrées accessibles par [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata)