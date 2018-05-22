# <a name="class-mipprotectionprofilesettings"></a>mip::ProtectionProfile::Settings, classe 
[Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).
 public const std::string& GetPath() const  |  Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  Obtient l’instance Observer qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Obtient les informations sur l’application qui utilise le SDK de protection.
 public bool GetSkipTelemetryInit() const  |  Détermine si l’initialisation de la télémétrie doit être ignorée.
 public void SetSkipTelemetryInit()  |  Désactive l’initialisation de la télémétrie.
 public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de la session.
 public const std::string& GetSessionId() const  |  Obtient l’ID de la session.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).

Paramètres :  
* **path** : chemin du fichier où sont stockées les informations de journalisation, les données de télémétrie et d’autres informations relatives à la protection 


* **observer** : instance de [Observer](class_mip_protectionprofile_observer.md) qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo** : informations sur l’application qui utilise le SDK de protection


  
### <a name="getpath"></a>GetPath
Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.

  
**Retourne** : le chemin où sont stockées les informations de journalisation, les données de télémétrie et d’autres informations relatives à la protection
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Obtient l’instance Observer qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).

  
**Retourne** : l’instance de [Observer](class_mip_protectionprofile_observer.md) qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtient les informations sur l’application qui utilise le SDK de protection.

  
**Retourne** : les informations sur l’application qui utilise le SDK de protection
  
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