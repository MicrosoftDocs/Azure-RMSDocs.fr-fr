# <a name="class-mipprofile"></a>mip::Profile, classe 
La classe [Profile](class_mip_profile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [Profile](class_mip_profile.md), mais elle peut créer plusieurs profils si nécessaire.
  
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

  
**Retourne** : paramètres définis sur le profil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[Profile::Observer](class_mip_profile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[Profile::Observer](class_mip_profile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync"></a>AddEngineAsync
Démarre l’ajout d’un nouveau moteur de stratégie au profil.

Paramètres :  
* **settings** : objet [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) qui spécifie les paramètres du moteur. 


* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[Profile::Observer](class_mip_profile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront entièrement supprimées.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[Profile::Observer](class_mip_profile_observer.md) est appelé en cas de réussite ou d’échec.