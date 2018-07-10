# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
Une classe qui définit l’interface de l’enregistreur d’événements sdk mip.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath)  |  Initialiser l’enregistreur d’événements.
 public void Flush()  |  Vider le l’enregistreur d’événements.
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const uint64_t line)  |  Écrire une instruction de journal dans le fichier journal.
  
## <a name="members"></a>Membres
  
### <a name="init"></a>Init
Initialiser l’enregistreur d’événements.

Paramètres :  
* **storagePath** : le chemin d’accès à l’emplacement où l’état persistant, notamment les journaux, peut être stocké.


  
### <a name="flush"></a>Purge
Vider le l’enregistreur d’événements.
  
### <a name="writetolog"></a>WriteToLog
Écrire une instruction de journal dans le fichier journal.

Paramètres :  
* **level** : loglevel pour l’instruction de journal. 


* **message** : message pour l’instruction de journal. 


* **function** : nom de la fonction pour l’instruction de journal. 


* **file** : nom du fichier où l’instruction de journal a été générée. 


* **line** : numéro de ligne où l’instruction de journal a été générée.

