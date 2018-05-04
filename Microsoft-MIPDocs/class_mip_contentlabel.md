# <a name="class-mipcontentlabel"></a>mip::ContentLabel, classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Outre les informations de l’étiquette, elle contient les propriétés d’une étiquette appliquée spécifique.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string & GetCreationTime | Obtenir l’heure de création de l’étiquette.
public AssignmentMethod GetAssignmentMethod | Obtenir la méthode d’assignation de l’étiquette.
public std::shared_ptr< Label > GetLabel | Obtient l’objet d’étiquette réel appliqué au contenu.
## <a name="members"></a>Membres
### <a name="getcreationtime"></a>GetCreationTime
Obtenir l’heure de création de l’étiquette.
#### <a name="returns"></a>Returns
Heure de création sous forme de chaîne gmt.
### <a name="getassignmentmethod"></a>GetAssignmentMethod
Obtenir la méthode d’assignation de l’étiquette.
#### <a name="returns"></a>Returns
Méthode d’assignation STANDARD | PRIVILEGED | AUTO. 
**Voir aussi** : mip::AssignmentMethod
### <a name="label"></a>Étiquette
Obtient l’objet d’étiquette réel appliqué au contenu.
#### <a name="returns"></a>Returns
Objet d’étiquette appliqué au contenu. 
**Voir aussi** : [mip::Label](#classmip_1_1_label)