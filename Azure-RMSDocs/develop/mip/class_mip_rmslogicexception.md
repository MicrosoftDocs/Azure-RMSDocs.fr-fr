# <a name="class-miprmslogicexception"></a>mip::RMSLogicException, classe 
Exception logique RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSLogicException(const ErrorTypes error, const std::string& message)  |  Constructeur [RMSLogicException](class_mip_rmslogicexception.md).
 public RMSLogicException(const ErrorTypes error, const char*const& message)  |  Constructeur [RMSLogicException](class_mip_rmslogicexception.md).
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmslogicexception"></a>RMSLogicException
Constructeur [RMSLogicException](class_mip_rmslogicexception.md).

Paramètres :  
* **error** : code de [l’erreur](class_mip_error.md) 


* **message** : message de l’exception


  
### <a name="rmslogicexception"></a>RMSLogicException
Constructeur [RMSLogicException](class_mip_rmslogicexception.md).

Paramètres :  
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