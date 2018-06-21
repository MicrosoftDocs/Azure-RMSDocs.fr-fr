# <a name="class-mipfilehandlerobserver"></a>mip::FileHandler::Observer, classe 
Interface [Observer](class_mip_filehandler_observer.md) permettant aux clients d’obtenir des notifications pour les événements liés aux gestionnaires de fichiers.
Si un événement *Error se produit, l’objet d’erreur est contenu dans la classe [mip::Error](class_mip_error.md). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _Pas encore documenté._
public void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Appelé quand l’étiquette est récupérée avec succès (à partir du fichier).
public void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand la récupération de l’étiquette (à partir du fichier) a échoué en raison d’une erreur.
public void OnGetProtectionSuccess(const std::shared_ptr<UserPolicy>& userPolicy, const std::shared_ptr<void>& context)  |  Appelé quand la stratégie de protection est récupérée avec succès (à partir du fichier).
public void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand la récupération de la stratégie de protection (à partir du fichier) a échoué en raison d’une erreur.
public void OnCommitSuccess(bool commited, const std::shared_ptr<void>& context)  |  Appelé quand la validation des modifications du fichier a réussi.
public void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand la validation des modifications du fichier a échoué en raison d’une erreur.
 protected Observer()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="observer"></a>~Observer
_Pas encore documenté._

  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
Appelé quand l’étiquette est récupérée avec succès (à partir du fichier).
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
Appelé quand la récupération de l’étiquette (à partir du fichier) a échoué en raison d’une erreur.
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
Appelé quand la stratégie de protection est récupérée avec succès (à partir du fichier).
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
Appelé quand la récupération de la stratégie de protection (à partir du fichier) a échoué en raison d’une erreur.
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
Appelé quand la validation des modifications du fichier a réussi.
  
### <a name="oncommitfailure"></a>OnCommitFailure
Appelé quand la validation des modifications du fichier a échoué en raison d’une erreur.
  
### <a name="observer"></a>Observateur
_Pas encore documenté._
