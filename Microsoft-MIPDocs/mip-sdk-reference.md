# <a name="mip-sdk-for-c-preview-reference"></a>Référence du SDK MIP pour C++ (préversion)

Le SDK MIP (Microsoft Information Protection) pour C++ (préversion) permet aux développeurs de gérer des stratégies de protection des données et de les appliquer à des données et d’autres ressources numériques.  

Pour plus d’informations, consultez le [blog des développeurs MIP](https://aka.ms/MIPDevelopers) et les [exemples MIP](https://aka.ms/mipsdksamples).

Le SDK MIP pour C++ comprend les classes suivantes :

| Nom de la classe | Description |
| :----------|:------------|
[mip::Action](class_mip_action.md) | Classe de base pour toutes les actions. |
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md) | Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
[mip::addContentHeaderAction](class_mip_addcontentheaderaction.md) | Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md) | Classe d’action qui spécifie l’ajout d’un filigrane.
[mip::BadInputError](class_mip_badinputerror.md) | Erreur d’entrée incorrecte, l’entrée de l’API n’est pas valide.
[mip::CommonRights](class_mip_commonrights.md) | Droits universellement pris en charge.
[mip::Consent](class_mip_consent.md) | Représente l’acceptation ou le refus d’un utilisateur d’autoriser une action.
[mip::ConsentCallback](class_mip_consentcallback.md) | Interface pour les notifications de demande de consentement.
[mip::ConsentResult](class_mip_consentresult.md) | Décrit le résultat de la demande de consentement après une interaction de l’utilisateur.
[mip::ContentLabel](class_mip_contentlabel.md) | Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
[mip::CustomAction](class_mip_customaction.md) | Classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés.
[mip::CustomProtectedStream](class_mip_customprotectedstream.md) | Encapsule un flux pour fournir le chiffrement et le déchiffrement en lecture et en écriture de façon transparente.
[mip::EditableDocumentRights](class_mip_editabledocumentrights.md) | Droits qui s’appliquent aux documents modifiables.
[mip::EmailRights](class_mip_emailrights.md) | Droits qui s’appliquent aux e-mails.
[mip::Error](class_mip_error.md) | Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
[mip::ExecutionState](class_mip_executionstate.md) | Interface pour tous les états nécessaires à l’exécution du moteur.
[mip::EileEngine](class_mip_fileengine.md) | Interface pour toutes les fonctions du moteur.
[mip::FileEngine::Settings](class_mip_fileengine_settings.md) | 
[mip::FileHandler](class_mip_filehandler.md) | Interface pour toutes les fonctions de gestion de fichiers.
[mip::FileHandler::Observer](class_mip_filehandler_observer.md) | Interface Observer permettant aux clients d’obtenir les notifications des événements liés aux gestionnaires de fichiers.
[mip::FileIOError](class_mip_fileioerror.md) | Erreur d’E/S de fichier.
[mip::FileProfile](class_mip_fileprofile.md) | Classe de base pour les opérations Microsoft Information Protection.
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md) | Interface Observer utilisée pour recevoir les notifications d’événements liés aux profils.
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md) | Interface pour la gestion des paramètres de profils de fichiers.
[mip::GetUserPolicyResult](class_mip_getuserpolicyresult.md) | Décrit les résultats d’une demande d’acquisition de stratégie utilisateur.
[mip::InternalError](class_mip_internalerror.md) | Erreur interne du SDK. Un événement inattendu s’est produit.
[mip::IStream](class_mip_istream.md) | Interface de base pour les flux protégés.
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md) | La modification demandée nécessite une explication.
[mip::JustifyAction](class_mip_justifyaction.md) | La demande nécessite la justification du passage d’une étiquette à une version antérieure, ainsi que la définition de la réponse dans l’état d’exécution.
[mip::Label](class_mip_label.md) | Abstraction d’une étiquette unique Microsoft Information Protection.
[mip::LabelingOptions](class_mip_labelingoptions.md) | Interface pour la configuration des options d’étiquetage de la méthode SetLabel.
[mip::MetadataAction](class_mip_metadataaction.md) | Action spécifiant les informations de métadonnées à ajouter au contenu.
[mip::NetworkError](class_mip_networkerror.md) | Erreur de mise en réseau.
[mip::NotSupportedError](class_mip_notsupportederror.md) | Erreur d’opération non prise en charge.
[mip::PolicyDescriptor](class_mip_policydescriptor.md) | Représente une stratégie ad hoc associée à du contenu protégé.
[mip::PolicyEngine](class_mip_policyengine.md) | Cette classe fournit une interface pour toutes les fonctions de moteur.
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) | Une instance de cette classe avec les paramètres appropriés doit être fournie pour démarrer un moteur.
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md) | L’étiquette actuelle a été définie par une méthode d’assignation privilégiée et ne peut pas être substituée.
[mip::Profile](class_mip_profile.md) | Classe de base pour les opérations Microsoft Information Protection.
[mip::Profile::Observer](class_mip_profile_observer.md) | Interface utilisée pour recevoir les notifications d’événements liés aux profils.
[mip::Profile::Settings](class_mip_profile_settings.md) | Configure les paramètres de profil.
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md) | Classe d’action qui spécifie l’ajout de la protection ad hoc au document.  
[mip::ProtectbyTemplateAction](class_mip_protectbytemplateaction.md) | Classe d’action qui spécifie l’ajout de la protection par modèle au document.
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md) | Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
[mip::ProtectionProfile](class_mip_protectionprofile.md) | Classe de base utilisée pour effectuer des opérations de protection.
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) | Utilisée pour recevoir les notifications de profil de protection.
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) | Paramètres de profil de protection utilisés tout au long de la durée de vie de l’instance.
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md) | Classe d’action qui spécifie la suppression du pied de page de contenu du document.
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) | Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md) | Classe d’action qui spécifie la suppression de la protection appliquée au document.
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md) | Classe d’action qui spécifie la suppression du filigrane du document.
[mip::RMSCryptographyException](class_mip_rmscryptographyexception.md) | Exception de chiffrement RMS.
[mip::RMSException](class_mip_rmsexception.md) | Exception de base RMS.
[mip::RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) | Exception d’argument non valide RMS.
[mip::RMSLogicException](class_mip_rmslogicexception.md) | Exception logique RMS.
[mip::RMSNetworkException](class_mip_rmsnetworkexception.md) | Exception réseau RMS.
[mip::RMSNotFoundException](class_mip_rmsnotfoundexception.md) | Exception RMS introuvable.
[mip::RMSNullPointerException](class_mip_rmsnullpointerexception.md) | Exception de pointeur null RMS.
[mip::RMSOfficeFileException](class_mip_rmsofficefileexception.md) | Exception de fichier Office RMS.
[mip::RMSPFileException](class_mip_rmspfileexception.md) | Exception RMS PFile.
[mip::RMSRightsException](class_mip_rmsrightsexception.md) | Exception de droits RMS.
[mip::RMSStreamException](class_mip_rmsstreamexception.md) | Exception de flux RMS.
[mip::Roles](class_mip_roles.md) | Définit les rôles pour la protection des données.
[mip::Stream](class_mip_stream.md) | Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
[mip::TemplateDescriptor](class_mip_templatedescriptor.md) | Décrit un modèle RMS.
[mip::UserPolicy](class_mip_userpolicy.md) | Représente la stratégie associée au contenu protégé.
[mip::UserRights](class_mip_userrights.md) | Représente un groupe d’utilisateurs et les droits qui leur sont associés.
[mip::UserRoles](class_mip_userroles.md) | Représente un groupe d’utilisateurs et les rôles qui leur sont associés.
 
