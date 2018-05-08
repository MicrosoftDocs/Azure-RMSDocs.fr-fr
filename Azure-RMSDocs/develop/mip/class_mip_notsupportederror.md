# <a name="class-mipnotsupportederror"></a>mip::NotSupportedError, classe 
Erreur d’opération non prise en charge.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline char const* what() const  |  Obtenir un message d’erreur cstring.
public std::shared_ptr<Error> Clone() const  |  Cloner l’erreur.
public inline virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public inline virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
public inline virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
public inline virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="what"></a>what
Obtenir un message d’erreur cstring.
  
#### <a name="returns"></a>Returns
un message d’erreur cstring
  
### <a name="error"></a>Erreur
Cloner l’erreur.
  
#### <a name="returns"></a>Returns
un clone de l’erreur.
  
### <a name="errortype"></a>ErrorType
Obtenir le type de l’erreur.
  
#### <a name="returns"></a>Returns
le type de l’erreur.
  
### <a name="geterrorname"></a>GetErrorName
Obtenir le nom de l’erreur.
  
#### <a name="returns"></a>Returns
le nom de l’erreur.
  
### <a name="getmessage"></a>GetMessage
Obtenir le message d’erreur.
  
#### <a name="returns"></a>Returns
le message d’erreur.
  
### <a name="setmessage"></a>SetMessage
Définir le message d’erreur.
  
#### <a name="parameters"></a>Paramètres
* msg : message d’erreur.