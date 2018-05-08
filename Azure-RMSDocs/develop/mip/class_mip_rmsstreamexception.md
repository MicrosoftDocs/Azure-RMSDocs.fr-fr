# <a name="class-miprmsstreamexception"></a>mip::RMSStreamException, classe 
Exception de flux RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline RMSStreamException(const std::string& message)  |  Constructeur [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
public inline RMSStreamException(const char*const& message)  |  Constructeur [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
public inline virtual const char* what() const  |  Obtient le message de l’exception.
public inline virtual ExceptionTypes type() const  |  Obtient le type d’exception.
public inline virtual int error() const  |  Obtient le code d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="rmsstreamexception"></a>RMSStreamException
Constructeur [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
  
#### <a name="parameters"></a>Paramètres
* message : message de l’exception
  
### <a name="rmsstreamexception"></a>RMSStreamException
Constructeur [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
  
#### <a name="parameters"></a>Paramètres
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
Code [d’erreur](#classmip_1_1_error)