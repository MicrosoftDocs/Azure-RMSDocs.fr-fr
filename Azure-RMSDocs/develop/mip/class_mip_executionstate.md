# <a name="class-mipexecutionstate"></a>mip::ExecutionState, classe 
Interface pour tous les états nécessaires à l’exécution du moteur.
Les clients doivent uniquement appeler les méthodes pour obtenir l’état qui est nécessaire. Ainsi, pour des raisons d’efficacité, les clients peuvent implémenter cette interface afin que l’état correspondant soit calculé de façon dynamique plutôt qu’en avance.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
 public bool IsDowngradeJustified() const  |  L’implémentation doit passer, qu’une justification de rétrogradation d’une étiquette existante ait été donnée ou non.
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
 public std::string GetTemplateId() const  |  Obtient l’ID du modèle de protection du service Rights Management.
 public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
 public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui représente tous les types d’action pris en charge.
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  Retourne un mappage des résultats de la classification.
  
## <a name="members"></a>Membres
  
### <a name="getnewlabelid"></a>GetNewLabelId
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.

  
**Retourne** : l’ID de l’étiquette de sensibilité à appliquer au contenu si une étiquette a été définie ; sinon, une valeur vide pour supprimer l’étiquette.
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
L’implémentation doit passer, qu’une justification de rétrogradation d’une étiquette existante ait été donnée ou non.

  
**Retourne** : true si le passage à une version antérieure a déjà été justifié ; sinon, false. 
  
**Voir aussi** : [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Obtenir la méthode d’assignation de la nouvelle étiquette.

  
**Retourne** : la méthode d’affectation STANDARD, PRIVILEGED, AUTO. 
  
**Voir aussi** : mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
Retourner les propriétés étendues de la nouvelle étiquette.

  
**Retourne** : un vecteur de paires clé/valeur représentant les propriétés étendues appliquées au contenu.
  
### <a name="getcontentmetadata"></a>GetContentMetadata
Obtenir les éléments de métadonnées à partir du contenu.

  
**Retourne** : un vecteur de paires clé/valeur représentant les métadonnées appliquées au contenu. Chaque élément de métadonnées est une paire nom/valeur.
  
### <a name="gettemplateid"></a>GetTemplateId
Obtient l’ID du modèle de protection du service Rights Management.

  
**Retourne** : l’ID du modèle de protection du service Rights Management s’il existe, sous la forme d’un GUID sans accolades ; sinon, une chaîne vide.
  
### <a name="getcontentformat"></a>GetContentFormat
Obtient le format du contenu.

  
**Retourne** : DEFAULT, EMAIL 
  
**Voir aussi** : mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
Obtient une énumération masquée qui représente tous les types d’action pris en charge.

  
**Retourne**  : une énumération masquée qui représente tous les types d’action pris en charge.
  
### <a name="classificationresult"></a>ClassificationResult
Retourne un mappage des résultats de la classification.

Paramètres :  
* **classificationId** : une liste des ID de classification. 



  
**Retourne** : une liste des résultats de la classification.