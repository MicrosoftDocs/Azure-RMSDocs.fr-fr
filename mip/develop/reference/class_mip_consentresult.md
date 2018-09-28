# <a name="class-mipconsentresult"></a>mip::ConsentResult, classe 
Décrit le résultat de la demande de consentement après une interaction de l’utilisateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public ConsentResult(bool accepted, bool showAgain, const std::string& userId)  |  Constructeur [ConsentResult](class_mip_consentresult.md).
 public bool Accepted() const  |  Obtient une valeur déterminant si l’utilisateur a consenti à l’action.
 public bool ShowAgain() const  |  Obtient une valeur déterminant si un consentement explicite est requis pour les demandes ultérieures.
 public const std::string& UserId() const  |  Obtient l’utilisateur (l’adresse e-mail) dont le consentement a été demandé.
  
## <a name="members"></a>Membres
  
### <a name="consentresult"></a>ConsentResult
Constructeur [ConsentResult](class_mip_consentresult.md).

Paramètres :  
* **accepted** : valeur indiquant si l’utilisateur a consenti ou non à l’action 


* **showAgain** : valeur indiquant si un consentement explicite est nécessaire ou non pour les demandes d’action ultérieures 


* **userId** : utilisateur (adresse e-mail) dont le consentement a été demandé


  
### <a name="accepted"></a>Accepted
Obtient une valeur déterminant si l’utilisateur a consenti à l’action.

  
**Retourne** : une valeur indiquant si l’utilisateur a consenti ou non à l’action
  
### <a name="showagain"></a>ShowAgain
Obtient une valeur déterminant si un consentement explicite est requis pour les demandes ultérieures.

  
**Retourne** : une valeur indiquant si un consentement explicite est nécessaire ou non pour les demandes ultérieures. Si la valeur true est retournée, le SDK mémorise le résultat de ce consentement et ne demande plus son consentement à l’application cliente.
  
### <a name="userid"></a>UserId
Obtient l’utilisateur (l’adresse e-mail) dont le consentement a été demandé.

  
**Retourne** : l’utilisateur dont le consentement a été demandé