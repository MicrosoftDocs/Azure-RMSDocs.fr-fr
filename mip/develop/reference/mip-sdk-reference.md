---
title: Référence du kit de développement logiciel MIP pour C++
description: Référence du kit de développement logiciel MIP pour C++
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: da5ee17fbb177fe9b6e37461a5d35425a3945e59
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565665"
---
# <a name="mip-sdk-for-c-reference"></a>Référence du kit de développement logiciel MIP pour C++

Le kit de développement logiciel (SDK) Microsoft Information Protection (MIP) pour C++ permet aux développeurs de gérer et d’appliquer des stratégies de protection des données à des données et à d’autres ressources numériques.

Le SDK MIP pour C++ inclut :

- [Énumérations et structures](mip-enums-and-structs.md)
- [Fonctions](mip-functions.md)
- Les classes suivantes :

## <a name="namespace-mip-classes"></a>classes d’espace de noms MIP

 Classe                         | Description                                
--------------------------------|---------------------------------------------
[AccessDeniedError de classe](class_mip_accessdeniederror.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
[Action de classe](class_mip_action.md)  |  Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
[ActionData de classe](class_mip_actiondata.md)  | Pas encore documenté.
[AddContentFooterAction de classe](class_mip_addcontentfooteraction.md)  |  Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
[AddContentHeaderAction de classe](class_mip_addcontentheaderaction.md)  |  Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
[AddWatermarkAction de classe](class_mip_addwatermarkaction.md)  |  Classe d’action qui spécifie l’ajout d’un filigrane.
[AddWatermarkActionData de classe](class_mip_addwatermarkactiondata.md)  | Pas encore documenté.
[AdhocProtectionRequiredError de classe](class_mip_adhocprotectionrequirederror.md)  |  La protection ad hoc doit être configurée pour terminer l’action sur le fichier.
[ApplicationActionState de classe](class_mip_applicationactionstate.md)  | Pas encore documenté.
[ApplyLabelAction de classe](class_mip_applylabelaction.md)  |  Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
[ArgumentData de classe](class_mip_argumentdata.md)  | Pas encore documenté.
[AsyncControl de classe](class_mip_asynccontrol.md)  |  Classe utilisée pour annuler l’opération asynchrone.
[AuthDelegate de classe](class_mip_authdelegate.md)  |  Délégué pour les opérations liées à l’authentification.
[BadInputError de classe](class_mip_badinputerror.md)  |  Erreur d’entrée incorrecte, levée quand l’entrée dans une API SDK n’est pas valide.
[ClassificationData de classe](class_mip_classificationdata.md)  | Pas encore documenté.
[ClassificationRequest de classe](class_mip_classificationrequest.md)  |  Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
[ClassificationResult de classe](class_mip_classificationresult.md)  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
[ComputeEngine de classe](class_mip_computeengine.md)  | Pas encore documenté.
[ComputeEngineContext de classe](class_mip_computeenginecontext.md)  | Pas encore documenté.
[ConditionData de classe](class_mip_conditiondata.md)  | Pas encore documenté.
[classe ConsentDelegate](class_mip_consentdelegate.md)  |  Délégué pour les opérations relatives au consentement.
[ConsentDeniedError de classe](class_mip_consentdeniederror.md)  |  Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
[classe ProtectionHandler :: ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  Paramètres utilisés pour créer un ProtectionHandler pour utiliser le contenu existant.
[ContentLabel de classe](class_mip_contentlabel.md)  |  Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
[ContentMarkingActionData de classe](class_mip_contentmarkingactiondata.md)  | Pas encore documenté.
[CustomAction de classe](class_mip_customaction.md)  |  CustomAction est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un conteneur de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
[DeprecatedApiError de classe](class_mip_deprecatedapierror.md)  |  L’appelant a appelé une API déconseillée.
[DetailedClassificationResult de classe](class_mip_detailedclassificationresult.md)  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
[DocumentState de classe](class_mip_documentstate.md)  | Pas encore documenté.
[Erreur de classe](class_mip_error.md)  |  Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
[ExecutionState de classe](class_mip_executionstate.md)  |  Interface pour tous les états nécessaires à l’exécution du moteur.
[FileEngine de classe](class_mip_fileengine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[FileExecutionState de classe](class_mip_fileexecutionstate.md)  | Pas encore documenté.
[FileHandler de classe](class_mip_filehandler.md)  |  Interface pour toutes les fonctions de gestion de fichiers.
[FileInspector de classe](class_mip_fileinspector.md)  | Pas encore documenté.
[FileIOError de classe](class_mip_fileioerror.md)  |  Erreur d’E/S de fichier.
[FileProfile de classe](class_mip_fileprofile.md)  |  La classe FileProfile est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
[HttpDelegate de classe](class_mip_httpdelegate.md)  |  Interface pour le remplacement de la gestion HTTP.
[HttpOperation de classe](class_mip_httpoperation.md)  |  Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors du remplacement de HttpDelegate.
[HttpRequest de classe](class_mip_httprequest.md)  |  Interface qui décrit une seule requête HTTP.
[HttpResponse de classe](class_mip_httpresponse.md)  |  Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de HttpDelegate.
[Identité de la classe](class_mip_identity.md)  |  Abstraction pour l’identité.
[InsufficientBufferError de classe](class_mip_insufficientbuffererror.md)  |  Erreur de mémoire tampon insuffisante.
[InternalError de classe](class_mip_internalerror.md)  |  Erreur interne. Cette erreur est levée quand un événement inattendu se produit pendant l’exécution.
[JustificationRequiredError de classe](class_mip_justificationrequirederror.md)  | Pas encore documenté.
[JustifyAction de classe](class_mip_justifyaction.md)  |  Justify Action nécessite de fournir une justification de rétrogradation d’une étiquette et de définir la réponse dans l’état d’exécution.
[Étiquette de la classe](class_mip_label.md)  |  Abstraction d’une étiquette unique Microsoft Information Protection.
[LabelActionData de classe](class_mip_labelactiondata.md)  | Pas encore documenté.
[LabelDisabledError de classe](class_mip_labeldisablederror.md)  |  L’étiquette est désactivée ou inactive.
[LabelGroupData de classe](class_mip_labelgroupdata.md)  | Pas encore documenté.
[LabelingOptions de classe](class_mip_labelingoptions.md)  |  Interface pour la configuration des options d’étiquetage des méthodes SetLabel/DeleteLabel.
[LabelNotFoundError de classe](class_mip_labelnotfounderror.md)  |  L’ID d’étiquette n’est pas reconnu.
[LicenseNotRegisteredError de classe](class_mip_licensenotregisterederror.md)  |  La licence n’est pas inscrite.
[LoggerDelegate de classe](class_mip_loggerdelegate.md)  |  Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
[MetadataAction de classe](class_mip_metadataaction.md)  |  Une Action qui ajoute des informations de métadonnées au contenu.
[MetadataEntry de classe](class_mip_metadataentry.md)  |  Classe d’abstraction pour l’entrée de métadonnées.
[MetadataVersion de classe](class_mip_metadataversion.md)  |  Interface pour un MetadataVersion. MetadataVersion détermine les métadonnées actives et leur mode de traitement.
[MipContext de classe](class_mip_mipcontext.md)  |  MipContext représente l’état partagé par tous les profils, moteurs et gestionnaires.
[MsgAttachmentData de classe](class_mip_msgattachmentdata.md)  | Pas encore documenté.
[MsgInspector de classe](class_mip_msginspector.md)  | Pas encore documenté.
[NetworkError de classe](class_mip_networkerror.md)  |  Erreur de mise en réseau. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service.
[NoAuthTokenError de classe](class_mip_noauthtokenerror.md)  |  L’utilisateur n’a pas pu accéder au contenu en raison d’un jeton d’authentification manquant.
[NoPermissionsError de classe](class_mip_nopermissionserror.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
[NoPolicyError de classe](class_mip_nopolicyerror.md)  |  La stratégie de locataire n’est pas configurée pour la classification/les étiquettes.
[NotSupportedError de classe](class_mip_notsupportederror.md)  |  L’opération demandée par l’application n’est pas prise en charge par le kit SDK.
[classe AuthDelegate :: OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)  |  classe qui contient toutes les informations requises de l’application appelante afin de générer un jeton oauth2.
[classe AuthDelegate :: OAuth2Token](class_mip_authdelegate_oauth2token.md)  |  Classe contenant les informations de jeton d’accès fournies par une application.
[classe FileHandler :: observer](class_mip_filehandler_observer.md)  |  Interface Observer permettant aux clients d’obtenir les notifications des événements liés au gestionnaire de fichiers.
[classe ProtectionEngine :: observer](class_mip_protectionengine_observer.md)  |  Interface qui reçoit les notifications relatives à ProtectionEngine.
[classe FileProfile :: observer](class_mip_fileprofile_observer.md)  |  Interface Observer permettant aux clients d’obtenir les notifications des événements liés aux profils.
[classe PolicyProfile :: observer](class_mip_policyprofile_observer.md)  |  Interface Observer permettant aux clients d’obtenir les notifications des événements liés aux profils.
[classe ProtectionHandler :: observer](class_mip_protectionhandler_observer.md)  |  Interface qui reçoit les notifications relatives à ProtectionHandler.
[classe ProtectionProfile :: observer](class_mip_protectionprofile_observer.md)  |  Interface qui reçoit les notifications relatives à ProtectionProfile.
[OperationCancelledError de classe](class_mip_operationcancellederror.md)  |  L'opération a été annulée.
[PolicyEngine de classe](class_mip_policyengine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[PolicyHandler de classe](class_mip_policyhandler.md)  |  Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
[PolicyPackageData de classe](class_mip_policypackagedata.md)  | Pas encore documenté.
[PolicyProfile de classe](class_mip_policyprofile.md)  |  La classe PolicyProfile est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe PolicyProfile, mais elle peut créer plusieurs profils si nécessaire.
[PolicyRuleData de classe](class_mip_policyruledata.md)  | Pas encore documenté.
[PrivilegedRequiredError de classe](class_mip_privilegedrequirederror.md)  |  L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
[PropertyData de classe](class_mip_propertydata.md)  | Pas encore documenté.
[ProtectAdhocAction de classe](class_mip_protectadhocaction.md)  |  Classe d’action qui spécifie l’ajout de la protection ad hoc au document.
[ProtectAdhocDkAction de classe](class_mip_protectadhocdkaction.md)  |  Classe d’action qui spécifie l’ajout de la protection de clé double ad hoc au document.
[ProtectByEncryptOnlyAction de classe](class_mip_protectbyencryptonlyaction.md)  |  Classe d’action qui spécifie l’ajout de la protection de chiffrement uniquement au document.
[ProtectByTemplateAction de classe](class_mip_protectbytemplateaction.md)  |  Classe d’action qui spécifie l’ajout de la protection par modèle au document.
[ProtectDoNotForwardAction de classe](class_mip_protectdonotforwardaction.md)  |  Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
[ProtectDoNotForwardDkAction de classe](class_mip_protectdonotforwarddkaction.md)  |  Une classe d’action qui spécifie l’ajout de la protection de la double clé ne pas transférer au document.
[ProtectionActionData de classe](class_mip_protectionactiondata.md)  | Pas encore documenté.
[ProtectionDescriptor de classe](class_mip_protectiondescriptor.md)  |  Description de la protection associée à un élément de contenu.
[ProtectionDescriptorBuilder de classe](class_mip_protectiondescriptorbuilder.md)  |  Construit un ProtectionDescriptor qui décrit la protection associée à un élément de contenu.
[ProtectionEngine de classe](class_mip_protectionengine.md)  |  Gère les actions liées à la protection sur une identité spécifique.
[ProtectionHandler de classe](class_mip_protectionhandler.md)  |  Gère les actions liées à la protection pour une configuration de protection spécifique.
[ProtectionProfile de classe](class_mip_protectionprofile.md)  |  ProtectionProfile est la classe racine utilisée pour effectuer des opérations de protection.
[ProtectionSettings de classe](class_mip_protectionsettings.md)  |  Interface pour la configuration des options de protection pour la méthode SetLabel.
[ProxyAuthenticationError de classe](class_mip_proxyauthenticationerror.md)  |  Échec de l’authentification du proxy.
[PublishingLicenseInfo de classe](class_mip_publishinglicenseinfo.md)  |  Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
[ProtectionHandler de classe ::P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  Paramètres utilisés pour créer un ProtectionHandler pour protéger un nouveau contenu.
[RecommendLabelAction de classe](class_mip_recommendlabelaction.md)  |  Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
[RemoveContentFooterAction de classe](class_mip_removecontentfooteraction.md)  |  Classe d’action qui spécifie la suppression du pied de page de contenu du document.
[RemoveContentHeaderAction de classe](class_mip_removecontentheaderaction.md)  |  Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
[RemoveProtectionAction de classe](class_mip_removeprotectionaction.md)  |  Classe d’action qui spécifie la suppression de la protection appliquée au document.
[RemoveWatermarkAction de classe](class_mip_removewatermarkaction.md)  |  Classe d’action qui spécifie la suppression du filigrane du document.
[RulePackageData de classe](class_mip_rulepackagedata.md)  | Pas encore documenté.
[SensitiveTypeClassificationData de classe](class_mip_sensitivetypeclassificationdata.md)  | Pas encore documenté.
[SensitivityConditionData de classe](class_mip_sensitivityconditiondata.md)  | Pas encore documenté.
[SensitivityTypesRulePackage de classe](class_mip_sensitivitytypesrulepackage.md)  | Pas encore documenté.
[ServiceDisabledError de classe](class_mip_servicedisablederror.md)  |  L’utilisateur n’a pas pu accéder au contenu en raison de la désactivation d’un service.
[classe FileEngine :: Settings](class_mip_fileengine_settings.md)  | Pas encore documenté.
[classe PolicyEngine :: Settings](class_mip_policyengine_settings.md)  |  Définit les paramètres associés à un PolicyEngine.
[classe PolicyProfile :: Settings](class_mip_policyprofile_settings.md)  |  Paramètres utilisés par PolicyProfile lors de sa création et tout au long de sa durée de vie.
[classe ProtectionProfile :: Settings](class_mip_protectionprofile_settings.md)  |  Settings utilisé par ProtectionProfile lors de sa création et tout au long de sa durée de vie.
[classe FileProfile :: Settings](class_mip_fileprofile_settings.md)  |  Settings utilisé par FileProfile lors de sa création et tout au long de sa durée de vie.
[classe ComputeEngine :: Settings](class_mip_computeengine_settings.md)  | Pas encore documenté.
[classe ProtectionEngine :: Settings](class_mip_protectionengine_settings.md)  |  Settings utilisé par ProtectionEngine lors de sa création et tout au long de sa durée de vie.
[Flux de classe](class_mip_stream.md)  |  Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
[SyncFileBaseData de classe](class_mip_syncfilebasedata.md)  | Pas encore documenté.
[SyncFilePolicyData de classe](class_mip_syncfilepolicydata.md)  | Pas encore documenté.
[SyncFileSensitivityData de classe](class_mip_syncfilesensitivitydata.md)  | Pas encore documenté.
[TaskDispatcherDelegate de classe](class_mip_taskdispatcherdelegate.md)  |  Classe qui définit l’interface du répartiteur de tâches du kit de développement logiciel (SDK) MIP.
[TemplateDescriptor de classe](class_mip_templatedescriptor.md)  | Pas encore documenté.
[TemplateNotFoundError de classe](class_mip_templatenotfounderror.md)  |  L’ID de modèle n’est pas reconnu par le service RMS.
[UserRights de classe](class_mip_userrights.md)  |  Groupe d’utilisateurs et droits qui leur sont associés.
[UserRoles de classe](class_mip_userroles.md)  |  Groupe d’utilisateurs et rôles qui leur sont associés.