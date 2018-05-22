# <a name="class-mippolicydescriptor"></a>mip::PolicyDescriptor, classe 
Représente une stratégie ad hoc associée à du contenu protégé.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetName()  |  Obtient le nom de la stratégie.
 public void SetName(const std::string& value)  |  Définit le nom de la stratégie.
 public const std::string& GetDescription()  |  Obtient la description de la stratégie.
 public void SetDescription(const std::string& value)  |  Définit la description de la stratégie.
public const std::vector<UserRights>& GetUserRightsList() const  |  Obtient la collection de mappages utilisateurs-droits.
public const std::vector<mip::UserRoles>& GetUserRolesList()  |  Obtient la collection de mappages utilisateurs-rôles.
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil()  |  Obtient l’heure d’expiration de la stratégie.
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  Définit l’heure d’expiration de la stratégie.
 public bool DoesAllowOfflineAccess()  |  Obtient une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.
 public void SetAllowOfflineAccess(bool value)  |  Définit une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.
 public const std::string& GetReferrer() const  |  Obtient l’adresse du référent de stratégie.
 public void SetReferrer(const std::string& uri)  |  Définit l’adresse du référent de stratégie.
 public const AppDataHashMap& GetEncryptedAppData()  |  Obtient les données propres à l’application qui ont été chiffrées.
 public void SetEncryptedAppData(const AppDataHashMap& value)  |  Définit les données spécifiques de l’application qui doivent être chiffrées.
 public const AppDataHashMap& GetSignedAppData()  |  Obtient les données spécifiques de l’application qui ont été signées.
 public void SetSignedAppData(const AppDataHashMap& value)  |  Définit les données spécifiques de l’application qui doivent être signées.
  
## <a name="members"></a>Membres
  
### <a name="getname"></a>GetName
Obtient le nom de la stratégie.

  
**Retourne** : le nom de la stratégie
  
### <a name="setname"></a>SetName
Définit le nom de la stratégie.

Paramètres :  
* **value** : nom de la stratégie


  
### <a name="getdescription"></a>GetDescription
Obtient la description de la stratégie.

  
**Retourne** : la description de la stratégie
  
### <a name="setdescription"></a>SetDescription
Définit la description de la stratégie.

Paramètres :  
* **value** : description de la stratégie


  
### <a name="userrights"></a>UserRights
Obtient la collection de mappages utilisateurs-droits.

  
**Retourne** : une collection de mappages utilisateurs-droits. La valeur de la propriété UserRightsList est vide si l’utilisateur actif n’a pas accès aux informations sur les droits d’utilisateur (c’est-à-dire s’il n’est pas le propriétaire et qu’il ne dispose pas du droit VIEWRIGHTSDATA).
  
### <a name="mipuserroles"></a>mip::UserRoles
Obtient la collection de mappages utilisateurs-rôles.

  
**Retourne** : la collection de mappages utilisateurs-rôles
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtient l’heure d’expiration de la stratégie.

  
**Retourne** : l’heure d’expiration de la stratégie
  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Définit l’heure d’expiration de la stratégie.

Paramètres :  
* **value** : heure d’expiration de la stratégie


  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Obtient une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.

  
**Retourne** : une valeur indiquant si la stratégie autorise ou non l’accès au contenu hors connexion (par défaut = true)
  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Définit une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.

Paramètres :  
* **value** : valeur indiquant si la stratégie autorise ou non l’accès au contenu hors connexion


  
### <a name="getreferrer"></a>GetReferrer
Obtient l’adresse du référent de stratégie.

  
**Retourne** : adresse du référent de la stratégie. Le référent est un URI qui peut être affiché à l’utilisateur en cas d’échec de l’acquisition de la stratégie. L’URI contient des informations indiquant de quelle façon cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="setreferrer"></a>SetReferrer
Définit l’adresse du référent de stratégie.

Paramètres :  
* **uri** : adresse du référent de la stratégie


Le référent est un URI qui peut être montré à l’utilisateur en cas d’échec de l’acquisition de la stratégie. L’URI contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="appdatahashmap"></a>AppDataHashMap
Obtient les données propres à l’application qui ont été chiffrées.

  
**Retourne** : des données spécifiques à l’application. Une [UserPolicy](class_mip_userpolicy.md) peut contenir un dictionnaire des données spécifiques à l’application qui ont été chiffrées par le service RMS. Ces données chiffrées ne dépendent pas des données signées accessibles par [PolicyDescriptor::GetSignedAppData](class_mip_policydescriptor.md#getsignedappdata)
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Définit les données spécifiques de l’application qui doivent être chiffrées.

Paramètres :  
* **value** : données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront chiffrées par le service RMS. Ces données chiffrées ne dépendent pas des données signées définies par [PolicyDescriptor::SetSignedAppData](class_mip_policydescriptor.md#setsignedappdata).
  
### <a name="appdatahashmap"></a>AppDataHashMap
Obtient les données spécifiques de l’application qui ont été signées.

  
**Retourne** : des données spécifiques à l’application. Une [UserPolicy](class_mip_userpolicy.md) peut contenir un dictionnaire des données spécifiques à l’application qui ont été signées par le service RMS. Ces données signées ne dépendent pas des données chiffrées accessibles par [PolicyDescriptor::GetEncryptedAppData](class_mip_policydescriptor.md#getencryptedappdata)
  
### <a name="setsignedappdata"></a>SetSignedAppData
Définit les données spécifiques de l’application qui doivent être signées.

Paramètres :  
* **value** : données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront signées par le service RMS. Ces données signées ne dépendent pas des données chiffrées définies par [PolicyDescriptor::SetEncryptedAppData](class_mip_policydescriptor.md#setencryptedappdata).