# <a name="class-mipfileprofilesettings"></a>mip::FileProfile::Settings, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Interface pour la configuration du profil.
 public ~Settings()  | _Pas encore documenté._
 public const std::string& GetPath() const  | _Pas encore documenté._
 public bool GetUseInMemoryStorage() const  | _Pas encore documenté._
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  | _Pas encore documenté._
public std::shared_ptr<Observer> GetObserver() const  | _Pas encore documenté._
 public const ApplicationInfo GetApplicationInfo() const  | _Pas encore documenté._
 public bool GetSkipTelemetryInit() const  | _Pas encore documenté._
 public void SetSkipTelemetryInit()  | _Pas encore documenté._
 public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session de profil.
 public const std::string& GetSessionId() const  |  Retourne l’ID de session de profil.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Interface pour la configuration du profil.

Paramètres :  
* **observer** : classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). Peut être nullptr.


  
### <a name="settings"></a>~Settings
_Pas encore documenté._

  
### <a name="getpath"></a>GetPath
_Pas encore documenté._

  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
_Pas encore documenté._

  
### <a name="getauthdelegate"></a>GetAuthDelegate
_Pas encore documenté._

  
### <a name="observer"></a>Observateur
_Pas encore documenté._

  
### <a name="applicationinfo"></a>ApplicationInfo
_Pas encore documenté._

  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
_Pas encore documenté._

  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
_Pas encore documenté._

  
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de session de profil.
  
### <a name="getsessionid"></a>GetSessionId
Retourne l’ID de session de profil.