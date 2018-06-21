# <a name="class-mipprofilesettings"></a>mip::Profile::Settings, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interface pour la configuration du profil.
 public const std::string& GetPath() const  |  Obtenir le chemin de l’état stocké.
 public bool GetUseInMemoryStorage() const  |  Obtenir l’indicateur d’utilisation de la mémoire de stockage.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Obtenir le délégué d’authentification.
public const std::shared_ptr<Profile::Observer>& GetObserver() const  |  Obtenir l’observateur d’événements.
 public const ApplicationInfo GetApplicationInfo() const  |  Obtenir les informations sur l’application.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Interface pour la configuration du profil.

Paramètres :  
* **path** : chemin d’un répertoire dans lequel le SDK stocke l’état du profil. 


* **useInMemoryStorage** : indicateur spécifiant si l’état doit ou non être stocké sur le disque. 


* **authDelegate** : délégué d’authentification utilisé par le SDK pour acquérir des jetons d’authentification. 


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