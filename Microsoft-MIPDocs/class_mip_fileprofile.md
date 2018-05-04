# <a name="class-mipfileprofile"></a>mip::FileProfile, classe 
La classe [FileProfile](#classmip_1_1_file_profile) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’une seule classe [Profile](#classmip_1_1_profile), mais elle peut créer plusieurs profils si nécessaire.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline virtual  ~FileProfile | 
public const Settings & GetSettings | Retourne les paramètres de profil.
public void ListEnginesAsync | Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync | Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public void AddEngineAsyncFileEngine::Settings & settings,const std::shared_ptr< void > & context) | Démarre l’ajout d’un nouveau moteur de fichier au profil.
public void DeleteEngineAsync | Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront entièrement supprimées.
protected inline  FileProfile | 
## <a name="members"></a>Membres
### <a name="fileprofile"></a>~FileProfile
### <a name="settings"></a>Paramètres
Retourne les paramètres de profil.
### <a name="listenginesasync"></a>ListEnginesAsync
Démarre une opération d’énumération de moteurs.
[FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) est appelé en cas de réussite ou d’échec.
### <a name="unloadengineasync"></a>UnloadEngineAsync
Démarre le déchargement du moteur de fichier avec l’ID spécifié. [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) est appelé en cas de réussite ou d’échec.
### <a name="addengineasync"></a>AddEngineAsync
Démarre l’ajout d’un nouveau moteur de fichier au profil.
[FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) est appelé en cas de réussite ou d’échec.
### <a name="deleteengineasync"></a>DeleteEngineAsync
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront entièrement supprimées.
[FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) est appelé en cas de réussite ou d’échec.
### <a name="fileprofile"></a>FileProfile