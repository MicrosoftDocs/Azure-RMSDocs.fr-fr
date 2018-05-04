# <a name="class-mipfileprofileobserver"></a>mip::FileProfile::Observer, classe 
Interface [Observer](#classmip_1_1_file_profile_1_1_observer) permettant aux clients d’obtenir des notifications pour les événements liés aux profils.
Si un événement *Error se produit, l’objet d’erreur est contenu dans la classe [mip::Error](#classmip_1_1_error). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline virtual  ~Observer | 
public inline virtual void OnLoadSuccessmip::FileProfile > & profile,const std::shared_ptr< void > & context) | Appelé quand le chargement du profil a réussi.
public inline virtual void OnLoadFailure | Appelé quand le chargement d’un profil a provoqué une erreur.
public inline virtual void OnListEnginesSuccess | Appelé quand la liste des moteurs a été générée avec succès.
public inline virtual void OnListEnginesError | Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public inline virtual void OnUnloadEngineSuccess | Appelé quand le déchargement d’un moteur a réussi.
public inline virtual void OnUnloadEngineError | Appelé quand le déchargement d’un moteur a provoqué une erreur.
public inline virtual void OnAddEngineSuccessmip::FileEngine > & engine,const std::shared_ptr< void > & context) | Appelée quand l’ajout d’un nouveau moteur a réussi.
public inline virtual void OnAddEngineError | Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public inline virtual void OnDeleteEngineSuccess | Appelé quand la suppression d’un moteur a réussi.
public inline virtual void OnDeleteEngineError | Appelé quand la suppression d’un moteur a provoqué une erreur.
public inline virtual void OnPolicyChanged | Appelé quand la stratégie a été modifiée pour le moteur avec l’ID spécifié.
protected inline  Observer | 
## <a name="members"></a>Membres
### <a name="observer"></a>~Observer
### <a name="onloadsuccess"></a>OnLoadSuccess
Appelé quand le chargement du profil a réussi.
### <a name="onloadfailure"></a>OnLoadFailure
Appelé quand le chargement d’un profil a provoqué une erreur.
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Appelé quand la liste des moteurs a été générée avec succès.
### <a name="onlistengineserror"></a>OnListEnginesError
Appelé quand la génération de la liste de moteurs a provoqué une erreur.
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Appelé quand le déchargement d’un moteur a réussi.
### <a name="onunloadengineerror"></a>OnUnloadEngineError
Appelé quand le déchargement d’un moteur a provoqué une erreur.
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Appelée quand l’ajout d’un nouveau moteur a réussi.
### <a name="onaddengineerror"></a>OnAddEngineError
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Appelé quand la suppression d’un moteur a réussi.
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Appelé quand la suppression d’un moteur a provoqué une erreur.
### <a name="onpolicychanged"></a>OnPolicyChanged
Appelé quand la stratégie a été modifiée pour le moteur avec l’ID spécifié.
### <a name="observer"></a>Observateur