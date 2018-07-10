# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
Interface qui reçoit les notifications relatives à [ProtectionEngine](class_mip_protectionengine.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  Appelé lorsque les modèles ont été récupérés.
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé lorsque la récupération de modèles a généré une erreur.
  
## <a name="members"></a>Membres
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
Appelé lorsque les modèles ont été récupérés.

Paramètres :  
* **templateIds** : récupère une référence à la liste des modèles 


* **context** : le même contexte que celui transmis à [ProtectionProfile::LoadAsync](class_mip_protectionengine.md#gettemplatesasync)


Une application peut transmettre n’importe quel type de contexte (par exemple std::promise, std::function, etc.) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure).
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
Appelé lorsque la récupération de modèles a généré une erreur.

Paramètres :  
* **error** : [Erreur](class_mip_error.md) qui s’est produite lors de la récupérationde modèles 


* **context** : le même contexte que celui transmis à [ProtectionProfile::LoadAsync](class_mip_protectionengine.md#gettemplatesasync)


Une application peut transmettre n’importe quel type de contexte (par exemple std::promise, std::function, etc.) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure).