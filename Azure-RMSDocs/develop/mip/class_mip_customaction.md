# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](#classmip_1_1_custom_action) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector< std::pair< std::string, std::string > > & GetProperties | Obtenir la liste de paires clé/valeur des propriétés.
public ActionType GetType
## <a name="members"></a>Membres
### <a name="getproperties"></a>GetProperties
Obtenir la liste de paires clé/valeur des propriétés.
#### <a name="returns"></a>Returns
Liste de paires clé/valeur.
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](#classmip_1_1_action).
#### <a name="returns"></a>Returns
ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.