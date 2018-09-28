# <a name="class-miprmsexception"></a>mip::RMSException, classe 
Exception de base RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSException(const ExceptionTypes type, const int error, const std::string& message)  |  Constructeur [RMSException](class_mip_rmsexception.md).
 public RMSException(const ExceptionTypes type, const int error, const char*const& message)  |  Constructeur [RMSException](class_mip_rmsexception.md).
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmsexception"></a>RMSException
Constructeur [RMSException](class_mip_rmsexception.md).

Paramètres :  
* **type** : type d’exception 


* **error** : code de [l’erreur](class_mip_error.md) 


* **message** : message de l’exception


  
### <a name="rmsexception"></a>RMSException
Constructeur [RMSException](class_mip_rmsexception.md).

Paramètres :  
* **type** : type d’exception 


* **error** : code de [l’erreur](class_mip_error.md) 


* **message** : message de l’exception


  
### <a name="what"></a>what
Obtient le message de l’exception.

  
**Retourne** : le message de l’exception
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtient le type d’exception.

  
**Retourne** : le type de l’exception
  
### <a name="error"></a>erreur
Obtient le code d’erreur.

  
**Retourne** : le code de [l’erreur](class_mip_error.md)