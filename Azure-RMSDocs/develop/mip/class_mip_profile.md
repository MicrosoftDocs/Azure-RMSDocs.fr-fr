# <a name="class-mipprofile"></a>mip::Profile, classe 
La classe [Profile](#classmip_1_1_profile) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [Profile](#classmip_1_1_profile), mais elle peut créer plusieurs profils si nécessaire.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtenir les paramètres définis sur le profil.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Démarre l’ajout d’un nouveau moteur de stratégie au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront entièrement supprimées.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtenir les paramètres définis sur le profil.
  
#### <a name="returns"></a>Returns
les paramètres définis sur le profil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Démarre une opération d’énumération de moteurs.
  
#### <a name="parameters"></a>Paramètres
* context : paramètre qui sera passé dans les fonctions de l’observateur. 
[Profile::Observer](#classmip_1_1_profile_1_1_observer) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
  
#### <a name="parameters"></a>Paramètres
* id : ID de moteur unique. 
* context : paramètre qui sera passé dans les fonctions de l’observateur. 
[Profile::Observer](#classmip_1_1_profile_1_1_observer) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync"></a>AddEngineAsync
Démarre l’ajout d’un nouveau moteur de stratégie au profil.
  
#### <a name="parameters"></a>Paramètres
* settings : objet [mip::PolicyEngine::Settings](#classmip_1_1_policy_engine_1_1_settings) qui spécifie les paramètres de moteur. 
* context : paramètre qui sera passé dans les fonctions de l’observateur. 
[Profile::Observer](#classmip_1_1_profile_1_1_observer) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront entièrement supprimées.
  
#### <a name="parameters"></a>Paramètres
* id : ID de moteur unique. 
* context : paramètre qui sera passé dans les fonctions de l’observateur. 
[Profile::Observer](#classmip_1_1_profile_1_1_observer) est appelé en cas de réussite ou d’échec.