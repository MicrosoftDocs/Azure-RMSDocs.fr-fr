# <a name="class-mipfileenginesettings"></a>mip::FileEngine::Settings, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Crée une instance avec les paramètres donnés.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Crée une instance avec les paramètres donnés.
 public const std::string& GetEngineId() const  |  Retourne l’ID du moteur.
 public const Identity& GetIdentity() const  |  Retourne l’identité du moteur.
 public void SetIdentity(const Identity& identity)  |  Définit l’identité du moteur.
 public const std::string& GetClientData() const  |  Retourne les données clientes du moteur.
 public const std::string& GetLocale() const  |  Retourne les paramètres régionaux du moteur.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
 public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur.
 public const std::string& GetSessionId() const  |  Retourne l’ID de session du moteur.
 public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison du cloud de protection, utilisée pour spécifier la limite du cloud.
 public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Obtient cloudEndpointBaseUrl.
 public void SetProtectionOnlyEngine(const bool protectionOnly)  |  Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
 public const bool IsProtectionOnlyEngine() const  |  Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Crée une instance avec les paramètres donnés.
Sert à créer [Settings](class_mip_fileengine_settings.md) pour appeler LoadEngineAsync afin de charger un moteur existant (précédemment ajouté avec AddEngineAsync).

Paramètres :  
* **engineId**  : affectez à ce paramètre l’ID de moteur unique généré par AddEngineAsync.


  
### <a name="settings"></a>Paramètres
Crée une instance avec les paramètres donnés.
Sert à créer [Settings](class_mip_fileengine_settings.md) pour appeler AddEngineAsync afin d’ajouter un nouveau moteur.

Paramètres :  
* **identity** : informations sur l’identité de l’utilisateur pour lequel le moteur doit être ajouté.


  
### <a name="getengineid"></a>GetEngineId
Retourne l’ID du moteur.
  
### <a name="getidentity"></a>GetIdentity
Retourne l’identité du moteur.
  
### <a name="setidentity"></a>SetIdentity
Définit l’identité du moteur.
  
### <a name="getclientdata"></a>GetClientData
Retourne les données clientes du moteur.
  
### <a name="getlocale"></a>GetLocale
Retourne les paramètres régionaux du moteur.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
  
### <a name="getcustomsettings"></a>SetCustomSettings
Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
  
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de session du moteur.
  
### <a name="getsessionid"></a>GetSessionId
Retourne l’ID de session du moteur.
  
### <a name="setprotectioncloudendpointbaseurl"></a>SetProtectionCloudEndpointBaseUrl
Définit l’URL de base du point de terminaison du cloud de protection, utilisée pour spécifier la limite du cloud.

Paramètres :  
* **protectionCloudEndpointBaseUrl** : URL de base associée aux points de terminaison de protection


  
### <a name="getprotectioncloudendpointbaseurl"></a>GetProtectionCloudEndpointBaseUrl
Obtient cloudEndpointBaseUrl.

  
**Retourne** : URL de base associée aux points de terminaison de protection
  
### <a name="setprotectiononlyengine"></a>SetProtectionOnlyEngine
Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
### <a name="isprotectiononlyengine"></a>IsProtectionOnlyEngine
Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.