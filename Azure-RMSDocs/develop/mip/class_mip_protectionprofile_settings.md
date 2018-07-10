# <a name="class-mipprotectionprofilesettings"></a>mip::ProtectionProfile::Settings, classe 
[Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).
 public const std::string& GetPath() const  |  Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.
 public bool GetUseInMemoryStorage() const  |  Savoir si les caches sont stockés en mémoire uniquement (plutôt que sur le disque)
 public bool IsLicenseCachingEnabled() const  |  Déterminer si la mise en cache de licences est activée ou pas.
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Obtient le délégué de consentement utilisé pour la connexion aux services.
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  Obtient l’instance Observer qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Obtient les informations sur l’application qui utilise le SDK de protection.
 public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
 public bool IsTelemetryOptedOut() const  |  Déterminer si la collecte des données de télémétrie doit être désactivée ou pas.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Utiliser l’implémentation de l’enregistreur d’événements externe.
 public bool GetSkipTelemetryInit() const  |  Détermine si l’initialisation de la télémétrie doit être ignorée.
 public void SetSkipTelemetryInit()  |  Désactive l’initialisation de la télémétrie.
 public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de la session.
 public const std::string& GetSessionId() const  |  Obtient l’ID de la session.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).

Paramètres :  
* **path** : chemin du fichier où sont stockées les informations de journalisation, les données de télémétrie et d’autres informations relatives à la protection 


* **useInMemoryStorage** : stocker tout état mis en cache dans la mémoire plutôt que sur le disque 


* **isLicenseCachingEnabled** : activer ou désactiver la mise en cache des licences du SDK de protection 


* **authDelegate** : objet de rappel à utiliser pour l’authentification, implémenté par l’application cliente 


* **observer** : instance de [Observer](class_mip_protectionprofile_observer.md) qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo** : informations sur l’application qui utilise le SDK de protection


  
### <a name="getpath"></a>GetPath
Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.

  
**Retourne** : le chemin où sont stockées les informations de journalisation, les données de télémétrie et d’autres informations relatives à la protection
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Savoir si les caches sont stockés en mémoire uniquement (plutôt que sur le disque)

  
**Retourne** : True si les caches sont stockés en mémoire uniquement
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
Déterminer si la mise en cache de licences est activée ou pas.

  
**Retourne** : True si la mise en cache de la licence du SDK de protection est activée
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.

  
**Retourne** : le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification
  
### <a name="consentdelegate"></a>ConsentDelegate
Obtient le délégué de consentement utilisé pour la connexion aux services.

  
**Retourne** : le délégué de consentement utilisé pour la connexion aux services
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Obtient l’instance Observer qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).

  
**Retourne** : l’instance [Observer](class_mip_protectionprofile_observer.md) qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtient les informations sur l’application qui utilise le SDK de protection.

  
**Retourne** : les informations sur l’application qui utilise le SDK de protection
  
### <a name="optouttelemetry"></a>OptOutTelemetry
Refuse la collecte des données de télémétrie.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Déterminer si la collecte des données de télémétrie doit être désactivée ou pas.

  
**Retourne** : détermine si la collecte des données de télémétrie doit être désactivée ou pas
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.

  
**Retourne** : le délégué de l’enregistreur d’événements à utiliser pour la journalisation
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Utiliser l’implémentation de l’enregistreur d’événements externe.
Doit être appelé par les applications clientes si elles souhaitent utiliser leur propre implémentation de l’enregistreur d’événements
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Détermine si l’initialisation de la télémétrie doit être ignorée.

  
**Retourne** : une valeur indiquant si l’initialisation de la télémétrie doit ou non être ignorée.
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Désactive l’initialisation de la télémétrie.
En principe, ne doit pas être appelé par des applications clientes, mais doit être utilisé par le SDK de fichier (qui initialise déjà la télémétrie) pour empêcher l’initialisation en double
  
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de la session.

Paramètres :  
* **sessionId** : ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie


  
### <a name="getsessionid"></a>GetSessionId
Obtient l’ID de la session.

  
**Retourne** : l’ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie