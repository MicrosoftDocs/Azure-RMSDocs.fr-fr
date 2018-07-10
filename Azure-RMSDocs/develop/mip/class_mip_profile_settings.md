# <a name="class-mipprofilesettings"></a>mip::Profile::Settings, classe 
[Paramètres](class_mip_profile_settings.md) utilisés par [Profil](class_mip_profile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interface pour la configuration du profil.
 public const std::string& GetPath() const  |  Obtenir le chemin de l’état stocké.
 public bool GetUseInMemoryStorage() const  |  Obtenir l’indicateur d’utilisation de la mémoire de stockage.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Obtenir le délégué d’authentification.
public const std::shared_ptr<Profile::Observer>& GetObserver() const  |  Obtenir l’observateur d’événements.
 public const ApplicationInfo GetApplicationInfo() const  |  Obtenir les informations sur l’application.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Utiliser l’implémentation de l’enregistreur d’événements externe.
 public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
 public bool IsTelemetryOptedOut() const  |  Détermine si la collecte des données de télémétrie doit être désactivée ou pas.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Interface pour la configuration du profil.

Paramètres :  
* **path** : chemin d’un répertoire dans lequel le SDK stocke l’état du profil. 


* **useInMemoryStorage** : indicateur spécifiant si l’état doit ou non être stocké sur le disque. 


* **authDelegate** : délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification. 


* **observer** : classe qui implémente l’interface [Profile::Observer](class_mip_profile_observer.md). Peut être nullptr. 


* **applicationInfo** : identificateurs d’application utilisés pour l’accès au service.


  
### <a name="getpath"></a>GetPath
Obtenir le chemin de l’état stocké.

  
**Retourne** : le chemin de l’état stocké.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtenir l’indicateur d’utilisation de la mémoire de stockage.

  
**Retourne** : true si l’utilisation en mémoire est définie ; sinon, false.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtenir le délégué d’authentification.

  
**Retourne** : le délégué d’authentification.
  
### <a name="profileobserver"></a>Profile::Observer
Obtenir l’observateur d’événements.

  
**Retourne** : l’observateur d’événements.
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtenir les informations sur l’application.

  
**Retourne** : les informations sur l’application.
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.

  
**Retourne** : le délégué de l’enregistreur d’événements à utiliser pour la journalisation
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Utiliser l’implémentation de l’enregistreur d’événements externe.
Doit être appelé par les applications clientes si elles souhaitent utiliser leur propre implémentation de l’enregistreur d’événements
  
### <a name="optouttelemetry"></a>OptOutTelemetry
Refuse la collecte des données de télémétrie.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Détermine si la collecte des données de télémétrie doit être désactivée ou pas.

  
**Retourne** : détermine si la collecte des données de télémétrie doit être désactivée ou pas