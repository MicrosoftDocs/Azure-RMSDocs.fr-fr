---
title: SDK MIP pour C++ référence
description: SDK MIP pour C++ référence
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 69896e60fcf8aa33b2181fd22aeda803ab35b1cf
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555991"
---
# <a name="mip-sdk-for-c-reference"></a>SDK MIP pour C++ référence

Le kit de développement logiciel (SDK) C++ Microsoft information protection pour permet aux développeurs de gérer et d’appliquer des stratégies de protection des données à des données et à d’autres ressources numériques.

Le SDK MIP pour C++ inclut :

- [Énumérations et structures](mip-enums-and-structs.md)
- [Fonctions](mip-functions.md)
- Les classes suivantes :

 Class                         | Description                                
--------------------------------|---------------------------------------------
[MIP :: AccessDeniedError, classe](class_mip_accessdeniederror.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
[MIP :: action de classe](class_mip_action.md)  |  Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
[MIP :: ActionData, classe](class_mip_actiondata.md)  | Pas encore documenté.
[MIP :: AddContentFooterAction, classe](class_mip_addcontentfooteraction.md)  |  Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
[MIP :: AddContentHeaderAction, classe](class_mip_addcontentheaderaction.md)  |  Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
[MIP :: AddWatermarkAction, classe](class_mip_addwatermarkaction.md)  |  Classe d’action qui spécifie l’ajout d’un filigrane.
[MIP :: AddWatermarkActionData, classe](class_mip_addwatermarkactiondata.md)  | Pas encore documenté.
[MIP :: AdhocProtectionRequiredError, classe](class_mip_adhocprotectionrequirederror.md)  |  La protection ad hoc doit être configurée pour terminer l’action sur le fichier.
[MIP :: ApplicationActionState, classe](class_mip_applicationactionstate.md)  | Pas encore documenté.
[MIP :: ApplyLabelAction, classe](class_mip_applylabelaction.md)  |  Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
[MIP :: ArgumentData, classe](class_mip_argumentdata.md)  | Pas encore documenté.
[MIP :: AuthDelegate, classe](class_mip_authdelegate.md)  |  Délégué pour les opérations liées à l’authentification.
[MIP :: AuthDelegate :: OAuth2Challenge, classe](class_mip_authdelegate_oauth2challenge.md)  |  classe qui contient toutes les informations requises de l’application appelante afin de générer un jeton oauth2.
[MIP :: AuthDelegate :: OAuth2Token, classe](class_mip_authdelegate_oauth2token.md)  |  Classe définissant comment le kit de développement logiciel MIP s’attend à ce que le jeton oauth2 soit renvoyé dans le kit de développement logiciel (SDK).
[MIP :: BadInputError, classe](class_mip_badinputerror.md)  |  Erreur d’entrée incorrecte, levée quand l’entrée dans une API SDK n’est pas valide.
[MIP :: ClassificationData, classe](class_mip_classificationdata.md)  | Pas encore documenté.
[MIP :: ClassificationRequest, classe](class_mip_classificationrequest.md)  |  Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
[MIP :: ClassificationResult, classe](class_mip_classificationresult.md)  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
[MIP :: ComputeEngine, classe](class_mip_computeengine.md)  | Pas encore documenté.
[MIP :: ComputeEngine :: Settings, classe](class_mip_computeengine_settings.md)  | Pas encore documenté.
[MIP :: ComputeEngineContext, classe](class_mip_computeenginecontext.md)  | Pas encore documenté.
[MIP :: ConditionData, classe](class_mip_conditiondata.md)  | Pas encore documenté.
[MIP :: ConsentDelegate, classe](class_mip_consentdelegate.md)  |  Délégué pour les opérations relatives au consentement.
[MIP :: ConsentDeniedError, classe](class_mip_consentdeniederror.md)  |  Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
[MIP :: ContentLabel, classe](class_mip_contentlabel.md)  |  Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
[MIP :: ContentMarkingActionData, classe](class_mip_contentmarkingactiondata.md)  | Pas encore documenté.
[MIP :: CustomAction de classe](class_mip_customaction.md)  |  CustomAction est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un conteneur de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
[MIP de classe ::D eprecatedApiError](class_mip_deprecatedapierror.md)  |  L’appelant a appelé une API déconseillée.
[MIP de classe ::D ocumentState](class_mip_documentstate.md)  | Pas encore documenté.
[MIP :: Error, classe](class_mip_error.md)  |  Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
[MIP :: ExecutionState, classe](class_mip_executionstate.md)  |  Interface pour tous les états nécessaires à l’exécution du moteur.
[MIP :: FileEngine, classe](class_mip_fileengine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[MIP :: FileEngine :: Settings, classe](class_mip_fileengine_settings.md)  | Pas encore documenté.
[MIP :: FileExecutionState, classe](class_mip_fileexecutionstate.md)  | Pas encore documenté.
[MIP :: FileHandler, classe](class_mip_filehandler.md)  |  Interface pour toutes les fonctions de gestion de fichiers.
[MIP :: FileHandler :: observer, classe](class_mip_filehandler_observer.md)  |  Interface observer permettant aux clients d’obtenir des événements de notification liés au gestionnaire de fichiers.
[MIP :: FileInspector, classe](class_mip_fileinspector.md)  | Pas encore documenté.
[MIP :: FileIOError, classe](class_mip_fileioerror.md)  |  Erreur d’E/S de fichier.
[MIP :: FileProfile, classe](class_mip_fileprofile.md)  |  La classe FileProfile est la classe racine pour l’utilisation des opérations Microsoft Information Protection.
[MIP :: FileProfile :: observer, classe](class_mip_fileprofile_observer.md)  |  Interface observer permettant aux clients d’obtenir des notifications pour les événements liés au profil.
[MIP :: FileProfile :: Settings, classe](class_mip_fileprofile_settings.md)  |  Paramètres utilisés par FileProfile lors de sa création et tout au long de sa durée de vie.
[MIP :: HttpDelegate, classe](class_mip_httpdelegate.md)  |  Interface pour le remplacement de la gestion HTTP.
[MIP :: HttpOperation, classe](class_mip_httpoperation.md)  |  Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors du remplacement de HttpDelegate.
[MIP :: HttpRequest de la classe](class_mip_httprequest.md)  |  Interface qui décrit une seule requête HTTP.
[MIP :: HttpResponse, classe](class_mip_httpresponse.md)  |  Interface qui décrit une réponse HTTP unique, implémentée par l’application cliente lors du remplacement de HttpDelegate.
[MIP :: Identity, classe](class_mip_identity.md)  |  Abstraction pour l’identité.
[MIP :: InternalError, classe](class_mip_internalerror.md)  |  Erreur interne. Cette erreur est levée quand un événement inattendu se produit pendant l’exécution.
[MIP :: JustificationRequiredError, classe](class_mip_justificationrequirederror.md)  | Pas encore documenté.
[MIP :: JustifyAction, classe](class_mip_justifyaction.md)  |  Justifier l’action nécessite de fournir une justification à une mise à niveau de l’étiquette et de définir la réponse dans l’état d’exécution.
[MIP :: label, classe](class_mip_label.md)  |  Abstraction d’une étiquette unique Microsoft Information Protection.
[MIP :: LabelActionData, classe](class_mip_labelactiondata.md)  | Pas encore documenté.
[MIP :: LabelDisabledError, classe](class_mip_labeldisablederror.md)  |  L’étiquette est désactivée ou inactive.
[MIP :: LabelGroupData, classe](class_mip_labelgroupdata.md)  | Pas encore documenté.
[MIP :: LabelingOptions, classe](class_mip_labelingoptions.md)  |  Interface pour la configuration des options d’étiquetage des méthodes SetLabel/DeleteLabel.
[MIP :: LabelNotFoundError, classe](class_mip_labelnotfounderror.md)  |  L’ID d’étiquette n’est pas reconnu.
[MIP :: LoggerDelegate, classe](class_mip_loggerdelegate.md)  |  Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
[MIP :: MetadataAction, classe](class_mip_metadataaction.md)  |  Action qui ajoute des informations de métadonnées au contenu.
[MIP :: MipContext, classe](class_mip_mipcontext.md)  |  MipContext représente l’état partagé par tous les profils, moteurs et gestionnaires.
[MIP :: MsgAttachmentData, classe](class_mip_msgattachmentdata.md)  | Pas encore documenté.
[MIP :: MsgInspector, classe](class_mip_msginspector.md)  | Pas encore documenté.
[MIP :: NetworkError, classe](class_mip_networkerror.md)  |  Erreur de mise en réseau. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service.
[MIP :: NoAuthTokenError, classe](class_mip_noauthtokenerror.md)  |  L’utilisateur n’a pas pu accéder au contenu en raison d’un jeton d’authentification manquant.
[MIP :: NoPermissionsError, classe](class_mip_nopermissionserror.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
[MIP :: NoPolicyError, classe](class_mip_nopolicyerror.md)  |  La stratégie de locataire n’est pas configurée pour la classification/les étiquettes.
[MIP :: NotSupportedError, classe](class_mip_notsupportederror.md)  |  L’opération demandée par l’application n’est pas prise en charge par le kit SDK.
[MIP :: OperationCancelledError, classe](class_mip_operationcancellederror.md)  |  L'opération a été annulée.
[MIP de classe ::P olicyEngine](class_mip_policyengine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[MIP ::P olicyEngine :: Settings, classe](class_mip_policyengine_settings.md)  |  Définit les paramètres associés à un PolicyEngine.
[MIP de classe ::P olicyHandler](class_mip_policyhandler.md)  |  Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
[MIP de classe ::P olicyPackageData](class_mip_policypackagedata.md)  | Pas encore documenté.
[MIP de classe ::P olicyProfile](class_mip_policyprofile.md)  |  La classe PolicyProfile est la classe racine pour l’utilisation des opérations Microsoft Information Protection. Une application classique n’A besoin que d’un seul PolicyProfile, mais elle peut créer plusieurs profils si nécessaire.
[MIP ::P olicyProfile :: observer, classe](class_mip_policyprofile_observer.md)  |  Interface observer permettant aux clients d’obtenir des notifications pour les événements liés au profil.
[MIP ::P olicyProfile :: Settings, classe](class_mip_policyprofile_settings.md)  |  Paramètres utilisés par PolicyProfile lors de sa création et tout au long de sa durée de vie.
[MIP de classe ::P olicyRuleData](class_mip_policyruledata.md)  | Pas encore documenté.
[MIP de classe ::P olicySyncError](class_mip_policysyncerror.md)  |  Une tentative de synchronisation des données de stratégie a échoué.
[MIP de classe ::P rivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
[MIP de classe ::P ropertyData](class_mip_propertydata.md)  | Pas encore documenté.
[MIP de classe ::P rotectAdhocAction](class_mip_protectadhocaction.md)  |  Classe d’action qui spécifie l’ajout de la protection ad hoc au document.
[MIP de classe ::P rotectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Classe d’action qui spécifie l’ajout de la protection par modèle au document.
[MIP de classe ::P rotectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
[MIP de classe ::P rotectionActionData](class_mip_protectionactiondata.md)  | Pas encore documenté.
[MIP de classe ::P rotectionDescriptor](class_mip_protectiondescriptor.md)  |  Description de la protection associée à un élément de contenu.
[MIP de classe ::P rotectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Construit un ProtectionDescriptor qui décrit la protection associée à un élément de contenu.
[MIP de classe ::P rotectionEngine](class_mip_protectionengine.md)  |  Gère les actions liées à la protection sur une identité spécifique.
[MIP ::P rotectionEngine :: observer, classe](class_mip_protectionengine_observer.md)  |  Interface qui reçoit les notifications liées à ProtectionEngine.
[MIP ::P rotectionEngine :: Settings, classe](class_mip_protectionengine_settings.md)  |  Paramètres utilisés par ProtectionEngine lors de sa création et tout au long de sa durée de vie.
[MIP de classe ::P rotectionHandler](class_mip_protectionhandler.md)  |  Gère les actions liées à la protection pour une configuration de protection spécifique.
[MIP ::P rotectionHandler :: ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  Paramètres utilisés pour créer un ProtectionHandler pour utiliser le contenu existant.
[MIP ::P rotectionHandler :: observer, classe](class_mip_protectionhandler_observer.md)  |  Interface qui reçoit les notifications liées à ProtectionHandler.
[MIP ::P rotectionHandler ::P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  Paramètres utilisés pour créer un ProtectionHandler pour protéger un nouveau contenu.
[MIP de classe ::P rotectionProfile](class_mip_protectionprofile.md)  |  ProtectionProfile est la classe racine pour effectuer des opérations de protection.
[MIP ::P rotectionProfile :: observer, classe](class_mip_protectionprofile_observer.md)  |  Interface qui reçoit les notifications liées à ProtectionProfile.
[MIP ::P rotectionProfile :: Settings, classe](class_mip_protectionprofile_settings.md)  |  Paramètres utilisés par ProtectionProfile lors de sa création et tout au long de sa durée de vie.
[MIP de classe ::P rotectionSettings](class_mip_protectionsettings.md)  |  Interface pour la configuration des options de protection pour la méthode SetLabel.
[MIP de classe ::P roxyAuthenticationError](class_mip_proxyauthenticationerror.md)  |  Échec de l’authentification du proxy.
[MIP de classe ::P ublishingLicenseInfo](class_mip_publishinglicenseinfo.md)  |  Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
[MIP :: RecommendLabelAction, classe](class_mip_recommendlabelaction.md)  |  Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
[MIP :: RemoveContentFooterAction, classe](class_mip_removecontentfooteraction.md)  |  Classe d’action qui spécifie la suppression du pied de page de contenu du document.
[MIP :: RemoveContentHeaderAction, classe](class_mip_removecontentheaderaction.md)  |  Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
[MIP :: RemoveProtectionAction, classe](class_mip_removeprotectionaction.md)  |  Classe d’action qui spécifie la suppression de la protection appliquée au document.
[MIP :: RemoveWatermarkAction, classe](class_mip_removewatermarkaction.md)  |  Classe d’action qui spécifie la suppression du filigrane du document.
[MIP :: RulePackageData, classe](class_mip_rulepackagedata.md)  | Pas encore documenté.
[MIP :: SensitivityConditionData, classe](class_mip_sensitivityconditiondata.md)  | Pas encore documenté.
[MIP :: SensitivityTypesRulePackage, classe](class_mip_sensitivitytypesrulepackage.md)  | Pas encore documenté.
[MIP :: ServiceDisabledError, classe](class_mip_servicedisablederror.md)  |  L’utilisateur n’a pas pu accéder au contenu en raison de la désactivation d’un service.
[MIP :: Stream, classe](class_mip_stream.md)  |  Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
[MIP :: SyncFileBaseData, classe](class_mip_syncfilebasedata.md)  | Pas encore documenté.
[MIP :: SyncFilePolicyData, classe](class_mip_syncfilepolicydata.md)  | Pas encore documenté.
[MIP :: SyncFileSensitivityData, classe](class_mip_syncfilesensitivitydata.md)  | Pas encore documenté.
[MIP :: TaskDispatcherDelegate, classe](class_mip_taskdispatcherdelegate.md)  |  Classe qui définit l’interface du répartiteur de tâches du kit de développement logiciel (SDK) MIP.
[MIP :: TemplateNotFoundError, classe](class_mip_templatenotfounderror.md)  |  L’ID de modèle n’est pas reconnu par le service RMS.
[MIP :: TransientNetworkError, classe](class_mip_transientnetworkerror.md)  |  Erreur de mise en réseau temporaire. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service. L’opération peut être retentée, car cette erreur est une erreur temporaire.
[MIP :: UserRights, classe](class_mip_userrights.md)  |  Groupe d’utilisateurs et droits qui leur sont associés.
[MIP :: UserRoles, classe](class_mip_userroles.md)  |  Groupe d’utilisateurs et rôles qui leur sont associés.