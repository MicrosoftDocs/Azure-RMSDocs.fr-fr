# <a name="class-mipprotectionprofileobserver"></a>mip::ProtectionProfile::Observer, classe 
Interface qui reçoit les notifications relatives à [ProtectionProfile](#classmip_1_1_protection_profile).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccessProtectionProfile > & profile,const std::shared_ptr< void > & context) | Appelé quand le chargement d’un profil a réussi.
public inline virtual void OnLoadFailure | Appelé quand le chargement d’un profil a provoqué une erreur.
## <a name="members"></a>Membres
### <a name="onloadsuccess"></a>OnLoadSuccess
Appelé quand le chargement d’un profil a réussi.
#### <a name="parameters"></a>Paramètres
* profile : référence au [ProtectionProfile](#classmip_1_1_protection_profile) créé
* context : le même contexte que celui passé à [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031). Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function, etc.) à [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) et ce même contexte est transmis tel quel à [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) ou [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)
### <a name="onloadfailure"></a>OnLoadFailure
Appelé quand le chargement d’un profil a provoqué une erreur.
#### <a name="parameters"></a>Paramètres
* error : [erreur](#classmip_1_1_error) qui s’est produite durant le chargement 
* context : le même contexte que celui passé à [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031). Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function, etc.) à [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) et ce même contexte est transmis tel quel à [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) ou [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)