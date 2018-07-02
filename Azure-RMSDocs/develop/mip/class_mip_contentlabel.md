# <a name="class-mipcontentlabel"></a>mip::ContentLabel, classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Outre les informations de l’étiquette, elle contient les propriétés d’une étiquette appliquée spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  Obtenir l’heure de création de l’étiquette.
 public AssignmentMethod GetAssignmentMethod() const  |  Obtenir la méthode d’assignation de l’étiquette.
public std::shared_ptr<Label> GetLabel() const  |  Obtient l’objet d’étiquette réel appliqué au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getcreationtime"></a>GetCreationTime
Obtenir l’heure de création de l’étiquette.

  
**Retourne** : heure de création sous forme de chaîne GMT.
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
Obtenir la méthode d’assignation de l’étiquette.

  
**Retourne** : Méthode d’affectation STANDARD | PRIVILEGED | AUTO. 
  
**Voir aussi** : mip::AssignmentMethod
  
### <a name="label"></a>Étiquette
Obtient l’objet d’étiquette réel appliqué au contenu.

  
**Retourne** : l’objet d’étiquette appliqué au contenu. 
  
**Voir aussi** : [mip::Label](class_mip_label.md)