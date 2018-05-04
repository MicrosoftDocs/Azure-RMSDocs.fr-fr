# <a name="class-miprmsofficefileexception"></a>mip::RMSOfficeFileException, classe 
Exception de fichier Office RMS.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  RMSOfficeFileExceptionReason reason) public inline  RMSOfficeFileExceptionReason reason) public inline virtual Reason reason | Obtient la classification de l’erreur de fichier Office.
public inline virtual const char * what | Obtient le message de l’exception.
public inline virtual ExceptionTypes type | Obtient le type d’exception.
public inline virtual int error | Obtient le code d’erreur.
## <a name="members"></a>Membres
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructeur [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
#### <a name="parameters"></a>Paramètres
* message : message de l’exception 
* reason : classification de l’erreur de fichier Office
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructeur [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
#### <a name="parameters"></a>Paramètres
* message : message de l’exception 
* reason : classification de l’erreur de fichier Office
### <a name="reason"></a>Raison
Obtient la classification de l’erreur de fichier Office.
#### <a name="returns"></a>Returns
Classification de l’erreur de fichier Office
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