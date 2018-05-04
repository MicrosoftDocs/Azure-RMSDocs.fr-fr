# <a name="class-miprmslogicexception"></a>mip::RMSLogicException, classe 
Exception logique RMS.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  RMSLogicExceptionErrorTypes error,const std::string & message) public inline  RMSLogicExceptionErrorTypes error,const char *const & message) public inline virtual const char * what | Obtient le message d’exception.
public inline virtual ExceptionTypes type | Obtient le type d’exception.
public inline virtual int error | Obtient le code d’erreur.
## <a name="members"></a>Membres
### <a name="rmslogicexception"></a>RMSLogicException
Constructeur [RMSLogicException](#classmip_1_1_r_m_s_logic_exception).
#### <a name="parameters"></a>Paramètres
* error : code [Error](#classmip_1_1_error) 
* message : message de l’exception
### <a name="rmslogicexception"></a>RMSLogicException
Constructeur [RMSLogicException](#classmip_1_1_r_m_s_logic_exception).
#### <a name="parameters"></a>Paramètres
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
### <a name="error"></a>erreur
Obtient le code d’erreur.
#### <a name="returns"></a>Returns
Code [Error](#classmip_1_1_error)