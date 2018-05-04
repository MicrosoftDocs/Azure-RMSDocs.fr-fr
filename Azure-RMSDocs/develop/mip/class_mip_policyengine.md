# <a name="class-mippolicyengine"></a>mip::PolicyEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings & GetSettings public const std::vector< std::shared_ptr< Label > > & ListSensitivityLabels | Répertorier les étiquettes de sensibilité associées au moteur de stratégie.
public std::shared_ptr< ContentLabel > GetSensitivityLabelExecutionState & state) | Obtenir l’étiquette de sensibilité à partir du contenu existant.
public std::shared_ptr< Label > GetDefaultSensitivityLabel | Obtenir l’étiquette de sensibilité par défaut.
public std::vector< std::shared_ptr< Action > > ComputeActionsExecutionState & state) | Exécute les règles dans le moteur en fonction de l’état fourni et retourne la liste des actions à exécuter.
## <a name="members"></a>Membres
### <a name="settings"></a>Paramètres
Obtenir les [Settings](#classmip_1_1_policy_engine_1_1_settings) du moteur de stratégie.
#### <a name="returns"></a>Returns
les paramètres du moteur de stratégie. 
**Voir aussi** : [mip::PolicyEngine::Settings](#classmip_1_1_policy_engine_1_1_settings)
### <a name="label"></a>Label
répertorier les étiquettes de sensibilité associées au moteur de stratégie.
#### <a name="returns"></a>Returns
une liste d’étiquettes de sensibilité.
### <a name="contentlabel"></a>ContentLabel
Obtenir l’étiquette de sensibilité à partir du contenu existant.
Les informations requises pour récupérer l’étiquette sont obtenues à l’aide de l’état d’exécution fourni. 
#### <a name="parameters"></a>Paramètres
* state 
#### <a name="returns"></a>Returns
un objet d’étiquette de contenu qui contient l’étiquette de sensibilité et des informations supplémentaires. retourne une valeur vide en l’absence d’étiquette. 
**Voir aussi** : [mip::ContentLabel](#classmip_1_1_content_label).
### <a name="label"></a>Étiquette
Obtenir l’étiquette de sensibilité par défaut.
#### <a name="returns"></a>Returns
l’étiquette de sensibilité par défaut s’il y en a une, ou la valeur nullptr si aucune étiquette de sensibilité par défaut n’est définie.
### <a name="action"></a>Action
Exécute les règles dans le moteur en fonction de l’état fourni et retourne la liste des actions à exécuter.
#### <a name="parameters"></a>Paramètres
* state : état actuel de l’exécution du contenu auquel les règles sont appliquées. 
#### <a name="returns"></a>Returns
une liste des actions devant être appliquées au contenu.