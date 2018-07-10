# <a name="class-mipfilehandler"></a>mip::FileHandler, classe 
Interface pour toutes les fonctions de gestion de fichiers.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  Démarre la récupération de la stratégie de protection à partir du fichier.
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Définit l’étiquette de sensibilité sur le fichier.
 public void DeleteLabel(AssignmentMethod method, const std::string& justificationMessage)  |  Supprime l’étiquette de sensibilité du fichier.
public void SetProtection(const std::shared_ptr<ProtectionDescriptor>& protectionDescriptor)  |  Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
 public void RemoveProtection()  |  Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | Écrit les modifications dans le fichier spécifié par le paramètre \|outputFilePath\ |  .
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | Écrit les modifications dans le flux spécifié par le paramètre \|outputStream\ |  .
 public std::string GetOutputFileName()  |  Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.
 public virtual ~FileHandler()  | _Pas encore documenté._
 protected FileHandler()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="getlabelasync"></a>GetLabelAsync
Démarre la récupération de l’étiquette de sensibilité à partir du fichier.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.

Paramètres :  
* **context** : contexte client qui est repassé de façon opaque à l’observateur.


  
### <a name="getprotectionasync"></a>GetProtectionAsync
Démarre la récupération de la stratégie de protection à partir du fichier.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.

Paramètres :  
* **context** : contexte client qui est repassé de façon opaque à l’observateur.


  
### <a name="setlabel"></a>SetLabel
Définit l’étiquette de sensibilité sur le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
Lève [JustificationRequiredError](class_mip_justificationrequirederror.md) quand la définition de l’étiquette nécessite une justification et qu’aucun message de justification n’a été fourni par le paramètre labelingOptions.
  
### <a name="deletelabel"></a>DeleteLabel
Supprime l’étiquette de sensibilité du fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé. La méthode Privileged et Auto permet à l’API de substituer une étiquette existante. Lève [JustificationRequiredError](class_mip_justificationrequirederror.md) quand la définition de l’étiquette nécessite une justification et qu’aucun message de justification n’a été fourni par le paramètre justificationMessage.
  
### <a name="setprotection"></a>SetProtection
Définit des autorisations personnalisées ou basées sur un modèle (en fonction de protectionDescriptor->GetProtectionType) pour le fichier.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="removeprotection"></a>RemoveProtection
Supprime la protection du fichier. Si le fichier porte une étiquette, celle-ci est perdue.
Les modifications ne sont pas écrites dans le fichier tant que CommitAsync n’est pas appelé.
  
### <a name="commitasync"></a>CommitAsync
Écrit les modifications dans le fichier spécifié par le paramètre |outputFilePath|.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="commitasync"></a>CommitAsync
Écrit les modifications dans le flux spécifié par le paramètre |outputStream|.
[FileHandler::Observer](class_mip_filehandler_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="getoutputfilename"></a>GetOutputFileName
Détermine le nom et l’extension du fichier de sortie en fonction du nom du fichier d’origine et des modifications cumulées.
  
### <a name="filehandler"></a>~FileHandler
_Pas encore documenté._

  
### <a name="filehandler"></a>FileHandler
_Pas encore documenté._
