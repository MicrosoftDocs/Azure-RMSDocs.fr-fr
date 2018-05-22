# <a name="class-mipuserrights"></a>mip::UserRights, classe 
Représente un groupe d’utilisateurs et les droits qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public UserRights(const UserList& users, const RightList& rights)  |  Constructeur [UserRights](class_mip_userrights.md).
 public const UserList& Users() const  |  Obtient les utilisateurs associés à un ensemble de droits.
 public const RightList& Rights() const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userrights"></a>UserRights
Constructeur [UserRights](class_mip_userrights.md).

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes droits 


* **rights** : droits partagés par le groupe d’utilisateurs


  
### <a name="userlist"></a>UserList
Obtient les utilisateurs associés à un ensemble de droits.

  
**Retourne** : les utilisateurs associés à un ensemble de droits
  
### <a name="rightlist"></a>RightList
Obtient les droits associés à un groupe d’utilisateurs.

  
**Retourne** : les droits associés à un groupe d’utilisateurs