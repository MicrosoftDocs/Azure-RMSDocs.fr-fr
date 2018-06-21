# <a name="class-miprmsrightsexception"></a>mip::RMSRightsException, classe 
Exception de droits RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSRightsException(const std::string& message)  |  Constructeur [RMSRightsException](class_mip_rmsrightsexception.md).
 public RMSRightsException(const char*const& message)  |  Constructeur [RMSRightsException](class_mip_rmsrightsexception.md).
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmsrightsexception"></a>RMSRightsException
Constructeur [RMSRightsException](class_mip_rmsrightsexception.md).

Paramètres :  
* **message** : message de l’exception


  
### <a name="rmsrightsexception"></a>RMSRightsException
Constructeur [RMSRightsException](class_mip_rmsrightsexception.md).

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