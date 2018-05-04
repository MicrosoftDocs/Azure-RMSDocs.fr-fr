# <a name="class-mipaddwatermarkaction"></a>mip::AddWatermarkAction, classe 
Classe d’action qui spécifie l’ajout d’un filigrane.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string & GetUIElementName | API utilisée pour marquer l’élément de filigrane.
public WatermarkLayout GetLayout | API utilisée pour obtenir la disposition du filigrane.
public const std::string & GetText | Obtenir le texte devant être placé dans l’en-tête de contenu.
public const std::string & GetFontName | Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.
public int GetFontSize | Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.
public const std::string & GetFontColor | Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.
public ActionType GetType
## <a name="members"></a>Membres
### <a name="getuielementname"></a>GetUIElementName
API utilisée pour marquer l’élément de filigrane.
#### <a name="returns"></a>Returns
le nom à utiliser pour l’élément d’interface utilisateur qui contient le filigrane. Le même nom est retourné dans RemoveWatermarkingAction si le filigrane doit être supprimé.
### <a name="getlayout"></a>GetLayout
API utilisée pour obtenir la disposition du filigrane.
#### <a name="returns"></a>Returns
WatermarkLayout : disposition du filigrane sous forme d’enum HORIZONTAL|DIAGONAL. ,
### <a name="gettext"></a>GetText
Obtenir le texte devant être placé dans l’en-tête de contenu.
#### <a name="returns"></a>Returns
le texte de l’en-tête de contenu.
### <a name="getfontname"></a>GetFontName
Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.
#### <a name="returns"></a>Returns
le nom de la police, valeur par défaut si elle n’est pas définie par la stratégie Calibri.
### <a name="getfontsize"></a>GetFontSize
Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.
#### <a name="returns"></a>Returns
la taille de la police sous forme de nombre entier.
### <a name="getfontcolor"></a>GetFontColor
Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.
#### <a name="returns"></a>Returns
la couleur de la police sous forme de chaîne (par exemple, #000000).
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](#classmip_1_1_action).
#### <a name="returns"></a>Returns
Valeur ActionType qui détermine le type d’action dérivée vers lequel cette classe de base peut être castée.