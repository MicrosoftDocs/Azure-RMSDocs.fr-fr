# <a name="class-mipconsentcallback"></a>mip::ConsentCallback, classe 
Interface pour les notifications de demande de consentement.
Ce rappel est implémenté par une application cliente pour savoir quand une notification de consentement doit être présentée à l’utilisateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public ConsentList Consents(ConsentList& consents)  |  Appelé quand le SDK a besoin du consentement de l’utilisateur pour une opération.
  
## <a name="members"></a>Membres
  
### <a name="consentlist"></a>ConsentList
Appelé quand le SDK a besoin du consentement de l’utilisateur pour une opération.

Paramètres :  
* **consents** : liste des consentements demandés par le SDK



  
**Retourne** : les résultats du [consentement](class_mip_consent.md). Quand des consentements sont demandés par le SDK, l’application cliente doit obtenir le consentement de l’utilisateur, les résultats de chaque consentement doivent être stockés dans [Consent::Result(const ConsentResult&)](class_mip_consent.md#result) et une liste des consentements résolus doit être retournée.