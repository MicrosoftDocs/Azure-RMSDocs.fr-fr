# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
Une instance de cette classe avec les paramètres appropriés doit être fournie pour démarrer un moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& id, const std::string& clientData, const std::string& locale)  |  Construire une instance avec les paramètres donnés. Sert à créer [Settings](class_mip_policyengine_settings.md) pour appeler LoadEngineAsync afin de charger un moteur existant.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Sert à créer [Settings](class_mip_policyengine_settings.md) pour appeler AddEngineAsync afin d’ajouter un nouveau moteur.
 public const std::string& GetId() const  |  Obtenir l’ID du moteur.
 public void SetId(const std::string& id)  |  Définir l’ID du moteur.
 public const Identity& GetIdentity() const  |  Obtenir l’objet Identity.
 public void SetIdentity(const Identity& identity)  |  Définir l’objet Identity.
 public const std::string& GetClientData() const  |  Obtenir la valeur Client Data définie dans les paramètres.
 public void SetClientData(const std::string& clientData)  |  Définir la chaîne Client Data.
 public const std::string& GetLocale() const  |  Obtenir la valeur Locale définie dans les paramètres.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
 public void SetSessionId(const std::string& sessionId)  |  Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.
 public const std::string& GetSessionId() const  |  Obtenir l’ID de session, qui est un identificateur unique.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Construire une instance avec les paramètres donnés. Sert à créer [Settings](class_mip_policyengine_settings.md) pour appeler LoadEngineAsync afin de charger un moteur existant.

Paramètres :  
* **id** : affectez à ce paramètre l’ID unique du moteur généré par AddEngineAsync ou un ID généré automatiquement. Quand vous chargez un moteur existant, réutilisez l’ID ; sinon, un moteur est créé. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. Par défaut, « en-US ».


  
### <a name="settings"></a>Paramètres
Sert à créer [Settings](class_mip_policyengine_settings.md) pour appeler AddEngineAsync afin d’ajouter un nouveau moteur.

Paramètres :  
* **identity** : identificateur unique de l’utilisateur pour lequel le moteur doit être ajouté. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. Par défaut, « en-US ».


  
### <a name="getid"></a>GetId
Obtenir l’ID du moteur.

  
**Retourne** : une chaîne unique identifiant le moteur.
  
### <a name="setid"></a>SetId
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity"></a>GetIdentity
Obtenir l’objet Identity.

  
**Retourne** : une référence à l’identité définie dans l’objet settings. 
**Voir aussi** : mip::Identity
  
### <a name="setidentity"></a>SetIdentity
Définir l’objet Identity.

Paramètres :  
* **identity** : identité unique d’un utilisateur. 


**Voir aussi** : mip::Identity
  
### <a name="getclientdata"></a>GetClientData
Obtenir la valeur Client Data définie dans les paramètres.

  
**Retourne** : une chaîne de données spécifiées par le client.
  
### <a name="setclientdata"></a>SetClientData
Définir la chaîne Client Data.

Paramètres :  
* **clientData** : données spécifiées par l’utilisateur.


  
### <a name="getlocale"></a>GetLocale
Obtenir la valeur Locale définie dans les paramètres.

  
**Retourne** : les paramètres régionaux.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings** : liste de paires nom/valeur.


  
### <a name="getcustomsettings"></a>SetCustomSettings
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **List** : liste de paires nom/valeur.


  
### <a name="setsessionid"></a>SetSessionId
Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.

Paramètres :  
* **sessionId** : chaîne unique qui connecte des événements de télémétrie.


  
### <a name="getsessionid"></a>GetSessionId
Obtenir l’ID de session, qui est un identificateur unique.

  
**Retourne** : l’ID de session.