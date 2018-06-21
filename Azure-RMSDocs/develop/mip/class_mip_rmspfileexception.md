# <a name="class-miprmspfileexception"></a>mip::RMSPFileException, classe 
Exception RMS PFile.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSPFileException(const std::string& message, Reason reason)  |  Constructeur [RMSPFileException](class_mip_rmspfileexception.md).
 public RMSPFileException(const char*const& message, Reason reason)  |  Constructeur [RMSPFileException](class_mip_rmspfileexception.md).
 public virtual Reason reason() const  |  Obtenir la classification de l’erreur PFile.
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmspfileexception"></a>RMSPFileException
Constructeur [RMSPFileException](class_mip_rmspfileexception.md).

Paramètres :  
* **message** : message de l’exception 


* **reason** : classification de l’erreur PFile


  
### <a name="rmspfileexception"></a>RMSPFileException
Constructeur [RMSPFileException](class_mip_rmspfileexception.md).

Paramètres :  
* **message** : message de l’exception 


* **reason** : classification de l’erreur PFile


  
### <a name="reason"></a>Raison
Obtenir la classification de l’erreur PFile.

  
**Retourne** : classification de l’erreur PFile
  
### <a name="what"></a>what
Obtient le message de l’exception.

  
**Retourne** : le message de l’exception
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtient le type d’exception.

  
**Retourne** : le type de l’exception
  
### <a name="error"></a>erreur
Obtient le code d’erreur.

  
**Retourne** : le code de [l’erreur](class_mip_error.md)