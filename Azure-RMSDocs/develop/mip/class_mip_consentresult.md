# <a name="class-mipconsentresult"></a>mip::ConsentResult, classe 
Décrit le résultat de la demande de consentement après une interaction de l’utilisateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline ConsentResult(bool accepted, bool showAgain, const std::string& userId)  |  Constructeur [ConsentResult](#classmip_1_1_consent_result).
public inline bool Accepted() const  |  Obtient une valeur déterminant si l’utilisateur a consenti à l’action.
public inline bool ShowAgain() const  |  Obtient une valeur déterminant si un consentement explicite est requis pour les demandes ultérieures.
public inline const std::string& UserId() const  |  Obtient l’utilisateur (l’adresse e-mail) dont le consentement a été demandé.
  
## <a name="members"></a>Membres
  
### <a name="consentresult"></a>ConsentResult
Constructeur [ConsentResult](#classmip_1_1_consent_result).
  
#### <a name="parameters"></a>Paramètres
* accepted : Information indiquant si l’utilisateur a consenti à l’action ou non 
* showAgain : information indiquant si un consentement explicite est requis ou non pour les demandes d’action ultérieures 
* userId : utilisateur (adresse e-mail) dont le consentement a été demandé
  
### <a name="accepted"></a>Accepted
Obtient une valeur déterminant si l’utilisateur a consenti à l’action.
  
#### <a name="returns"></a>Returns
Valeur déterminant si l’utilisateur a consenti à l’action
  
### <a name="showagain"></a>ShowAgain
Obtient une valeur déterminant si un consentement explicite est requis pour les demandes ultérieures.
  
#### <a name="returns"></a>Returns
Valeur déterminant si un consentement explicite est requis pour les demandes ultérieures. Si la valeur true est retournée, le SDK mémorise le résultat de ce consentement et n’invite plus ultérieurement l’application cliente à donner son consentement.
  
### <a name="userid"></a>UserId
Obtient l’utilisateur (l’adresse e-mail) dont le consentement a été demandé.
  
#### <a name="returns"></a>Returns
Utilisateur dont le consentement a été demandé