# <a name="class-mipprofileobserver"></a>mip::Profile::Observer, classe 
Interface [Observer](class_mip_profile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
Si un événement *Error se produit, l’objet d’erreur est contenu dans la classe [mip::Error](class_mip_error.md). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<Profile>& profile, const std::shared_ptr<void>& context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  Appelé quand le déchargement d’un moteur a réussi.
public virtual void OnUnloadEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand le déchargement d’un moteur a provoqué une erreur.
public virtual void OnAddEngineSuccess(const std::shared_ptr<PolicyEngine>& engine, const std::shared_ptr<void>& context)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
 public virtual void OnPolicyChanged(const std::string& engineId)  |  Appelé quand la stratégie a été changée pour le moteur avec l’ID spécifié.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **profile** : profil actuel utilisé pour démarrer l’opération. 


* **context** : contexte passé à l’opération.


  
### <a name="onloadfailure"></a>OnLoadFailure
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de chargement. 


* **context** : contexte passé à l’opération.


  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **context** : contexte passé à l’opération.


  
### <a name="onlistengineserror"></a>OnListEnginesError
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **context** : contexte passé à l’opération.


  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Appelé quand le déchargement d’un moteur a réussi.

Paramètres :  
* **context** : contexte passé à l’opération.


  
### <a name="onunloadengineerror"></a>OnUnloadEngineError
Appelé quand le déchargement d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de déchargement du moteur. 


* **context** : contexte passé à l’opération.


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Appelé quand l’ajout d’un nouveau moteur a réussi.
  
### <a name="onaddengineerror"></a>OnAddEngineError
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **context** : contexte passé à l’opération.


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **context** : contexte passé à l’opération.


  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **context** : contexte passé à l’opération.


  
### <a name="onpolicychanged"></a>OnPolicyChanged
Appelé quand la stratégie a été changée pour le moteur avec l’ID spécifié.

Paramètres :  
* **engineId** : moteur 


Pour charger la nouvelle stratégie, il est nécessaire de rappeler AddEngineAsync avec l’ID de moteur donné.