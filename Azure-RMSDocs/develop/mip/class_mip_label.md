# <a name="class-miplabel"></a>mip::Label, classe 
Abstraction d’une étiquette unique Microsoft Information Protection.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string & GetId | Obtenir l’ID de l’étiquette.
public const std::string & GetName | Obtenir le nom de l’étiquette.
public const std::string & GetDescription | Obtenir la description de l’étiquette.
public const std::string & GetColor | Obtenir la couleur d’affichage de l’étiquette.
public const std::string & GetOrder | Obtenir l’ordre de l’étiquette.
public const std::string & GetTooltip | Obtenir la description de l’info-bulle de l’étiquette.
public bool IsActive | Obtient une valeur booléenne signalant si l’étiquette est active.
public std::weak_ptr< Label > GetParent | Obtenir l’étiquette parente.
public const std::vector< std::shared_ptr< Label > > & GetChildren | Obtenir les étiquettes enfants de l’étiquette actuelle.
## <a name="members"></a>Membres
### <a name="getid"></a>GetId
Obtenir l’ID de l’étiquette.
#### <a name="returns"></a>Retourne
l’ID de l’étiquette.
### <a name="getname"></a>GetName
Obtenir le nom de l’étiquette.
#### <a name="returns"></a>Retourne
le nom de l’étiquette.
### <a name="getdescription"></a>GetDescription
Obtenir la description de l’étiquette.
#### <a name="returns"></a>Retourne
la description de l’étiquette.
### <a name="getcolor"></a>GetColor
Obtenir la couleur d’affichage de l’étiquette.
#### <a name="returns"></a>Retourne
la valeur de couleur au format de chaîne. « #RRGGBB » où RR, GG et BB sont une valeur au format hexadécimal 0-f.
### <a name="getorder"></a>GetOrder
Obtenir l’ordre de l’étiquette.
#### <a name="returns"></a>Retourne
une valeur numérique attribuée en tant que chaîne.
### <a name="gettooltip"></a>GetTooltip
Obtenir la description de l’info-bulle de l’étiquette.
#### <a name="returns"></a>Retourne
une chaîne d’info-bulle.
### <a name="isactive"></a>IsActive
Obtient une valeur booléenne signalant si l’étiquette est active.
Seules les étiquettes actives peuvent être appliquées. Les étiquettes inactives ne peuvent pas être appliquées et sont utilisées uniquement à des fins d’affichage. 
#### <a name="returns"></a>Retourne
true si l’étiquette est active ; sinon, false.
### <a name="label"></a>Label
Obtenir l’étiquette parente.
#### <a name="returns"></a>Retourne
un pointeur faible vers l’étiquette parente si elle existe ; sinon, un pointeur vide.
### <a name="label"></a>Étiquette
Obtenir les étiquettes enfants de l’étiquette actuelle.
#### <a name="returns"></a>Retourne
un vecteur de pointeurs partagés vers des étiquettes.