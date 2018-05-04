# <a name="class-mippolicydescriptor"></a>mip::PolicyDescriptor, classe 
Représente une stratégie ad hoc associée à du contenu protégé.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string & GetName | Obtient le nom de la stratégie.
public void SetName | Définit le nom de la stratégie.
public const std::string & GetDescription | Obtient la description de la stratégie.
public void SetDescription | Définit la description de la stratégie.
public const std::vector< UserRights > & GetUserRightsList | Obtient la collection de mappages utilisateurs-droits.
public const std::vector< mip::UserRoles > & GetUserRolesList | Obtient la collection de mappages utilisateurs-rôles.
public const std::chrono::time_point< std::chrono::system_clock > & GetContentValidUntil | Obtient l’heure d’expiration de la stratégie.
public void SetContentValidUntil | Définit l’heure d’expiration de la stratégie.
public bool DoesAllowOfflineAccess | Obtient une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.
public void SetAllowOfflineAccess | Définit une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.
public const std::string & GetReferrer | Obtient l’adresse du référent de stratégie.
public void SetReferrer | Définit l’adresse du référent de stratégie.
public const AppDataHashMap & GetEncryptedAppData | Obtient les données spécifiques de l’application qui ont été chiffrées.
public void SetEncryptedAppDataAppDataHashMap & value) | Définit les données spécifiques de l’application qui doivent être chiffrées.
public const AppDataHashMap & GetSignedAppData | Obtient les données spécifiques de l’application qui ont été signées.
public void SetSignedAppDataAppDataHashMap & value) | Définit les données spécifiques de l’application qui doivent être signées.
## <a name="members"></a>Membres
### <a name="getname"></a>GetName
Obtient le nom de la stratégie.
#### <a name="returns"></a>Returns
Nom de la stratégie
### <a name="setname"></a>SetName
Définit le nom de la stratégie.
#### <a name="parameters"></a>Paramètres
* value : nom de la stratégie
### <a name="getdescription"></a>GetDescription
Obtient la description de la stratégie.
#### <a name="returns"></a>Returns
Description de la stratégie
### <a name="setdescription"></a>SetDescription
Définit la description de la stratégie.
#### <a name="parameters"></a>Paramètres
* value : description de la stratégie
### <a name="userrights"></a>UserRights
Obtient la collection de mappages utilisateurs-droits.
#### <a name="returns"></a>Returns
Collection de mappages utilisateurs-droits. La valeur de la propriété UserRightsList est vide si l’utilisateur actuel n’a pas accès aux informations sur les droits d’utilisateur (c’est-à-dire s’il n’est pas le propriétaire et qu’il ne dispose pas du droit VIEWRIGHTSDATA).
### <a name="mipuserroles"></a>mip::UserRoles
Obtient la collection de mappages utilisateurs-rôles.
#### <a name="returns"></a>Returns
Collection de mappages utilisateurs-rôles
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtient l’heure d’expiration de la stratégie.
#### <a name="returns"></a>Returns
Heure d’expiration de la stratégie
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Définit l’heure d’expiration de la stratégie.
#### <a name="parameters"></a>Paramètres
* value : heure d’expiration de la stratégie
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Obtient une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.
#### <a name="returns"></a>Returns
Une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion (par défaut = true)
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Définit une valeur indiquant si la stratégie autorise l’accès au contenu hors connexion.
#### <a name="parameters"></a>Paramètres
* value : valeur indiquant si la stratégie autorise l’accès au contenu hors connexion
### <a name="getreferrer"></a>GetReferrer
Obtient l’adresse du référent de stratégie.
#### <a name="returns"></a>Returns
Adresse du référent de la stratégie. Le référent est un URI qui peut être affiché à l’utilisateur en cas d’échec de l’acquisition de la stratégie. L’URI contient des informations indiquant de quelle façon cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
### <a name="setreferrer"></a>SetReferrer
Définit l’adresse du référent de stratégie.
#### <a name="parameters"></a>Paramètres
* uri : adresse du référent de la stratégie. Le référent est un URI qui peut être affiché à l’utilisateur en cas d’échec de l’acquisition de la stratégie. L’URI contient des informations indiquant de quelle façon cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
### <a name="appdatahashmap"></a>AppDataHashMap
Obtient les données spécifiques de l’application qui ont été chiffrées.
#### <a name="returns"></a>Returns
Données spécifiques de l’application. Une [UserPolicy](#classmip_1_1_user_policy) peut contenir un dictionnaire des données spécifiques de l’application qui ont été chiffrées par le service RMS. Ces données chiffrées ne dépendent pas des données signées accessibles par [PolicyDescriptor::GetSignedAppData](#classmip_1_1_policy_descriptor_1ad523870efc92f9f81c82121a054d74d4)
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Définit les données spécifiques de l’application qui doivent être chiffrées.
#### <a name="parameters"></a>Paramètres
* value : données spécifiques de l’application. Une application peut spécifier un dictionnaire des données spécifiques de l’application qui seront chiffrées par le service RMS. Ces données chiffrées ne dépendent pas des données signées définies par [PolicyDescriptor::SetSignedAppData](#classmip_1_1_policy_descriptor_1a00f35c0b91e48ccdcc6387466a61f362).
### <a name="appdatahashmap"></a>AppDataHashMap
Obtient les données spécifiques de l’application qui ont été signées.
#### <a name="returns"></a>Returns
Données spécifiques de l’application. Une [UserPolicy](#classmip_1_1_user_policy) peut contenir un dictionnaire des données spécifiques de l’application qui ont été signées par le service RMS. Ces données signées ne dépendent pas des données chiffrées accessibles par [PolicyDescriptor::GetEncryptedAppData](#classmip_1_1_policy_descriptor_1a9a5bcf9d1bf7357de549429179197ab6)
### <a name="setsignedappdata"></a>SetSignedAppData
Définit les données spécifiques de l’application qui doivent être signées.
#### <a name="parameters"></a>Paramètres
* value : données spécifiques de l’application. Une application peut spécifier un dictionnaire des données spécifiques de l’application qui seront signées par le service RMS. Ces données signées ne dépendent pas des données chiffrées définies par [PolicyDescriptor::SetEncryptedAppData](#classmip_1_1_policy_descriptor_1a5275224932dc17319092304497e59eb2).