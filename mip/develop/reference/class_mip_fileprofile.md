# <a name="class-mipfileprofile"></a>mip::FileProfile, classe 
La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’une seule classe [Profile](class_mip_profile.md), mais elle peut créer plusieurs profils si nécessaire.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Retourne les paramètres de profil.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Démarre l’ajout d’un nouveau moteur de fichier au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront entièrement supprimées.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Retourne les paramètres de profil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Démarre une opération d’énumération de moteurs.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Démarre le déchargement du moteur de fichier avec l’ID spécifié. [FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync"></a>AddEngineAsync
Démarre l’ajout d’un nouveau moteur de fichier au profil.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront entièrement supprimées.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.