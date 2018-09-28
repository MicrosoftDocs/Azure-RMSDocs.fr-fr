# <a name="class-consentdelegate"></a>classe ConsentDelegate 
Délégué pour les opérations relatives au consentement.
Ce délégué est implémenté par une application cliente pour savoir quand une notification de requête de consentement doit être présentée à l’utilisateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public Consent GetUserConsent(const std::string& url)  |  Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.
  
## <a name="members"></a>Membres
  
### <a name="consent"></a>Consent
Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.

Paramètres :  
* **url** : URL pour laquelle le Kit SDK nécessite le consentement de l’utilisateur



  
**Retourne** : énum de consentement avec la décision de l’utilisateur.
Lorsque le Kit SDK requiert le consentement de l’utilisateur avec cette méthode, l’application cliente doit présenter l’URL à l’utilisateur. Les applications clientes doivent fournir un moyen d’obtenir le consentement de l’utilisateur et retourner l’énum de consentement appropriée qui correspond à la décision de l’utilisateur.