# <a name="class-mipfileenginesettings"></a>mip::FileEngine::Settings, classe 
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  Settings | Crée une instance avec les paramètres donnés.
public inline  Settings | Crée une instance avec les paramètres donnés.
public inline const std::string & GetId | Retourne l’ID du moteur.
public inline const Identity & GetIdentity | Retourne l’identité du moteur.
public inline void SetIdentity | Définit l’identité du moteur.
public inline const std::string & GetClientData | Retourne les données clientes du moteur.
public inline const std::string & GetLocale | Retourne les paramètres régionaux du moteur.
public inline void SetCustomSettings | Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public inline const std::vector< std::pair< std::string, std::string > > & GetCustomSettings | Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public inline void SetSessionId | Définit l’ID de session du moteur.
public inline const std::string & GetSessionId | Retourne l’ID de session du moteur.
## <a name="members"></a>Membres
### <a name="settings"></a>Paramètres
Crée une instance avec les paramètres donnés.
Sert à créer [Settings](#classmip_1_1_file_engine_1_1_settings) pour appeler LoadEngineAsync afin de charger un moteur existant (précédemment ajouté avec AddEngineAsync).
#### <a name="parameters"></a>Paramètres
* id : assignez à ce paramètre l’ID de moteur unique généré par AddEngineAsync.
### <a name="settings"></a>Paramètres
Crée une instance avec les paramètres donnés.
Sert à créer [Settings](#classmip_1_1_file_engine_1_1_settings) pour appeler AddEngineAsync afin d’ajouter un nouveau moteur.
#### <a name="parameters"></a>Paramètres
* identity : informations sur l’identité de l’utilisateur pour lequel le moteur doit être ajouté.
### <a name="getid"></a>GetId
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