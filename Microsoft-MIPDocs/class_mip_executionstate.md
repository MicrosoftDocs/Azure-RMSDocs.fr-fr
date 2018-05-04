# <a name="class-mipexecutionstate"></a>mip::ExecutionState, classe 
Interface pour tous les états nécessaires à l’exécution du moteur.
Les clients doivent uniquement appeler les méthodes pour obtenir l’état qui est nécessaire. Ainsi, pour des raisons d’efficacité, les clients peuvent implémenter cette interface afin que l’état correspondant soit calculé de façon dynamique plutôt qu’en avance.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId | Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
public bool IsDowngradeJustified | L’implémentation doit passer une valeur qui indique si une justification du passage d’une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod | Obtenir la méthode d’assignation de la nouvelle étiquette.
public std::vector< std::pair< std::string, std::string > > GetContentMetadata | Obtenir les éléments de métadonnées à partir du contenu.
public std::string GetTemplateId | Obtient l’ID du modèle de protection du service Rights Management.
public ContentFormat GetContentFormat | Obtient le format du contenu.
public const ActionType GetSupportedActions
## <a name="members"></a>Membres
### <a name="getnewlabelid"></a>GetNewLabelId
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
#### <a name="returns"></a>Returns
ID de l’étiquette de sensibilité à appliquer au contenu si une étiquette a été définie ; sinon, valeur vide pour supprimer l’étiquette.
### <a name="isdowngradejustified"></a>IsDowngradeJustified
L’implémentation doit passer, qu’une justification de rétrogradation d’une étiquette existante ait été donnée ou non.
#### <a name="returns"></a>Returns
true si le passage à une version antérieure a déjà été justifié ; sinon, false. 
**Voir aussi** : [mip::JustifyAction](#classmip_1_1_justify_action)
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Obtenir la méthode d’assignation de la nouvelle étiquette.
#### <a name="returns"></a>Returns
Méthode d’assignation STANDARD, PRIVILEGED, AUTO. 
**Voir aussi** : mip::AssignmentMethod
### <a name="getcontentmetadata"></a>GetContentMetadata
Obtenir les éléments de métadonnées à partir du contenu.
#### <a name="returns"></a>Returns
Vecteur de paires clé/valeur représentant les métadonnées appliquées au contenu. Chaque élément de métadonnées est une paire nom/valeur.
### <a name="gettemplateid"></a>GetTemplateId
Obtient l’ID du modèle de protection du service Rights Management.
#### <a name="returns"></a>Returns
ID du modèle de protection du service Rights Management si un modèle a été défini ; sinon, chaîne vide sous la forme d’un GUID sans accolades.
### <a name="getcontentformat"></a>GetContentFormat
Obtient le format du contenu.
#### <a name="returns"></a>Returns
DEFAULT, EMAIL **Voir aussi** : mip::ContentFormat
### <a name="actiontype"></a>ActionType
Retourner une liste d’actions que l’application prend en charge. Tous les types d’actions sont répertoriés dans [mip/upe/action.h](#action_8h).