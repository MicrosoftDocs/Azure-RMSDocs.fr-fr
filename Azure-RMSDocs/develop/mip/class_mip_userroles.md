# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Représente un groupe d’utilisateurs et les rôles qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public MIP_EXPORT UserRoles(const UserList& users, const RoleList& roles)  |  Constructeur [UserRoles](class_mip_userroles.md).
 public const UserList& Users() const  |  Obtient les utilisateurs associés à un ensemble de rôles.
 public const RoleList& Roles() const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles"></a>UserRoles
Constructeur [UserRoles](class_mip_userroles.md).

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes rôles 


* **roles** : [rôles](class_mip_roles.md) partagés par un groupe d’utilisateurs


  
### <a name="userlist"></a>UserList
Obtient les utilisateurs associés à un ensemble de rôles.

  
**Retourne** : les utilisateurs associés à un ensemble de rôles
  
### <a name="rolelist"></a>RoleList
Obtient les rôles associés à un groupe d’utilisateurs.

  
**Retourne** : les [rôles](class_mip_roles.md) associés à un groupe d’utilisateurs