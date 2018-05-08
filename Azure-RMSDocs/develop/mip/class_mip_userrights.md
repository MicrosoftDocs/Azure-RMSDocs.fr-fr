# <a name="class-mipuserrights"></a>mip::UserRights, classe 
Représente un groupe d’utilisateurs et les droits qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline UserRights(const UserList& users, const RightList& rights)  |  Constructeur [UserRights](#classmip_1_1_user_rights).
public inline const UserList& Users() const  |  Obtient les utilisateurs associés à un ensemble de droits.
public inline const RightList& Rights() const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userrights"></a>UserRights
Constructeur [UserRights](#classmip_1_1_user_rights).
  
#### <a name="parameters"></a>Paramètres
* users : groupe d’utilisateurs qui partagent les mêmes droits 
* rights : droits partagés par un groupe d’utilisateurs
  
### <a name="userlist"></a>UserList
Obtient les utilisateurs associés à un ensemble de droits.
  
#### <a name="returns"></a>Returns
Utilisateurs associés à un ensemble de droits
  
### <a name="rightlist"></a>RightList
Obtient les droits associés à un groupe d’utilisateurs.
  
#### <a name="returns"></a>Returns
Droits associés à un groupe d’utilisateurs