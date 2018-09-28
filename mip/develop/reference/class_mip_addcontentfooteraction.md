# <a name="class-mipaddcontentfooteraction"></a>mip::AddContentFooterAction, classe 
Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  API utilisée pour marquer l’élément de pied de page de contenu.
 public const std::string& GetText() const  |  Obtenir le texte devant être placé dans le pied de page de contenu.
 public const std::string& GetFontName() const  |  Obtenir le nom de la police utilisée pour afficher le pied de page de contenu.
 public int GetFontSize() const  |  Obtenir la taille de la police utilisée pour afficher le pied de page de contenu.
 public const std::string& GetFontColor() const  |  Obtenir la couleur de la police utilisée pour afficher le pied de page de contenu.
 public ContentMarkAlignment GetAlignment() const  |  Obtenir l’alignement du pied de page.
 public int GetMargin() const  |  Obtenir la marge du pied de page à partir du bas.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementname"></a>GetUIElementName
API utilisée pour marquer l’élément de pied de page de contenu.

  
**Retourne** : le nom à utiliser pour l’élément d’interface utilisateur qui contient le pied de page de contenu. Le même nom est retourné dans [RemoveContentFooterAction](class_mip_removecontentfooteraction.md) si le pied de page de contenu doit être supprimé.
  
### <a name="gettext"></a>GetText
Obtenir le texte devant être placé dans le pied de page de contenu.

  
**Retourne** : le texte du pied de page de contenu.
  
### <a name="getfontname"></a>GetFontName
Obtenir le nom de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne** : le nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize"></a>GetFontSize
Obtenir la taille de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne** : la taille de la police sous forme de nombre entier.
  
### <a name="getfontcolor"></a>GetFontColor
Obtenir la couleur de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne** : la couleur de la police sous forme de chaîne (par exemple « #000000 »).
  
### <a name="getalignment"></a>GetAlignment
Obtenir l’alignement du pied de page.

  
**Retourne** : l’énumérateur ContentMarkAlignment : LEFT|RIGHT|CENTER. 
  
**Voir aussi** : ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
Obtenir la marge du pied de page à partir du bas.

  
**Retourne** : un nombre entier représentant les marges à partir du bas du document (par exemple 10 mm).
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.