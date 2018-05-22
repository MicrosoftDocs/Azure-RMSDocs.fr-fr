# <a name="class-miprmscryptographyexception"></a>mip::RMSCryptographyException, classe 
Exception de chiffrement RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSCryptographyException(const std::string& message)  |  Constructeur [RMSCryptographyException](class_mip_rmscryptographyexception.md).
 public RMSCryptographyException(const char*const& message)  |  Constructeur [RMSCryptographyException](class_mip_rmscryptographyexception.md).
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmscryptographyexception"></a>RMSCryptographyException
Constructeur [RMSCryptographyException](class_mip_rmscryptographyexception.md).

Paramètres :  
* **message** : message de l’exception


  
### <a name="rmscryptographyexception"></a>RMSCryptographyException
Constructeur [RMSCryptographyException](class_mip_rmscryptographyexception.md).

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