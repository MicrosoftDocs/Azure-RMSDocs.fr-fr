# <a name="class-mipprotectionprofileobserver"></a>mip::ProtectionProfile::Observer, classe 
Interface qui reçoit les notifications relatives à [ProtectionProfile](class_mip_protectionprofile.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **profile** : référence au [ProtectionProfile](class_mip_protectionprofile.md) nouvellement créé


* **context** : le même contexte que celui qui a été passé à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)


Une application peut passer n’importe quel type de contexte (par exemple std::promise, std::function, etc.) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) ou à [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **error** : [erreur](class_mip_error.md) qui s’est produite lors du chargement 


* **context** : le même contexte que celui qui a été passé à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)


Une application peut passer n’importe quel type de contexte (par exemple std::promise, std::function, etc.) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) ou à [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)