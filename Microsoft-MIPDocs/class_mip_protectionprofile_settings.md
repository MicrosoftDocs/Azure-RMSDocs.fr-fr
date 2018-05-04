# <a name="class-mipprotectionprofilesettings"></a>mip::ProtectionProfile::Settings, classe 
[Settings](#classmip_1_1_protection_profile_1_1_settings) utilisé par [ProtectionProfile](#classmip_1_1_protection_profile) lors de sa création et tout au long de sa durée de vie.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  SettingsProtectionProfile::Observer > & observer,const ApplicationInfo & applicationInfo) public inline const std::string & GetPath | Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.
public inline const std::shared_ptr< ProtectionProfile::Observer > & GetObserver public inline const ApplicationInfo & GetApplicationInfo | Obtient les informations sur l’application qui utilise le SDK de protection.
public inline bool GetSkipTelemetryInit | Détermine si l’initialisation de la télémétrie doit être désactivée.
public inline void SetSkipTelemetryInit | Désactive l’initialisation de la télémétrie.
public inline void SetSessionId | Définit l’ID de session. public inline const std::string & GetSessionId | Obtient l’ID de la session.
## <a name="members"></a>Membres
### <a name="settings"></a>Settings
Constructeur [ProtectionProfile::Settings](#classmip_1_1_protection_profile_1_1_settings).
#### <a name="parameters"></a>Paramètres
* path : chemin du fichier où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection 
* observer : instance [Observer](#classmip_1_1_protection_profile_1_1_observer) qui reçoit les notifications des événements liés à [ProtectionProfile](#classmip_1_1_protection_profile)
* applicationInfo : informations sur l’application qui utilise le SDK de protection
### <a name="getpath"></a>GetPath
Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.
#### <a name="returns"></a>Returns
le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Obtient l’instance Observer qui reçoit les notifications des événements liés à [ProtectionProfile](#classmip_1_1_protection_profile).
#### <a name="returns"></a>Returns
l’instance [Observer](#classmip_1_1_protection_profile_1_1_observer) qui reçoit les notifications des événements liés à [ProtectionProfile](#classmip_1_1_protection_profile)
### <a name="applicationinfo"></a>ApplicationInfo
Obtient les informations sur l’application qui utilise le SDK de protection.
#### <a name="returns"></a>Returns
les informations sur l’application qui utilise le SDK de protection
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Détermine si l’initialisation de la télémétrie doit être ignorée.
#### <a name="returns"></a>Returns
une valeur déterminant si l’initialisation de la télémétrie doit être ignorée
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Désactive l’initialisation de la télémétrie.
En principe, ne doit pas être appelé par des applications clientes, mais doit être utilisé par le SDK de fichier (qui initialise déjà la télémétrie) pour empêcher l’initialisation en double
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de la session.
#### <a name="parameters"></a>Paramètres
* sessionId : ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie
### <a name="getsessionid"></a>GetSessionId
Obtient l’ID de la session.
#### <a name="returns"></a>Returns
l’ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie