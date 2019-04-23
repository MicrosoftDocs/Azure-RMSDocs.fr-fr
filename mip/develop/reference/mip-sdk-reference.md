---
title: SDK MIP pour C++ référence
description: SDK MIP pour C++ référence
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1db2faeca6c2ff00a0053a7d65d16872190d306f
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60172791"
---
# <a name="mip-sdk-for-c-reference"></a>SDK MIP pour C++ référence

Microsoft Information Protection (MIP) SDK pour C++ permet aux développeurs de gérer et appliquer des stratégies de protection des données aux données et autres ressources numériques.

Le SDK MIP pour C++ inclut :

- [Énumérations et structures](mip-enums-and-structs.md)
- [Fonctions](mip-functions.md)
- Les classes suivantes :

 Classe                         | Description                                
--------------------------------|---------------------------------------------
class mip::AccessDeniedError  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
mip::Action, classe  |  Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
mip::AddContentFooterAction, classe  |  Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
mip::AddContentHeaderAction, classe  |  Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
mip::AddWatermarkAction, classe  |  Classe d’action qui spécifie l’ajout d’un filigrane.
classe mip::AdhocProtectionRequiredError  |  La protection ad hoc doit être définie pour effectuer l’action sur le fichier.
class mip::ApplyLabelAction  |  Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
classe mip::AuthDelegate  |  Délégué pour l’authentification des opérations associées.
classe mip::AuthDelegate::OAuth2Challenge  |  une classe qui contient toutes les informations requises à partir de l’application appelante afin de générer un jeton oauth2.
classe mip::AuthDelegate::OAuth2Token  |  Classe définissant comment le SDK MIP attend le jeton oauth2 à passer dans le Kit de développement.
mip::BadInputError, classe  |  Erreur d’entrée incorrecte, levée quand l’entrée dans une API SDK n’est pas valide.
classe mip::ClassificationRequest  |  Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
class mip::ClassificationResult  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
classe mip::ConsentDelegate  |  Délégué pour les opérations relatives au consentement.
mip::ConsentDeniedError, classe  |  Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
mip::ContentLabel, classe  |  Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
mip::CustomAction, classe  |  [CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
mip::Error, classe  |  Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
mip::ExecutionState, classe  |  Interface pour tous les états nécessaires à l’exécution du moteur.
mip::FileEngine, classe  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
mip::FileEngine::Settings, classe  | _Pas encore documenté._
classe mip::FileExecutionState  | _Pas encore documenté._
mip::FileHandler, classe  |  Interface pour toutes les fonctions de gestion de fichiers.
mip::FileHandler::Observer, classe  |  Interface [Observer](class_mip_filehandler_observer.md) permettant aux clients d’obtenir les notifications des événements liés au gestionnaire de fichiers.
mip::FileIOError, classe  |  Erreur d’E/S de fichier.
mip::FileProfile, classe  |  La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
mip::FileProfile::Observer, classe  |  Interface [Observer](class_mip_fileprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
mip::FileProfile::Settings, classe  |  [Settings](class_mip_fileprofile_settings.md) utilisé par [FileProfile](class_mip_fileprofile.md) lors de sa création et tout au long de sa durée de vie.
mip::HttpDelegate, classe  |  Interface pour le remplacement de la gestion HTTP.
classe mip::HttpOperation  |  Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors de la substitution [HttpDelegate](class_mip_httpdelegate.md).
mip::HttpRequest, classe  |  Interface qui décrit une seule requête HTTP.
mip::HttpResponse, classe  |  Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
classe mip::Identity  |  Abstraction d’identité.
mip::InternalError, classe  |  Erreur interne. Cette erreur est levée quand un événement inattendu se produit pendant l’exécution.
mip::JustificationRequiredError, classe  | _Pas encore documenté._
class mip::JustifyAction  |  Justify [Action](class_mip_action.md) nécessite de fournir une justification de rétrogradation d’une étiquette et de définir la réponse dans l’état d’exécution.
mip::Label, classe  |  Abstraction d’une étiquette unique Microsoft Information Protection.
mip::LabelingOptions, classe  |  Interface pour la configuration des options d’étiquetage des méthodes SetLabel/DeleteLabel.
class mip::LoggerDelegate  |  Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
mip::MetadataAction, classe  |  Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
mip::NetworkError, classe  |  Erreur de mise en réseau. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service.
classe mip::NoAuthTokenError  |  L’utilisateur n’a pas pu obtenir l’accès au contenu en raison du manque de jeton d’authentification.
classe mip::NoPermissionsError  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
classe mip::NoPolicyError  |  Stratégie de client n’est pas configurée pour les étiquettes de classification /.
mip::NotSupportedError, classe  |  L’opération demandée par l’application n’est pas prise en charge par le kit SDK.
classe mip::OperationCancelledError  |  Opération a été annulée.
mip::PolicyEngine, classe  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
class mip::PolicyEngine::Settings  |  Définit les paramètres associés à un [PolicyEngine](class_mip_policyengine.md).
mip::PolicyHandler, classe  |  Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
mip::PolicyProfile, classe  |  La classe [PolicyProfile](class_mip_policyprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [PolicyProfile](class_mip_policyprofile.md), mais elle peut créer plusieurs profils si nécessaire.
mip::PolicyProfile::Observer, classe  |  Interface [Observer](class_mip_policyprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
mip::PolicyProfile::Settings, classe  |  [Paramètres](class_mip_policyprofile_settings.md) utilisés par [PolicyProfile](class_mip_policyprofile.md) lors de sa création et tout au long de sa durée de vie.
mip::PolicySyncError, classe  |  Une tentative de synchronisation des données de stratégie a échoué.
mip::PrivilegedRequiredError, classe  |  L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
mip::ProtectAdhocAction, classe  |  Classe d’action qui spécifie l’ajout de la protection ad hoc au document.
class mip::ProtectByTemplateAction  |  Classe d’action qui spécifie l’ajout de la protection par modèle au document.
mip::ProtectDoNotForwardAction, classe  |  Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
class mip::ProtectionDescriptor  |  Description de la protection associée à un élément de contenu.
class mip::ProtectionDescriptorBuilder  |  Construit un [ProtectionDescriptor](class_mip_protectiondescriptor.md) qui décrit la protection associée à un élément de contenu.
class mip::ProtectionEngine  |  Gère les actions liées à la protection sur une identité spécifique.
class mip::ProtectionEngine::Observer  |  Interface qui reçoit les notifications relatives à [ProtectionEngine](class_mip_protectionengine.md).
class mip::ProtectionEngine::Settings  |  [Settings](class_mip_protectionengine_settings.md) utilisé par [ProtectionEngine](class_mip_protectionengine.md) lors de sa création et tout au long de sa durée de vie.
class mip::ProtectionHandler  |  Gère les actions liées à la protection pour une configuration de protection spécifique.
class mip::ProtectionHandler::Observer  |  Interface qui reçoit les notifications relatives à [ProtectionHandler](class_mip_protectionhandler.md).
mip::ProtectionProfile, classe  |  [ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
mip::ProtectionProfile::Observer, classe  |  Interface qui reçoit les notifications relatives à [ProtectionProfile](class_mip_protectionprofile.md).
mip::ProtectionProfile::Settings, classe  |  [Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de sa création et tout au long de sa durée de vie.
classe mip::ProxyAuthenticationError  |  Échec de l’authentification de proxy.
class mip::RecommendLabelAction  |  Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
mip::RemoveContentFooterAction, classe  |  Classe d’action qui spécifie la suppression du pied de page de contenu du document.
mip::RemoveContentHeaderAction, classe  |  Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
mip::RemoveProtectionAction, classe  |  Classe d’action qui spécifie la suppression de la protection appliquée au document.
mip::RemoveWatermarkAction, classe  |  Classe d’action qui spécifie la suppression du filigrane du document.
classe mip::SensitivityTypesRulePackage  | _Pas encore documenté._
classe mip::ServiceDisabledError  |  L’utilisateur n’a pas pu obtenir l’accès au contenu en raison d’un service en cours de désactivation.
mip::Stream, classe  |  Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
classe mip::TaskDispatcherDelegate  |  Une classe qui définit l’interface pour le répartiteur de tâche du SDK MIP.
mip::TransientNetworkError, classe  |  Erreur de mise en réseau temporaire. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service. L’opération peut être retentée, car cette erreur est une erreur temporaire.
mip::UserRights, classe  |  Groupe d’utilisateurs et droits qui leur sont associés.
mip::UserRoles, classe  |  Groupe d’utilisateurs et rôles qui leur sont associés.