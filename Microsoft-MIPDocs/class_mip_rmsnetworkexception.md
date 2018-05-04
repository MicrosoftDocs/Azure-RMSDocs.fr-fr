# <a name="class-miprmsnetworkexception"></a>mip::RMSNetworkException, classe 
Exception réseau RMS.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  RMSNetworkExceptionReason reason) public inline  RMSNetworkExceptionReason reason) public inline virtual Reason reason | Obtient la classification de l’erreur réseau.
public inline virtual const char * what | Obtient le message de l’exception.
public inline virtual ExceptionTypes type | Obtient le type d’exception.
public inline virtual int error | Obtient le code d’erreur.
## <a name="members"></a>Membres
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructeur [RMSNetworkException](#classmip_1_1_r_m_s_network_exception).
#### <a name="parameters"></a>Paramètres
* message : message de l’exception 
* reason : classification de l’erreur réseau
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructeur [RMSNetworkException](#classmip_1_1_r_m_s_network_exception).
#### <a name="parameters"></a>Paramètres
* message : message de l’exception 
* reason : classification de l’erreur réseau
### <a name="reason"></a>Reason
Obtient la classification de l’erreur réseau.
#### <a name="returns"></a>Returns
Classification de l’erreur réseau
### <a name="what"></a>what
Obtient le message de l’exception.
#### <a name="returns"></a>Returns
Message de l’exception
### <a name="exceptiontypes"></a>ExceptionTypes
Obtient le type d’exception.
#### <a name="returns"></a>Returns
Type d'exception
### <a name="error"></a>erreur
Obtient le code d’erreur.
#### <a name="returns"></a>Returns
Code [Error](#classmip_1_1_error)