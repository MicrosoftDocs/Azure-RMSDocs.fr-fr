# <a name="class-mipprofilesettings"></a>mip::Profile::Settings, classe 
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  SettingsProfile::Observer > & observer,const ApplicationInfo & applicationInfo) | Interface pour la configuration du profil.
public inline const std::string & GetPath | Obtenir le chemin de l’état stocké.
public inline bool GetUseInMemoryStorage | Obtenir l’indicateur d’utilisation de la mémoire de stockage.
public inline const std::shared_ptr< AuthDelegate > & GetAuthDelegate | Obtenir le délégué d’authentification.
public inline const std::shared_ptr< Profile::Observer > & GetObserver | Obtenir l’observateur d’événements.
public inline const ApplicationInfo GetApplicationInfo | Obtenir les informations sur l’application.
## <a name="members"></a>Membres
### <a name="settings"></a>Paramètres
Interface pour la configuration du profil.
#### <a name="parameters"></a>Paramètres
* path : chemin d’un répertoire dans lequel le SDK stocke l’état du profil. 
* useInMemoryStorage : indicateur spécifiant si l’état doit être stocké sur le disque. 
* authDelegate : délégué d’authentification utilisé par le SDK pour acquérir des jetons d’authentification. 
* observer : classe qui implémente l’interface [Profile::Observer](#classmip_1_1_profile_1_1_observer). Peut être nullptr. 
* applicationInfo : identificateurs d’application utilisés pour l’accès au service.
### <a name="getpath"></a>GetPath
Obtenir le chemin de l’état stocké.
#### <a name="returns"></a>Returns
le chemin de l’état stocké.
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtenir l’indicateur d’utilisation de la mémoire de stockage.
#### <a name="returns"></a>Returns
true si l’utilisation de la mémoire est définie ; sinon, false.
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtenir le délégué d’authentification.
#### <a name="returns"></a>Returns
le délégué d’authentification.
### <a name="profileobserver"></a>Profile::Observer
Obtenir l’observateur d’événements.
#### <a name="returns"></a>Returns
l’observateur d’événements.
### <a name="applicationinfo"></a>ApplicationInfo
Obtenir les informations sur l’application.
#### <a name="returns"></a>Returns
les informations sur l’application.