# <a name="class-mipaddcontentheaderaction"></a>mip::AddContentHeaderAction, classe 
Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  API utilisée pour marquer l’élément d’en-tête de contenu.
 public const std::string& GetText() const  |  Obtenir le texte devant être placé dans l’en-tête de contenu.
 public const std::string& GetFontName() const  |  Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.
 public int GetFontSize() const  |  Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.
 public const std::string& GetFontColor() const  |  Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.
 public ContentMarkAlignment GetAlignment() const  |  Obtenir l’alignement de l’en-tête.
 public int GetMargin() const  |  Obtenir la marge de l’en-tête à partir du bas.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementname"></a>GetUIElementName
API utilisée pour marquer l’élément d’en-tête de contenu.

  
**Retourne** : le nom à utiliser pour l’élément d’interface utilisateur qui contient l’en-tête de contenu. Le même nom est retourné dans [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) si l’en-tête de contenu doit être supprimé.
  
### <a name="gettext"></a>GetText
Obtenir le texte devant être placé dans l’en-tête de contenu.

  
**Retourne** : le texte de l’en-tête de contenu.
  
### <a name="getfontname"></a>GetFontName
Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne** : le nom de la police, une valeur par défaut si elle n’est pas définie par la stratégie Calibri.
  
### <a name="getfontsize"></a>GetFontSize
Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne** : la taille de la police sous forme de nombre entier.
  
### <a name="getfontcolor"></a>GetFontColor
Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne** : la couleur de la police sous forme de chaîne (par exemple « #000000 »).
  
### <a name="getalignment"></a>GetAlignment
Obtenir l’alignement de l’en-tête.

  
**Retourne** : l’énumérateur ContentMarkAlignment, LEFT|RIGHT|CENTER. 
**Voir aussi** : ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
Obtenir la marge de l’en-tête à partir du bas.

  
**Retourne** : un nombre entier représentant les marges à partir du bas du document (par exemple 10 mm).
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.