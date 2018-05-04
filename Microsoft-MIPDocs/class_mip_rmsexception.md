# <a name="class-miprmsexception"></a>mip::RMSException, classe 
Exception de base RMS.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  RMSExceptionExceptionTypes type,const int error,const std::string & message) public inline  RMSExceptionExceptionTypes type,const int error,const char *const & message) public inline virtual const char * what | Obtient le message d’exception.
public inline virtual ExceptionTypes type | Obtient le type d’exception.
public inline virtual int error | Obtient le code d’erreur.
## <a name="members"></a>Membres
### <a name="rmsexception"></a>RMSException
Constructeur [RMSException](#classmip_1_1_r_m_s_exception).
#### <a name="parameters"></a>Paramètres
* type : type d’exception 
* error : code [Error](#classmip_1_1_error) 
* message : message de l’exception
### <a name="rmsexception"></a>RMSException
Constructeur [RMSException](#classmip_1_1_r_m_s_exception).
#### <a name="parameters"></a>Paramètres
* type : type d’exception 
* error : code [Error](#classmip_1_1_error) 
* message : message de l’exception
### <a name="what"></a>what
Obtient le message de l’exception.
#### <a name="returns"></a>Returns
Message de l’exception
### <a name="exceptiontypes"></a>ExceptionTypes
Obtient le type d’exception.
#### <a name="returns"></a>Returns
Type d'exception
### <a name="error"></a>error
Obtient le code d’erreur.
#### <a name="returns"></a>Returns
Code [Error](#classmip_1_1_error)