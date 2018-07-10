# <a name="class-mipfileprofilesettings"></a>mip::FileProfile::Settings, classe 
[Settings](class_mip_fileprofile_settings.md) utilisé par [FileProfile](class_mip_fileprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md).
 public const std::string& GetPath() const  |  Obtient le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant.
 public bool GetUseInMemoryStorage() const  |  Détermine si tous les états doivent être stockés dans la mémoire (plutôt que sur le disque)
 public bool IsLicenseCachingEnabled() const  |  Déterminer si la mise en cache de licences est activée ou pas.
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Obtient le délégué de consentement utilisé pour demander le consentement de l’utilisateur pour la connexion aux services.
public std::shared_ptr<Observer> GetObserver() const  |  Obtient l’instance Observer qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md).
 public const ApplicationInfo GetApplicationInfo() const  |  Obtient les informations sur l’application qui utilise le SDK.
 public bool GetSkipTelemetryInit() const  |  Détermine si l’initialisation de la télémétrie doit être ignorée.
 public void SetSkipTelemetryInit()  |  Désactive l’initialisation de la télémétrie.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Utiliser l’implémentation de l’enregistreur d’événements externe.
 public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
 public bool IsTelemetryOptedOut() const  |  Déterminer si la collecte des données de télémétrie doit être désactivée ou pas.
 public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de la session.
 public const std::string& GetSessionId() const  |  Obtient l’ID de la session.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md).

Paramètres :  
* **path** : le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant 


* **useInMemoryStorage** : détermine si tous les états doivent être stockés dans la mémoire (plutôt que sur le disque) 


* **isLicenseCachingEnabled** : activer ou désactiver la mise en cache des licences de protection 


* **authDelegate** : le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification 


* **observer** : instance de [Observer](class_mip_fileprofile_observer.md) qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md)


* **applicationInfo** : les informations sur l’application qui utilise le SDK


  
### <a name="getpath"></a>GetPath
Obtient le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant.

  
**Retourne** : le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Détermine si tous les états doivent être stockés dans la mémoire (plutôt que sur le disque)

  
**Retourne** : détermine si tous les états doivent être stockés dans la mémoire (plutôt que sur le disque)
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
Déterminer si la mise en cache de licences est activée ou pas.

  
**Retourne** : True si les caches sont stockés en mémoire uniquement
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.

  
**Retourne** : le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification
  
### <a name="consentdelegate"></a>ConsentDelegate
Obtient le délégué de consentement utilisé pour demander le consentement de l’utilisateur pour la connexion aux services.

  
**Retourne** : le délégué consentement utilisé pour demander le consentement de l’utilisateur
  
### <a name="observer"></a>Observateur
Obtient l’instance Observer qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md).

  
**Retourne** : l’instance [Observer](class_mip_fileprofile_observer.md) qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtient les informations sur l’application qui utilise le SDK.

  
**Retourne** : les informations sur l’application qui utilise le SDK
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Détermine si l’initialisation de la télémétrie doit être ignorée.

  
**Retourne** : une valeur indiquant si l’initialisation de la télémétrie doit ou non être ignorée.
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Désactive l’initialisation de la télémétrie.
En principe, ne doit pas être appelé par des applications clientes, mais doit être utilisé par le SDK de fichier (qui initialise déjà la télémétrie) pour empêcher l’initialisation en double
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.

  
**Retourne** : le délégué de l’enregistreur d’événements à utiliser pour la journalisation
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Utiliser l’implémentation de l’enregistreur d’événements externe.
Doit être appelé par les applications clientes si elles souhaitent utiliser leur propre implémentation de l’enregistreur d’événements
  
### <a name="optouttelemetry"></a>OptOutTelemetry
Refuse la collecte des données de télémétrie.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Déterminer si la collecte des données de télémétrie doit être désactivée ou pas.

  
**Retourne** : détermine si la collecte des données de télémétrie doit être désactivée ou pas
  
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de la session.

Paramètres :  
* **sessionId** : ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie


  
### <a name="getsessionid"></a>GetSessionId
Obtient l’ID de la session.

  
**Retourne** : l’ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie