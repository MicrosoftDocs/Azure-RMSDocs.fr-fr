# <a name="class-mipconsentcallback"></a>mip::ConsentCallback, classe 
Interface pour les notifications de demande de consentement.
Ce rappel est implémenté par une application cliente pour savoir quand une notification de consentement doit être présentée à l’utilisateur.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public ConsentList ConsentsConsentList & consents) | Appelé quand le SDK a besoin du consentement de l’utilisateur pour une opération.
## <a name="members"></a>Membres
### <a name="consentlist"></a>ConsentList
Appelé quand le SDK a besoin du consentement de l’utilisateur pour une opération.
#### <a name="parameters"></a>Paramètres
* consents : liste des consentements demandés par le SDK
#### <a name="returns"></a>Returns
Résultats [Consent](#classmip_1_1_consent). Quand des consentements sont demandés par le SDK, l’application cliente doit obtenir le consentement de l’utilisateur, les résultats de chaque consentement doivent être stockés dans [Consent::Result(const ConsentResult&)](#classmip_1_1_consent_1ad6c17d9af548a40b2fe854fe0d9bca64) et une liste des consentements résolus doit être retournée.