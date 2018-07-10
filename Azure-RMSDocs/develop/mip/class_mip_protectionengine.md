# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
Effectue des actions liées à la protection sur une identité spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtient les paramètres du moteur.
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection à partir de sa forme sérialisée.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtient les paramètres du moteur.

  
**Retourne**  : les paramètres du moteur
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **observer** : classe qui implémente l’interface [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context** : ce même contexte sera transféré à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) ou [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)


  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **descriptor** : un [ProtectionDescriptor](class_mip_protectiondescriptor.md) décrivant la configuration de la protection 


* **options** : options de création 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context** : ce même contexte sera transféré à [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) ou ProtectionHandler::Observer::OnCreateProtectionHandlerFailure


  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
Crée un gestionnaire de protection à partir de sa forme sérialisée.

Paramètres :  
* **serializedPublishingLicense** : licence de publication sérialisée 


* **options** : options de création 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context** : ce même contexte sera transféré à [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) ou ProtectionHandler::Observer::OnCreateProtectionHandlerFailure

