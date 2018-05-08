# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Représente un groupe d’utilisateurs et les rôles qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MIP_EXPORT UserRoles(const UserList& users, const RoleList& roles)  |  Constructeur [UserRoles](#classmip_1_1_user_roles).
public inline const UserList& Users() const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public inline const RoleList& Roles() const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles"></a>UserRoles
Constructeur [UserRoles](#classmip_1_1_user_roles).
  
#### <a name="parameters"></a>Paramètres
* users : groupe d’utilisateurs qui partagent les mêmes rôles 
* roles : [rôles](#classmip_1_1_roles) partagés par un groupe d’utilisateurs
  
### <a name="userlist"></a>UserList
Obtient les utilisateurs associés à un ensemble de rôles.
  
#### <a name="returns"></a>Returns
Utilisateurs associés à un ensemble de rôles
  
### <a name="rolelist"></a>RoleList
Obtient les rôles associés à un groupe d’utilisateurs.
  
#### <a name="returns"></a>Returns
[Rôles](#classmip_1_1_roles) associés à un groupe d’utilisateurs