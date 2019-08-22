---
title: SDK MIP pour C++ référence
description: SDK MIP pour C++ référence
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2fab85dfd5b5d0d1103f9c3ee4b0d3725a10cb8f
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884830"
---
# <a name="mip-sdk-for-c-reference"></a>SDK MIP pour C++ référence

Le kit de développement logiciel (SDK) C++ Microsoft information protection pour permet aux développeurs de gérer et d’appliquer des stratégies de protection des données à des données et à d’autres ressources numériques.

Le SDK MIP pour C++ inclut :

- [Énumérations et structures](mip-enums-and-structs.md)
- [Fonctions](mip-functions.md)
- Les classes suivantes :

 Classe                         | Description                                
--------------------------------|---------------------------------------------
class mip::AccessDeniedError  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
mip::Action, classe  |  Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
MIP:: ActionData, classe  | _Pas encore documenté._
mip::AddContentFooterAction, classe  |  Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
mip::AddContentHeaderAction, classe  |  Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
mip::AddWatermarkAction, classe  |  Classe d’action qui spécifie l’ajout d’un filigrane.
MIP:: AddWatermarkActionData, classe  | _Pas encore documenté._
MIP:: AdhocProtectionRequiredError, classe  |  La protection ad hoc doit être configurée pour terminer l’action sur le fichier.
MIP:: ApplicationActionState, classe  | _Pas encore documenté._
class mip::ApplyLabelAction  |  Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
MIP:: ArgumentData, classe  | _Pas encore documenté._
MIP:: AuthDelegate, classe  |  Délégué pour les opérations liées à l’authentification.
mip::BadInputError, classe  |  Erreur d’entrée incorrecte, levée quand l’entrée dans une API SDK n’est pas valide.
MIP:: ClassificationData, classe  | _Pas encore documenté._
MIP:: ClassificationRequest, classe  |  Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
class mip::ClassificationResult  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
MIP:: ComputeEngine, classe  | _Pas encore documenté._
MIP:: ComputeEngineContext, classe  | _Pas encore documenté._
MIP:: ConditionData, classe  | _Pas encore documenté._
MIP:: ConsentDelegate, classe  |  Délégué pour les opérations relatives au consentement.
mip::ConsentDeniedError, classe  |  Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
mip::ContentLabel, classe  |  Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
MIP:: ContentMarkingActionData, classe  | _Pas encore documenté._
mip::CustomAction, classe  |  [CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
MIP de classe::D eprecatedApiError  |  L’appelant a appelé une API déconseillée.
MIP de classe::D ocumentState  | _Pas encore documenté._
mip::Error, classe  |  Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
mip::ExecutionState, classe  |  Interface pour tous les états nécessaires à l’exécution du moteur.
mip::FileEngine, classe  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
MIP:: FileExecutionState, classe  | _Pas encore documenté._
mip::FileHandler, classe  |  Interface pour toutes les fonctions de gestion de fichiers.
MIP:: FileInspector, classe  | _Pas encore documenté._
mip::FileIOError, classe  |  Erreur d’E/S de fichier.
mip::FileProfile, classe  |  La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
mip::HttpDelegate, classe  |  Interface pour le remplacement de la gestion HTTP.
MIP:: HttpOperation, classe  |  Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
mip::HttpRequest, classe  |  Interface qui décrit une seule requête HTTP.
mip::HttpResponse, classe  |  Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
MIP:: Identity, classe  |  Abstraction pour l’identité.
mip::InternalError, classe  |  Erreur interne. Cette erreur est levée quand un événement inattendu se produit pendant l’exécution.
mip::JustificationRequiredError, classe  | _Pas encore documenté._
class mip::JustifyAction  |  Justify [Action](class_mip_action.md) nécessite de fournir une justification de rétrogradation d’une étiquette et de définir la réponse dans l’état d’exécution.
mip::Label, classe  |  Abstraction d’une étiquette unique Microsoft Information Protection.
MIP:: LabelActionData, classe  | _Pas encore documenté._
MIP:: LabelDisabledError, classe  |  L' [étiquette](class_mip_label.md) est désactivée ou inactive.
MIP:: LabelGroupData, classe  | _Pas encore documenté._
mip::LabelingOptions, classe  |  Interface pour la configuration des options d’étiquetage des méthodes SetLabel/DeleteLabel.
MIP:: LabelNotFoundError, classe  |  [Étiquette](class_mip_label.md) L’ID n’est pas reconnu.
class mip::LoggerDelegate  |  Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
mip::MetadataAction, classe  |  Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
MIP:: MipContext, classe  | MipContext représente l’état partagé par tous les profils, moteurs et gestionnaires.
MIP:: MsgAttachmentData, classe  | _Pas encore documenté._
MIP:: MsgInspector, classe  | _Pas encore documenté._
mip::NetworkError, classe  |  Erreur de mise en réseau. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service.
MIP:: NoAuthTokenError, classe  |  L’utilisateur n’a pas pu accéder au contenu en raison d’un jeton d’authentification manquant.
MIP:: NoPermissionsError, classe  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
MIP:: NoPolicyError, classe  |  La stratégie de locataire n’est pas configurée pour la classification/les étiquettes.
mip::NotSupportedError, classe  |  L’opération demandée par l’application n’est pas prise en charge par le kit SDK.
MIP:: OperationCancelledError, classe  |  L’opération a été annulée.
mip::PolicyEngine, classe  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
mip::PolicyHandler, classe  |  Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
MIP de classe::P olicyPackageData  | _Pas encore documenté._
mip::PolicyProfile, classe  |  La classe [PolicyProfile](class_mip_policyprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [PolicyProfile](class_mip_policyprofile.md), mais elle peut créer plusieurs profils si nécessaire.
MIP de classe::P olicyRuleData  | _Pas encore documenté._
mip::PolicySyncError, classe  |  Une tentative de synchronisation des données de stratégie a échoué.
mip::PrivilegedRequiredError, classe  |  L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
MIP de classe::P ropertyData  | _Pas encore documenté._
mip::ProtectAdhocAction, classe  |  Classe d’action qui spécifie l’ajout de la protection ad hoc au document.
class mip::ProtectByTemplateAction  |  Classe d’action qui spécifie l’ajout de la protection par modèle au document.
mip::ProtectDoNotForwardAction, classe  |  Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
MIP de classe::P rotectionActionData  | _Pas encore documenté._
class mip::ProtectionDescriptor  |  Description de la protection associée à un élément de contenu.
class mip::ProtectionDescriptorBuilder  |  Construit un [ProtectionDescriptor](class_mip_protectiondescriptor.md) qui décrit la protection associée à un élément de contenu.
class mip::ProtectionEngine  |  Gère les actions liées à la protection sur une identité spécifique.
class mip::ProtectionHandler  |  Gère les actions liées à la protection pour une configuration de protection spécifique.
mip::ProtectionProfile, classe  |  [ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
MIP de classe::P rotectionSettings  |  Interface pour la configuration des options de protection pour la méthode SetLabel.
MIP de classe::P roxyAuthenticationError  |  Échec de l’authentification du proxy.
MIP de classe::P ublishingLicenseInfo  |  Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
class mip::RecommendLabelAction  |  Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
mip::RemoveContentFooterAction, classe  |  Classe d’action qui spécifie la suppression du pied de page de contenu du document.
mip::RemoveContentHeaderAction, classe  |  Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
mip::RemoveProtectionAction, classe  |  Classe d’action qui spécifie la suppression de la protection appliquée au document.
mip::RemoveWatermarkAction, classe  |  Classe d’action qui spécifie la suppression du filigrane du document.
MIP:: RulePackageData, classe  | _Pas encore documenté._
MIP:: SensitivityConditionData, classe  | _Pas encore documenté._
MIP:: SensitivityTypesRulePackage, classe  | _Pas encore documenté._
MIP:: ServiceDisabledError, classe  |  L’utilisateur n’a pas pu accéder au contenu en raison de la désactivation d’un service.
mip::Stream, classe  |  Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
MIP:: SyncFileBaseData, classe  | _Pas encore documenté._
MIP:: SyncFilePolicyData, classe  | _Pas encore documenté._
MIP:: SyncFileSensitivityData, classe  | _Pas encore documenté._
MIP:: TaskDispatcherDelegate, classe  |  Classe qui définit l’interface du répartiteur de tâches du kit de développement logiciel (SDK) MIP.
MIP:: TemplateNotFoundError, classe  |  L’ID de modèle n’est pas reconnu par le service RMS.
mip::TransientNetworkError, classe  |  Erreur de mise en réseau temporaire. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service. L’opération peut être retentée, car cette erreur est une erreur temporaire.
mip::UserRights, classe  |  Groupe d’utilisateurs et droits qui leur sont associés.
mip::UserRoles, classe  |  Groupe d’utilisateurs et rôles qui leur sont associés.
