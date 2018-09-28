# <a name="class-miprmsnetworkexception"></a>mip::RMSNetworkException, classe 
Exception réseau RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public RMSNetworkException(const std::string& message, Reason reason)  |  Constructeur [RMSNetworkException](class_mip_rmsnetworkexception.md).
 public RMSNetworkException(const char*const& message, Reason reason)  |  Constructeur [RMSNetworkException](class_mip_rmsnetworkexception.md).
 public virtual Reason reason() const  |  Obtient la classification de l’erreur réseau.
 public virtual const char* what() const  |  Obtient le message de l’exception.
 public virtual ExceptionTypes type() const  |  Obtient le type d’exception.
 public virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructeur [RMSNetworkException](class_mip_rmsnetworkexception.md).

Paramètres :  
* **message** : message de l’exception 


* **reason** : classification de l’erreur réseau


  
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructeur [RMSNetworkException](class_mip_rmsnetworkexception.md).

Paramètres :  
* **message** : message de l’exception 


* **reason** : classification de l’erreur réseau


  
### <a name="reason"></a>Raison
Obtient la classification de l’erreur réseau.

  
**Retourne** : la classification de l’erreur réseau
  
### <a name="what"></a>what
Obtient le message de l’exception.

  
**Retourne** : le message de l’exception
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtient le type d’exception.

  
**Retourne** : le type de l’exception
  
### <a name="error"></a>erreur
Obtient le code d’erreur.

  
**Retourne** : le code de [l’erreur](class_mip_error.md)