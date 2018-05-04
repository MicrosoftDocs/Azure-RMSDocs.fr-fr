# <a name="class-mipfilehandlerobserver"></a>mip::FileHandler::Observer, classe 
Interface [Observer](#classmip_1_1_file_handler_1_1_observer) permettant aux clients d’obtenir des notifications pour les événements liés aux gestionnaires de fichiers.
Si un événement *Error se produit, l’objet d’erreur est contenu dans la classe [mip::Error](#classmip_1_1_error). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public inline virtual  ~Observer | 
public void OnGetLabelSuccessContentLabel > & label,const std::shared_ptr< void > & context) | Appelé quand l’étiquette est récupérée avec succès (à partir du fichier).
public void OnGetLabelFailure | Appelé quand la récupération de l’étiquette (à partir du fichier) a échoué en raison d’une erreur.
public void OnGetProtectionSuccessUserPolicy > & userPolicy,const std::shared_ptr< void > & context) | Appelé quand la stratégie de protection est récupérée avec succès (à partir du fichier).
public void OnGetProtectionFailure | Appelé quand la récupération de la stratégie de protection (à partir du fichier) a échoué en raison d’une erreur.
public void OnCommitSuccess | Appelée quand la validation des modifications du fichier a réussi.
public void OnCommitFailure | Appelée quand la validation des modifications du fichier a échoué en raison d’une erreur.
protected inline  Observer | 
## <a name="members"></a>Membres
### <a name="observer"></a>~Observer
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
Appelé quand l’étiquette est récupérée avec succès (à partir du fichier).
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
Appelé quand la récupération de l’étiquette (à partir du fichier) a échoué en raison d’une erreur.
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
Appelé quand la stratégie de protection est récupérée avec succès (à partir du fichier).
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
Appelé quand la récupération de la stratégie de protection (à partir du fichier) a échoué en raison d’une erreur.
### <a name="oncommitsuccess"></a>OnCommitSuccess
Appelée quand la validation des modifications du fichier a réussi.
### <a name="oncommitfailure"></a>OnCommitFailure
Appelée quand la validation des modifications du fichier a échoué en raison d’une erreur.
### <a name="observer"></a>Observateur