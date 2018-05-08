# <a name="class-mipfileprofilesettings"></a>mip::FileProfile::Settings, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Interface pour la configuration du profil.
public inline ~Settings()  |  
public inline const std::string& GetPath() const  |  
public inline bool GetUseInMemoryStorage() const  |  
public inline std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  
public inline std::shared_ptr<Observer> GetObserver() const  |  
public inline const ApplicationInfo GetApplicationInfo() const  |  
public inline bool GetSkipTelemetryInit() const  |  
public inline void SetSkipTelemetryInit()  |  
public inline void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session de profil.
public inline const std::string& GetSessionId() const  |  Retourne l’ID de session de profil.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Interface pour la configuration du profil.
  
#### <a name="parameters"></a>Paramètres
* observer Classe qui implémente l’interface [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer). Peut être nullptr.
  
### <a name="settings"></a>~Settings
  
### <a name="getpath"></a>GetPath
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
  
### <a name="getauthdelegate"></a>GetAuthDelegate
  
### <a name="observer"></a>Observateur
  
### <a name="applicationinfo"></a>ApplicationInfo
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
  
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de session de profil.
  
### <a name="getsessionid"></a>GetSessionId
Retourne l’ID de session de profil.