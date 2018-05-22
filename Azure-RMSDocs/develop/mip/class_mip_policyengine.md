# <a name="class-mippolicyengine"></a>mip::PolicyEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtenir les [Settings](class_mip_policyengine_settings.md) du moteur de stratégie.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  répertorier les étiquettes de sensibilité associées au moteur de stratégie.
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  Obtenir l’étiquette de sensibilité à partir du contenu existant.
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  Obtenir l’étiquette de sensibilité par défaut.
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  Exécute les règles dans le moteur en fonction de l’état fourni et retourne la liste des actions à exécuter.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtenir les [Settings](class_mip_policyengine_settings.md) du moteur de stratégie.

  
**Retourne** : les paramètres du moteur de stratégie. 
**Voir aussi** : [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Étiquette
répertorier les étiquettes de sensibilité associées au moteur de stratégie.

  
**Retourne** : une liste d’étiquettes de sensibilité.
  
### <a name="contentlabel"></a>ContentLabel
Obtenir l’étiquette de sensibilité à partir du contenu existant.
Les informations requises pour récupérer l’étiquette sont obtenues à l’aide de l’état d’exécution fourni. 

Paramètres :  
* **state** : 



  
**Retourne** : un objet d’étiquette de contenu qui contient l’étiquette de sensibilité et des informations supplémentaires. retourne une valeur vide en l’absence d’étiquette. 
**Voir aussi** : [mip::ContentLabel](class_mip_contentlabel.md).
  
### <a name="label"></a>Étiquette
Obtenir l’étiquette de sensibilité par défaut.

  
**Retourne** : l’étiquette de sensibilité par défaut si elle existe, ou la valeur nullptr si aucune étiquette de sensibilité par défaut n’est définie.
  
### <a name="action"></a>Action
Exécute les règles dans le moteur en fonction de l’état fourni et retourne la liste des actions à exécuter.

Paramètres :  
* **state** : état actuel de l’exécution du contenu auquel les règles sont appliquées. 



  
**Retourne** : une liste des actions à appliquer au contenu.