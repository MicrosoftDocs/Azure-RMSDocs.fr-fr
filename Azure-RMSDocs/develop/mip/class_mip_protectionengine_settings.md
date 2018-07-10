# <a name="class-mipprotectionenginesettings"></a>class mip::ProtectionEngine::Settings 
[Settings](class_mip_protectionengine_settings.md) utilisé par [ProtectionEngine](class_mip_protectionengine.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour la création d’un nouveau moteur.
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour le chargement d’un moteur existant.
 public const std::string& GetEngineId() const  |  Obtient l’ID du moteur.
 public void SetEngineId(const std::string& engineId)  |  Définit l’ID du moteur.
 public const Identity& GetIdentity() const  |  Obtient l’identité de l’utilisateur associé au moteur.
 public void SetIdentity(const Identity& identity)  |  Définit l’identité de l’utilisateur associé au moteur.
 public const std::string& GetClientData() const  |  Obtient les données personnalisées spécifiées par le client.
 public const std::string& GetLocale() const  |  Obtient les paramètres régionaux selon lesquels les données du moteur seront écrites.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  Définit les paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtient les paires nom/valeur utilisées pour les tests et l’expérimentation.
 public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie.
 public const std::string& GetSessionId() const  |  Obtient l’ID de session du moteur.
 public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison du cloud, utilisée pour spécifier la limite du cloud.
 public const std::string& GetCloudEndpointBaseUrl() const  |  Obtient cloudEndpointBaseUrl.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour la création d’un nouveau moteur.

Paramètres :  
* **identity** : identité qui sera associée à [ProtectionEngine](class_mip_protectionengine.md)


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie du moteur est fournie dans ces paramètres régionaux. Par défaut, « en-US ».


  
### <a name="settings"></a>Paramètres
Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour le chargement d’un moteur existant.

Paramètres :  
* **engineId** : identificateur unique du moteur qui sera chargé 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie du moteur est fournie dans ces paramètres régionaux. Par défaut, « en-US ».


  
### <a name="getengineid"></a>GetEngineId
Obtient l’ID du moteur.

  
**Retourne** : l’ID du moteur
  
### <a name="setengineid"></a>SetEngineId
Définit l’ID du moteur.

Paramètres :  
* **engineId** : ID du moteur.


  
### <a name="getidentity"></a>GetIdentity
Obtient l’identité de l’utilisateur associé au moteur.

  
**Retourne** : l’identité de l’utilisateur associé au moteur
  
### <a name="setidentity"></a>SetIdentity
Définit l’identité de l’utilisateur associé au moteur.

Paramètres :  
* **identity** : l’identité de l’utilisateur associé au moteur


  
### <a name="getclientdata"></a>GetClientData
Obtient les données personnalisées spécifiées par le client.

  
**Retourne** : les données personnalisées spécifiées par le client
  
### <a name="getlocale"></a>GetLocale
Obtient les paramètres régionaux selon lesquels les données du moteur seront écrites.

  
**Retourne** : les paramètres régionaux selon lesquels les données du moteur seront écrites
  
### <a name="setcustomsettings"></a>SetCustomSettings
Définit les paires nom/valeur utilisées pour les tests et l’expérimentation.

Paramètres :  
* **customSettings** : une liste de paires nom/valeur utilisées pour les tests et l’expérimentation


  
### <a name="getcustomsettings"></a>SetCustomSettings
Obtient les paires nom/valeur utilisées pour les tests et l’expérimentation.

  
**Retourne** : les paires nom/valeur utilisées pour les tests et l’expérimentation
  
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie.

Paramètres :  
* **sessionId** : l’ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie


  
### <a name="getsessionid"></a>GetSessionId
Obtient l’ID de session du moteur.

  
**Retourne** : l’ID de session du moteur
  
### <a name="setcloudendpointbaseurl"></a>SetCloudEndpointBaseUrl
Définit l’URL de base du point de terminaison du cloud, utilisée pour spécifier la limite du cloud.

Paramètres :  
* **cloudEndpointBaseUrl** : URL de base associée aux points de terminaison de protection


  
### <a name="getcloudendpointbaseurl"></a>GetCloudEndpointBaseUrl
Obtient cloudEndpointBaseUrl.

  
**Retourne** : URL de base associée aux points de terminaison de protection