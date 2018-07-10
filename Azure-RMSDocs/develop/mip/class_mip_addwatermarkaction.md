# <a name="class-mipaddwatermarkaction"></a>mip::AddWatermarkAction, classe 
Classe d’action qui spécifie l’ajout d’un filigrane.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  API utilisée pour marquer l’élément de filigrane.
 public WatermarkLayout GetLayout() const  |  API utilisée pour obtenir la disposition du filigrane.
 public const std::string& GetText() const  |  Obtenir le texte devant être placé dans le filigrane.
 public const std::string& GetFontName() const  |  Obtenir le nom de la police utilisée pour afficher le filigrane.
 public int GetFontSize() const  |  Obtenir la taille de la police utilisée pour afficher le filigrane.
 public const std::string& GetFontColor() const  |  Obtenir la couleur de la police utilisée pour afficher le filigrane.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementname"></a>GetUIElementName
API utilisée pour marquer l’élément de filigrane.

  
**Retourne** : le nom à utiliser pour l’élément d’interface utilisateur qui contient le filigrane. Le même nom est retourné dans RemoveWatermarkingAction si le filigrane doit être supprimé.
  
### <a name="getlayout"></a>GetLayout
API utilisée pour obtenir la disposition du filigrane.

  
**Retourne** : WatermarkLayout - la disposition du filigrane sous forme d’enum HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext"></a>GetText
Obtenir le texte devant être placé dans le filigrane.

  
**Retourne** : le texte de l’en-tête de contenu.
  
### <a name="getfontname"></a>GetFontName
Obtenir le nom de la police utilisée pour afficher le filigrane.

  
**Retourne** : le nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize"></a>GetFontSize
Obtenir la taille de la police utilisée pour afficher le filigrane.

  
**Retourne** : la taille de la police sous forme de nombre entier.
  
### <a name="getfontcolor"></a>GetFontColor
Obtenir la couleur de la police utilisée pour afficher le filigrane.

  
**Retourne** : la couleur de la police sous forme de chaîne (par exemple « #000000 »).
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.