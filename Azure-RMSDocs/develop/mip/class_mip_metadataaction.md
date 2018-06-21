# <a name="class-mipmetadataaction"></a>mip::MetadataAction, classe 
[Action](class_mip_action.md) utilisée pour spécifier les informations de métadonnées à ajouter au contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  Obtenir la liste des métadonnées sous forme de paires clé-valeur. Les métadonnées doivent être ajoutées aux métadonnées de contenu.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne** : un vecteur de chaînes à supprimer. Cette suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
Obtenir la liste des métadonnées sous forme de paires clé-valeur. Les métadonnées doivent être ajoutées aux métadonnées de contenu.

  
**Retourne** : const std::vector<std::pair<std::string, std::string>>& La suppression des métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.