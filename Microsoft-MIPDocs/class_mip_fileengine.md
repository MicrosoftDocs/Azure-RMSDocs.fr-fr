# <a name="class-mipfileengine"></a>mip::FileEngine, classe 
Interface pour toutes les fonctions du moteur.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline virtual  ~FileEngine | 
public const Settings & GetSettings | Retourne les paramètres du moteur.
public const std::vector< std::shared_ptr< Label > > & ListSensitivityLabels | Retourne une liste d’étiquettes de sensibilité.
public std::shared_ptr< FileHandler > CreateFileHandlerFileHandler::Observer > & fileHandlerObserver) | Retourne le gestionnaire de fichiers pour le chemin de fichier donné.
public std::shared_ptr< FileHandler > CreateFileHandlerStream > & inputStream,const std::string & inputFileName,const std::shared_ptr< FileHandler::Observer > & fileHandlerObserver) | Retourne le gestionnaire de fichiers pour le flux de fichier donné.
protected inline  FileEngine | 
## <a name="members"></a>Membres
### <a name="fileengine"></a>~FileEngine
### <a name="settings"></a>Paramètres
Retourne les paramètres du moteur.
### <a name="label"></a>Étiquette
Retourne une liste d’étiquettes de sensibilité.
### <a name="filehandler"></a>FileHandler
Retourne le gestionnaire de fichiers pour le chemin de fichier donné.
#### <a name="parameters"></a>Paramètres
* Fichier à ouvrir. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 
* Une classe qui implémente l’interface [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
### <a name="filehandler"></a>FileHandler
Retourne le gestionnaire de fichiers pour le flux de fichier donné.
#### <a name="parameters"></a>Paramètres
* Flux qui représente le fichier. 
* Chemin du fichier. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 
* Une classe qui implémente l’interface [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
### <a name="fileengine"></a>FileEngine