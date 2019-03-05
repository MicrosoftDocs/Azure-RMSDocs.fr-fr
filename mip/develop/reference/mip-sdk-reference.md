---
title: SDK MIP pour C++ référence
description: SDK MIP pour C++ référence
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 80b0ae49220cfb745e0fa0a0a0ce004d132c4d3f
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333770"
---
# <a name="mip-sdk-for-c-reference"></a>SDK MIP pour C++ référence

Microsoft Information Protection (MIP) SDK pour C++ permet aux développeurs de gérer et appliquer des stratégies de protection des données aux données et autres ressources numériques.  

Le SDK MIP pour C++ inclut :

- [Énumérations et structures](mip-enums-and-structs.md)
- [Fonctions](mip-functions.md)
- Les classes suivantes :

| Nom de namespace::Class | Description |
| :----------|:------------|
[mip::AccessDeniedError](class_mip_AccessDeniedError.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
[mip::Action](class_mip_Action.md)  |  Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
[mip::AddContentFooterAction](class_mip_AddContentFooterAction.md)  |  Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
[mip::AddContentHeaderAction](class_mip_AddContentHeaderAction.md)  |  Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
[mip::AddWatermarkAction](class_mip_AddWatermarkAction.md)  |  Classe d’action qui spécifie l’ajout d’un filigrane.
[mip::ApplyLabelAction](class_mip_ApplyLabelAction.md)  |  Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
[mip::AuthDelegate](class_mip_AuthDelegate.md)  |  Délégué pour l’authentification des opérations associées.
[mip::BadInputError](class_mip_BadInputError.md)  |  Erreur d’entrée incorrecte, levée quand l’entrée dans une API SDK n’est pas valide.
[mip::ClassificationRequest](class_mip_ClassificationRequest.md)  |  Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
[mip::ClassificationResult](class_mip_ClassificationResult.md)  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
[mip::ConsentDelegate](class_mip_ConsentDelegate.md)  |  Délégué pour les opérations relatives au consentement.
[mip::ConsentDeniedError](class_mip_ConsentDeniedError.md)  |  Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
[mip::ContentLabel](class_mip_ContentLabel.md)  |  Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
[mip::CustomAction](class_mip_CustomAction.md)  |  [CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
[mip::Error](class_mip_Error.md)  |  Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
[mip::ExecutionState](class_mip_ExecutionState.md)  |  Interface pour tous les états nécessaires à l’exécution du moteur.
[mip::FileEngine](class_mip_FileEngine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[mip::FileExecutionState](class_mip_FileExecutionState.md)  | _Pas encore documenté._
[mip::FileHandler](class_mip_FileHandler.md)  |  Interface pour toutes les fonctions de gestion de fichiers.
[mip::FileIOError](class_mip_FileIOError.md)  |  Erreur d’E/S de fichier.
[mip::FileProfile](class_mip_FileProfile.md)  |  La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
[mip::HttpDelegate](class_mip_HttpDelegate.md)  |  Interface pour le remplacement de la gestion HTTP.
[mip::HttpRequest](class_mip_HttpRequest.md)  |  Interface qui décrit une seule requête HTTP.
[mip::HttpResponse](class_mip_HttpResponse.md)  |  Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
[mip::Identity](class_mip_Identity.md)  |  Abstraction d’identité.
[mip::InternalError](class_mip_InternalError.md)  |  Erreur interne. Cette erreur est levée quand un événement inattendu se produit pendant l’exécution.
[mip::JustificationRequiredError](class_mip_JustificationRequiredError.md)  | _Pas encore documenté._
[mip::JustifyAction](class_mip_JustifyAction.md)  |  Justify [Action](class_mip_action.md) nécessite de fournir une justification de rétrogradation d’une étiquette et de définir la réponse dans l’état d’exécution.
[mip::Label](class_mip_Label.md)  |  Abstraction d’une étiquette unique Microsoft Information Protection.
[mip::LabelingOptions](class_mip_LabelingOptions.md)  |  Interface pour la configuration des options d’étiquetage des méthodes SetLabel/DeleteLabel.
[mip::LoggerDelegate](class_mip_LoggerDelegate.md)  |  Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
[mip::MetadataAction](class_mip_MetadataAction.md)  |  Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
[mip::NetworkError](class_mip_NetworkError.md)  |  Erreur de mise en réseau. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service.
[mip::NoAuthTokenError](class_mip_NoAuthTokenError.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu en raison du manque de jeton d’authentification.
[mip::NoPermissionsError](class_mip_NoPermissionsError.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
[mip::NoPolicyError](class_mip_NoPolicyError.md)  |  Stratégie de client n’est pas configurée pour les étiquettes de classification /.
[mip::NotSupportedError](class_mip_NotSupportedError.md)  |  L’opération demandée par l’application n’est pas prise en charge par le kit SDK.
[mip::PolicyEngine](class_mip_PolicyEngine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[mip::PolicyHandler](class_mip_PolicyHandler.md)  |  Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
[mip::PolicyProfile](class_mip_PolicyProfile.md)  |  La classe [PolicyProfile](class_mip_policyprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [PolicyProfile](class_mip_policyprofile.md), mais elle peut créer plusieurs profils si nécessaire.
[mip::PolicySyncError](class_mip_PolicySyncError.md)  |  Une tentative de synchronisation des données de stratégie a échoué.
[mip::PrivilegedRequiredError](class_mip_PrivilegedRequiredError.md)  |  L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
[mip::ProtectAdhocAction](class_mip_ProtectAdhocAction.md)  |  Classe d’action qui spécifie l’ajout de la protection ad hoc au document.
[mip::ProtectByTemplateAction](class_mip_ProtectByTemplateAction.md)  |  Classe d’action qui spécifie l’ajout de la protection par modèle au document.
[mip::ProtectDoNotForwardAction](class_mip_ProtectDoNotForwardAction.md)  |  Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
[mip::ProtectionDescriptor](class_mip_ProtectionDescriptor.md)  |  Description de la protection associée à un élément de contenu.
[mip::ProtectionDescriptorBuilder](class_mip_ProtectionDescriptorBuilder.md)  |  Construit un [ProtectionDescriptor](class_mip_protectiondescriptor.md) qui décrit la protection associée à un élément de contenu.
[mip::ProtectionEngine](class_mip_ProtectionEngine.md)  |  Gère les actions liées à la protection sur une identité spécifique.
[mip::ProtectionHandler](class_mip_ProtectionHandler.md)  |  Gère les actions liées à la protection pour une configuration de protection spécifique.
[mip::ProtectionProfile](class_mip_ProtectionProfile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
[mip::ProxyAuthenticationError](class_mip_ProxyAuthenticationError.md)  |  Échec de l’authentification de proxy.
[mip::RecommendLabelAction](class_mip_RecommendLabelAction.md)  |  Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
[mip::RemoveContentFooterAction](class_mip_RemoveContentFooterAction.md)  |  Classe d’action qui spécifie la suppression du pied de page de contenu du document.
[mip::RemoveContentHeaderAction](class_mip_RemoveContentHeaderAction.md)  |  Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
[mip::RemoveProtectionAction](class_mip_RemoveProtectionAction.md)  |  Classe d’action qui spécifie la suppression de la protection appliquée au document.
[mip::RemoveWatermarkAction](class_mip_RemoveWatermarkAction.md)  |  Classe d’action qui spécifie la suppression du filigrane du document.
[mip::SensitivityTypesRulePackage](class_mip_SensitivityTypesRulePackage.md)  | _Pas encore documenté._
[mip::ServiceDisabledError](class_mip_ServiceDisabledError.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu en raison d’un service en cours de désactivation.
[mip::Stream](class_mip_Stream.md)  |  Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
[mip::TransientNetworkError](class_mip_TransientNetworkError.md)  |  Erreur de mise en réseau temporaire. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service. L’opération peut être retentée, car cette erreur est une erreur temporaire.
[mip::UserRights](class_mip_UserRights.md)  |  Groupe d’utilisateurs et droits qui leur sont associés.
[mip::UserRoles](class_mip_UserRoles.md)  |  Groupe d’utilisateurs et rôles qui leur sont associés.
