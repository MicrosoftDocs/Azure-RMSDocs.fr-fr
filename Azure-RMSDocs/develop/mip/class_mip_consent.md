# <a name="class-mipconsent"></a>mip::Consent, classe 
Représente l’acceptation ou le refus d’un utilisateur d’autoriser une action.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const mip::ConsentResult& Result() const  |  Obtient le résultat d’une demande de consentement.
public void Result(const ConsentResult& value)  |  Définit le résultat d’une demande de consentement.
public mip::ConsentType Type() const  |  Obtient le type du consentement.
public const std::vector<std::string> Urls() const  |  Obtient les URL impliquées dans la demande de consentement.
public const std::string User() const  |  Obtient l’utilisateur (l’adresse e-mail) dont le consentement est demandé.
public const std::string Domain() const  |  Obtient le domaine associé à l’utilisateur dont le consentement est demandé.
  
## <a name="members"></a>Membres
  
### <a name="mipconsentresult"></a>mip::ConsentResult
Obtient le résultat d’une demande de consentement.
  
#### <a name="returns"></a>Returns
Résultat de la demande de consentement
  
### <a name="result"></a>Result
Définit le résultat d’une demande de consentement.
  
#### <a name="parameters"></a>Paramètres
* valeur : résultat de la demande de consentement
  
### <a name="mipconsenttype"></a>mip::ConsentType
Obtient le type du consentement.
  
#### <a name="returns"></a>Returns
Type du consentement
  
### <a name="urls"></a>Urls
Obtient les URL impliquées dans la demande de consentement.
  
#### <a name="returns"></a>Returns
URL impliquées dans la demande de consentement
  
### <a name="user"></a>Utilisateur
Obtient l’utilisateur (l’adresse e-mail) dont le consentement est demandé.
  
#### <a name="returns"></a>Returns
Utilisateur dont le consentement est demandé
  
### <a name="domain"></a>Domaine
Obtient le domaine associé à l’utilisateur dont le consentement est demandé.
  
#### <a name="returns"></a>Returns
Domaine associé à l’utilisateur dont le consentement est demandé