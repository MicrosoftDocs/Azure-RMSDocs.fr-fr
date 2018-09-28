# <a name="class-miprmsstreamexception"></a>mip::RMSStreamException, classe 
Exception de flux RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSStreamException(const std::string& message)  |  Constructeur [RMSStreamException](class_mip_rmsstreamexception.md).
 public RMSStreamException(const char*const& message)  |  Constructeur [RMSStreamException](class_mip_rmsstreamexception.md).
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmsstreamexception"></a>RMSStreamException
Constructeur [RMSStreamException](class_mip_rmsstreamexception.md).

Paramètres :  
* **message** : message de l’exception


  
### <a name="rmsstreamexception"></a>RMSStreamException
Constructeur [RMSStreamException](class_mip_rmsstreamexception.md).

Paramètres :  
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