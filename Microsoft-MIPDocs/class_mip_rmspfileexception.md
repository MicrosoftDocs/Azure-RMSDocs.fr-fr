# <a name="class-miprmspfileexception"></a>mip::RMSPFileException, classe 
Exception RMS PFile.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  RMSPFileExceptionReason reason) public inline  RMSPFileExceptionReason reason) public inline virtual Reason reason | Obtient la classification de l’erreur PFile.
public inline virtual const char * what | Obtient le message de l’exception.
public inline virtual ExceptionTypes type | Obtient le type d’exception.
public inline virtual int error | Obtient le code d’erreur.
## <a name="members"></a>Membres
### <a name="rmspfileexception"></a>RMSPFileException
Constructeur [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception).
#### <a name="parameters"></a>Paramètres
* message : message de l’exception 
* reason : classification de l’erreur PFile
### <a name="rmspfileexception"></a>RMSPFileException
Constructeur [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception).
#### <a name="parameters"></a>Paramètres
* message : message de l’exception 
* reason : classification de l’erreur PFile
### <a name="reason"></a>Raison
Obtenir la classification de l’erreur PFile.
#### <a name="returns"></a>Returns
la classification de l’erreur PFile
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