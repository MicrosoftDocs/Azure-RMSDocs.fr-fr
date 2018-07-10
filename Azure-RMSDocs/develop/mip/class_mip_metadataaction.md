# <a name="class-mipmetadataaction"></a>mip::MetadataAction, classe 
Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  Obtenir la liste des métadonnées sous forme de paires clé-valeur. Les métadonnées doivent être ajoutées aux métadonnées de contenu.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne** : un vecteur de chaînes à supprimer. La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
Obtenir la liste des métadonnées sous forme de paires clé-valeur. Les métadonnées doivent être ajoutées aux métadonnées de contenu.

  
**Retourne** : Const std::vector<std::pair<std::string, std::string>>& La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.