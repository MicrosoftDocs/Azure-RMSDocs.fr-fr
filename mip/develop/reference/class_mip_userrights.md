# <a name="class-mipuserrights"></a>mip::UserRights, classe 
Représente un groupe d’utilisateurs et les droits qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRights(const std::vector<std::string>& users, const std::vector<std::string>& rights)  |  Constructeur [UserRights](class_mip_userrights.md).
public const std::vector<std::string>& Users() const  |  Obtient les utilisateurs associés à un ensemble de droits.
public const std::vector<std::string>& Rights() const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userrights"></a>UserRights
Constructeur [UserRights](class_mip_userrights.md).

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes droits 


* **rights** : droits partagés par le groupe d’utilisateurs


  
### <a name="users"></a>Utilisateurs
Obtient les utilisateurs associés à un ensemble de droits.

  
**Retourne** : les utilisateurs associés à un ensemble de droits
  
### <a name="rights"></a>Droits
Obtient les droits associés à un groupe d’utilisateurs.

  
**Retourne** : les droits associés à un groupe d’utilisateurs