# <a name="mip-sdk-for-c-preview-reference"></a>Référence du SDK MIP pour C++ (préversion)

Le SDK MIP (Microsoft Information Protection) pour C++ (préversion) permet aux développeurs de gérer des stratégies de protection des données et de les appliquer à des données et d’autres ressources numériques.  

Pour plus d’informations, consultez le [blog des développeurs MIP](https://aka.ms/MIPDevelopers) et les [exemples MIP](https://aka.ms/mipsdksamples).

Le SDK MIP pour C++ inclut :

- [Énumérations et structures](mip-enums-and-structs.md)
- [Fonctions](mip-functions.md)
- Les classes suivantes :

| Nom de la classe | Description |
| :----------|:------------|
[ConsentDelegate](class_consentdelegate.md)  |  Délégué pour les opérations relatives au consentement.
[mip::AccessDeniedError](class_mip_accessdeniederror.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué, etc.
[mip::Action](class_mip_action.md)  |  Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
[mip::AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Classe d’action qui spécifie l’ajout d’un filigrane.
[mip::ApplyLabelAction](class_mip_applylabelaction.md)  |  Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
[mip::BadInputError](class_mip_badinputerror.md)  |  Erreur d’entrée incorrecte, levée lorsque l’entrée dans une API SDK n’est pas valide.
[mip::ClassificationResult](class_mip_classificationresult.md)  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
[mip::ContentLabel](class_mip_contentlabel.md)  |  Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
[mip::CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
[mip::Error](class_mip_error.md)  |  Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
[mip::ExecutionState](class_mip_executionstate.md)  |  Interface pour tous les états nécessaires à l’exécution du moteur.
[mip::FileEngine](class_mip_fileengine.md)  |  Interface pour toutes les fonctions du moteur.
[mip::FileEngine::Settings](class_mip_fileengine::settings.md)  | _Pas encore documenté._
[mip::FileHandler](class_mip_filehandler.md)  |  Interface pour toutes les fonctions de gestion de fichiers.
[mip::FileHandler::Observer](class_mip_filehandler::observer.md)  |  Interface [Observer](class_mip_filehandler_observer.md) permettant aux clients d’obtenir des notifications pour les événements liés aux gestionnaires de fichiers.
[mip::FileIOError](class_mip_fileioerror.md)  |  Erreur d’E/S de fichier.
[mip::FileProfile](class_mip_fileprofile.md)  |  La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md)  |  Interface [Observer](class_mip_fileprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md)  |  [Settings](class_mip_fileprofile_settings.md) utilisé par [FileProfile](class_mip_fileprofile.md) lors de sa création et tout au long de sa durée de vie.
[mip::InternalError](class_mip_internalerror.md)  |  Erreur interne. Cette erreur est levée quand un événement inattendu se produit pendant l’exécution.
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md)  | _Pas encore documenté._
[mip::JustifyAction](class_mip_justifyaction.md)  |  Justify [Action](class_mip_action.md) nécessite de fournir une justification de rétrogradation d’une étiquette et de définir la réponse dans l’état d’exécution.
[mip::Label](class_mip_label.md)  |  Abstraction d’une étiquette unique Microsoft Information Protection.
[mip::LabelingOptions](class_mip_labelingoptions.md)  |  Interface pour la configuration des options d’étiquetage de la méthode SetLabel.
[mip::LoggerDelegate](class_mip_loggerdelegate.md)  |  Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
[mip::MetadataAction](class_mip_metadataaction.md)  |  Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
[mip::NetworkError](class_mip_networkerror.md)  |  Erreur de mise en réseau. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service.
[mip::NotSupportedError](class_mip_notsupportederror.md)  |  L’opération demandée par l’application n’est pas prise en charge par le Kit SDK.
[mip::PolicyEngine](class_mip_policyengine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  Une instance de cette classe avec les paramètres appropriés doit être fournie pour démarrer un moteur.
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
[mip::Profile](class_mip_profile.md)  |  La classe [Profile](class_mip_profile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [Profile](class_mip_profile.md), mais elle peut créer plusieurs profils si nécessaire.
[mip::Profile::Observer](class_mip_profile_observer.md)  |  Interface [Observer](class_mip_profile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
[mip::Profile::Settings](class_mip_profile_settings.md)  |  [Settings](class_mip_profile_settings.md) utilisé par [Profile](class_mip_profile.md) lors de sa création et tout au long de sa durée de vie.
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md)  |  Classe d’action qui spécifie l’ajout de la protection ad hoc au document.
[mip::ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Classe d’action qui spécifie l’ajout de la protection par modèle au document.
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
[mip::ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  Représente une stratégie ad hoc associée à du contenu protégé.
[mip::ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Représente une stratégie ad hoc associée à du contenu protégé.
[mip::ProtectionEngine](class_mip_protectionengine.md)  |  Effectue des actions liées à la protection sur une identité spécifique.
[mip::ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  Interface qui reçoit les notifications relatives à [ProtectionEngine](class_mip_protectionengine.md).
[mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  [Settings](class_mip_protectionengine_settings.md) utilisé par [ProtectionEngine](class_mip_protectionengine.md) lors de sa création et tout au long de sa durée de vie.
[mip::ProtectionHandler](class_mip_protectionhandler.md)  |  Effectue des actions liées à la protection pour une configuration de protection spécifique (par exemple, utilisateurs, droits, rôles, etc.)
[mip::ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)  |  Interface qui reçoit les notifications relatives à [ProtectionHandler](class_mip_protectionhandler.md).
[mip::ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  Interface qui reçoit les notifications relatives à [ProtectionProfile](class_mip_protectionprofile.md).
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  [Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de sa création et tout au long de sa durée de vie.
[mip::RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Classe d’action qui spécifie la suppression du pied de page de contenu du document.
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Classe d’action qui spécifie la suppression de la protection appliquée au document.
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Classe d’action qui spécifie la suppression du filigrane du document.
[mip::Stream](class_mip_stream.md)  |  Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
[mip::UserRights](class_mip_userrights.md)  |  Représente un groupe d’utilisateurs et les droits qui leur sont associés.
[mip::UserRoles](class_mip_userroles.md)  |  Représente un groupe d’utilisateurs et les rôles qui leur sont associés.

 
