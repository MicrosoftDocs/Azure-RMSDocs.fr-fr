# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Représente un groupe d’utilisateurs et les rôles qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector<std::string>& users, const std::vector<std::string>& roles)  |  Constructeur [UserRoles](class_mip_userroles.md).
public const std::vector<std::string>& Users() const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public const std::vector<std::string>& Roles() const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles"></a>UserRoles
Constructeur [UserRoles](class_mip_userroles.md).

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes rôles 


* **roles** : rôles partagés par un groupe d’utilisateurs


  
### <a name="users"></a>Utilisateurs
Obtient les utilisateurs associés à un ensemble de rôles.

  
**Retourne** : les utilisateurs associés à un ensemble de rôles
  
### <a name="roles"></a>Rôles
Obtient les rôles associés à un groupe d’utilisateurs.

  
**Retourne** : les rôles associés à un groupe d’utilisateurs