# <a name="class-mipfileengine"></a>mip::FileEngine, classe 
Interface pour toutes les fonctions du moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public virtual ~FileEngine()  | _Pas encore documenté._
 public const Settings& GetSettings() const  |  Retourne les paramètres du moteur.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Retourne une liste d’étiquettes de sensibilité.
public void CreateFileHandlerAsync(const std::string& inputFilePath, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.
public void CreateFileHandlerAsync(const std::shared_ptr<Stream>& inputStream, const std::string& inputFileName, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.
 protected FileEngine()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="fileengine"></a>~FileEngine
_Pas encore documenté._

  
### <a name="settings"></a>Paramètres
Retourne les paramètres du moteur.
  
### <a name="label"></a>Étiquette
Retourne une liste d’étiquettes de sensibilité.
  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.

Paramètres :  
* **The** : fichier à ouvrir. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **A** : classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context** : contexte client qui est repassé de façon opaque à l’observateur.


  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.

Paramètres :  
* **A** : flux qui représente le fichier. 


* **The** : chemin du fichier. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **A** : classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context** : contexte client qui est repassé de façon opaque à l’observateur.


  
### <a name="fileengine"></a>FileEngine
_Pas encore documenté._
