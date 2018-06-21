# <a name="class-miprmsofficefileexception"></a>mip::RMSOfficeFileException, classe 
Exception de fichier Office RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSOfficeFileException(const std::string& message, Reason reason)  |  Constructeur [RMSOfficeFileException](class_mip_rmsofficefileexception.md).
 public RMSOfficeFileException(const char*const& message, Reason reason)  |  Constructeur [RMSOfficeFileException](class_mip_rmsofficefileexception.md).
 public virtual Reason reason() const  |  Obtient la classification de l’erreur de fichier Office.
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructeur [RMSOfficeFileException](class_mip_rmsofficefileexception.md).

Paramètres :  
* **message** : message de l’exception 


* **reason** : classification de l’erreur de fichier Office


  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructeur [RMSOfficeFileException](class_mip_rmsofficefileexception.md).

Paramètres :  
* **message** : message de l’exception 


* **reason** : classification de l’erreur de fichier Office


  
### <a name="reason"></a>Raison
Obtient la classification de l’erreur de fichier Office.

  
**Retourne** : classification de l’erreur de fichier Office
  
### <a name="what"></a>what
Obtient le message de l’exception.

  
**Retourne** : le message de l’exception
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtient le type d’exception.

  
**Retourne** : le type de l’exception
  
### <a name="error"></a>erreur
Obtient le code d’erreur.

  
**Retourne** : le code de [l’erreur](class_mip_error.md)