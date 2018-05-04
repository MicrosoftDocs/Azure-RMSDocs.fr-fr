# <a name="class-mipconsentresult"></a>class mip::ConsentResult 
Décrit le résultat de la demande de consentement après interaction de l’utilisateur.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline  ConsentResult public inline bool Accepted | Obtient une information indiquant si l’utilisateur a consenti à l’action ou non.
public inline bool ShowAgain | Obtient une information indiquant si un consentement explicite est requis pour les demandes ultérieures ou non.
public inline const std::string & UserId | Obtient l’utilisateur (adresse e-mail) dont le consentement a été demandé.
## <a name="members"></a>Membres
### <a name="consentresult"></a>ConsentResult
Constructeur [ConsentResult](#classmip_1_1_consent_result).
#### <a name="parameters"></a>Paramètres
* accepted : Information indiquant si l’utilisateur a consenti à l’action ou non 
* showAgain : information indiquant si un consentement explicite est requis ou non pour les demandes d’action ultérieures 
* userId : utilisateur (adresse e-mail) dont le consentement a été demandé
### <a name="accepted"></a>Accepted
Obtient une information indiquant si l’utilisateur a consenti à l’action ou non.
#### <a name="returns"></a>Returns
Information indiquant si l’utilisateur a consenti à l’action ou non
### <a name="showagain"></a>ShowAgain
Obtient une information indiquant si un consentement explicite est requis ou non pour les demandes ultérieures.
#### <a name="returns"></a>Returns
Information indiquant si un consentement explicite est requis ou non pour les demandes ultérieures. Si tel est le cas, le SDK conserve le résultat de ce consentement et n’invite pas l’application cliente à donner son consentement à l’avenir.
### <a name="userid"></a>UserId
Obtient l’utilisateur (adresse e-mail) dont le consentement a été demandé.
#### <a name="returns"></a>Returns
Utilisateur dont le consentement a été demandé