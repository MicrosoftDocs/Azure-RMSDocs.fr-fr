# <a name="class-mipremovecontentfooteraction"></a>mip::RemoveContentFooterAction, classe 
Classe d’action qui spécifie la suppression du pied de page de contenu du document.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector< std::string > & GetUIElementNames | Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
public ActionType GetType
## <a name="members"></a>Membres
### <a name="getuielementnames"></a>GetUIElementNames
Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
#### <a name="returns"></a>Returns
Liste de noms d’éléments d’interface utilisateur.
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](#classmip_1_1_action).
#### <a name="returns"></a>Returns
Valeur ActionType qui détermine le type d’action dérivée vers lequel cette classe de base peut être castée.