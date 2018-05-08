# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
Une instance de cette classe avec les paramètres appropriés doit être fournie pour démarrer un moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
`public inline Settings(const std::string& id, const std::string& clientData, const std::string& locale)`  |  Construire une instance avec les paramètres donnés. Sert à créer [Settings](#classmip_1_1_policy_engine_1_1_settings) pour appeler LoadEngineAsync afin de charger un moteur existant.
`public inline Settings(const Identity& identity, const std::string& clientData, const std::string& locale)`  |  Sert à créer [Settings](#classmip_1_1_policy_engine_1_1_settings) pour appeler AddEngineAsync afin d’ajouter un nouveau moteur.
`public inline const std::string& GetId() const`  |  Obtenir l’ID du moteur.
`public inline void SetId(const std::string& id)`  |  Définir l’ID du moteur.
`public inline const Identity& GetIdentity() const`  |  Obtenir l’objet Identity.
`public inline void SetIdentity(const Identity& identity)`  |  Définir l’objet Identity.
`public inline const std::string& GetClientData() const`  |  Obtenir la valeur Client Data définie dans les paramètres.
`public inline void SetClientData(const std::string& clientData)`  |  Définir la chaîne Client Data.
`public inline const std::string& GetLocale() const`  |  Obtenir la valeur Locale définie dans les paramètres.
`public inline void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)`  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
`public inline const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const`  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
`public inline void SetSessionId(const std::string& sessionId)`  |  Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.
`public inline const std::string& GetSessionId() const`  |  Obtenir l’ID de session, qui est un identificateur unique.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Construire une instance avec les paramètres donnés. Sert à créer [Settings](#classmip_1_1_policy_engine_1_1_settings) pour appeler LoadEngineAsync afin de charger un moteur existant.
  
#### <a name="parameters"></a>Paramètres
* id : assignez à ce paramètre l’ID de moteur unique généré par AddEngineAsync ou un ID généré automatiquement. Quand vous chargez un moteur existant, réutilisez l’ID ; sinon, un moteur est créé. 
* clientData : données clientes personnalisables qui peuvent être stockées avec le moteur durant le déchargement, et être récupérées à partir d’un moteur chargé. 
* locale : la sortie localisable du moteur est fournie dans ces paramètres régionaux, par défaut « en-US ».
  
### <a name="settings"></a>Paramètres
Sert à créer [Settings](#classmip_1_1_policy_engine_1_1_settings) pour appeler AddEngineAsync afin d’ajouter un nouveau moteur.
  
#### <a name="parameters"></a>Paramètres
* identity : identificateur unique de l’utilisateur pour lequel le moteur doit être ajouté. 
* clientData : données clientes personnalisables qui peuvent être stockées avec le moteur durant le déchargement, et être récupérées à partir d’un moteur chargé. 
* locale : la sortie localisable du moteur est fournie dans ces paramètres régionaux, par défaut `en-US`.
  
### <a name="getid"></a>GetId
Obtenir l’ID du moteur.
  
#### <a name="returns"></a>Returns
une chaîne unique identifiant le moteur.
  
### <a name="setid"></a>SetId
Définir l’ID du moteur.
  
#### <a name="parameters"></a>Paramètres
* id : ID du moteur.
  
### <a name="getidentity"></a>GetIdentity
Obtenir l’objet Identity.
  
#### <a name="returns"></a>Returns
une référence à l’identité définie dans l’objet Settings. 
**Voir aussi** : mip::Identity
  
### <a name="setidentity"></a>SetIdentity
Définir l’objet Identity.
  
#### <a name="parameters"></a>Paramètres
* identity : identité unique d’un utilisateur. 
**Voir aussi** : mip::Identity
  
### <a name="getclientdata"></a>GetClientData
Obtenir la valeur Client Data définie dans les paramètres.
  
#### <a name="returns"></a>Returns
une chaîne de données spécifiées par le client.
  
### <a name="setclientdata"></a>SetClientData
Définir la chaîne Client Data.
  
#### <a name="parameters"></a>Paramètres
* clientData : données spécifiées par le client.
  
### <a name="getlocale"></a>GetLocale
Obtenir la valeur Locale définie dans les paramètres.
  
#### <a name="returns"></a>Returns
la valeur des paramètres régionaux.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
  
#### <a name="parameters"></a>Paramètres
* customSettings : liste de paires nom/valeur.
  
### <a name="getcustomsettings"></a>GetCustomSettings
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
  
#### <a name="parameters"></a>Paramètres
* Liste de paires nom/valeur.
  
### <a name="setsessionid"></a>SetSessionId
Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.
  
#### <a name="parameters"></a>Paramètres
* sessionId : chaîne unique qui connecte des événements de télémétrie.
  
### <a name="getsessionid"></a>GetSessionId
Obtenir l’ID de session, qui est un identificateur unique.
  
#### <a name="returns"></a>Returns
l’ID de la session.