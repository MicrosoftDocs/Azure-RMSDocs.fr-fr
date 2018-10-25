---
title: Référence du SDK MIP pour C++ (préversion)
description: Référence du SDK MIP pour C++ (préversion)
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06d8bb26a8e3026562006d68d4ae8d1630eba81c
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446326"
---
# <a name="mip-sdk-for-c-preview-reference"></a>Référence du SDK MIP pour C++ (préversion)

Le SDK MIP (Microsoft Information Protection) pour C++ (préversion) permet aux développeurs de gérer des stratégies de protection des données et de les appliquer à des données et d’autres ressources numériques.  

Pour plus d’informations, consultez le [blog des développeurs MIP](https://aka.ms/MIPDevelopers)<!-- and [MIP samples](https://aka.ms/mipsdksamples)-->.

Le SDK MIP pour C++ inclut :

- [Énumérations et structures](mip-enums-and-structs.md)
- [Fonctions](mip-functions.md)
- Les classes suivantes :

| Nom de la classe | Description |
| :----------|:------------|
[AccessDeniedError](class_mip_accessdeniederror.md)  |  L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
[Action](class_mip_action.md)  |  Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
[AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
[AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
[AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Classe d’action qui spécifie l’ajout d’un filigrane.
[ApplyLabelAction](class_mip_applylabelaction.md)  |  Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
[BadInputError](class_mip_badinputerror.md)  |  Erreur d’entrée incorrecte, levée quand l’entrée dans une API SDK n’est pas valide.
[ClassificationResult](class_mip_classificationresult.md)  |  Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
[ConsentDelegate](class_consentdelegate.md)  |  Délégué pour les opérations relatives au consentement.
[ConsentDeniedError](class_mip_consentdeniederror.md)  |  Une opération nécessitant le consentement de l’utilisateur ne l’a pas obtenu.
[ContentLabel](class_mip_contentlabel.md)  |  Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
[CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
[Erreur](class_mip_error.md)  |  Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
[ExecutionState](class_mip_executionstate.md)  |  Interface pour tous les états nécessaires à l’exécution du moteur.
[FileEngine::Settings](class_mip_fileengine_settings.md)  | _Pas encore documenté._
[FileEngine](class_mip_fileengine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[FileHandler::Observer](class_mip_filehandler_observer.md)  |  Interface [Observer](class_mip_filehandler_observer.md) permettant aux clients d’obtenir les notifications des événements liés au gestionnaire de fichiers.
[FileHandler](class_mip_filehandler.md)  |  Interface pour toutes les fonctions de gestion de fichiers.
[FileIOError](class_mip_fileioerror.md)  |  Erreur d’E/S de fichier.
[FileProfile::Observer](class_mip_fileprofile_observer.md)  |  Interface [Observer](class_mip_fileprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
[FileProfile::Settings](class_mip_fileprofile_settings.md)  |  [Settings](class_mip_fileprofile_settings.md) utilisé par [FileProfile](class_mip_fileprofile.md) lors de sa création et tout au long de sa durée de vie.
[FileProfile](class_mip_fileprofile.md)  |  La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
[HttpDelegate](class_mip_httpdelegate.md)  |  Interface pour le remplacement de la gestion HTTP.
[HttpRequest](class_mip_httprequest.md)  |  Interface qui décrit une seule requête HTTP.
[HttpResponse](class_mip_httpresponse.md)  |  Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
[InternalError](class_mip_internalerror.md)  |  Erreur interne. Cette erreur est levée quand un événement inattendu se produit pendant l’exécution.
[JustificationRequiredError](class_mip_justificationrequirederror.md)  | _Pas encore documenté._
[JustifyAction](class_mip_justifyaction.md)  |  Justify [Action](class_mip_action.md) nécessite de fournir une justification de rétrogradation d’une étiquette et de définir la réponse dans l’état d’exécution.
[Étiquette](class_mip_label.md)  |  Abstraction d’une étiquette unique Microsoft Information Protection.
[LabelingOptions](class_mip_labelingoptions.md)  |  Interface pour la configuration des options d’étiquetage des méthodes SetLabel/DeleteLabel.
[LoggerDelegate](class_mip_loggerdelegate.md)  |  Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
[MetadataAction](class_mip_metadataaction.md)  |  Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
[NetworkError](class_mip_networkerror.md)  |  Erreur de mise en réseau. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service.
[NotSupportedError](class_mip_notsupportederror.md)  |  L’opération demandée par l’application n’est pas prise en charge par le kit SDK.
[PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  Définit les paramètres associés à un [PolicyEngine](class_mip_policyengine.md).
[PolicyEngine](class_mip_policyengine.md)  |  Cette classe fournit une interface pour toutes les fonctions de moteur.
[PolicyHandler](class_mip_policyhandler.md)  |  Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
[PolicyProfile::Observer](class_mip_policyprofile_observer.md)  |  Interface [Observer](class_mip_policyprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
[PolicyProfile::Settings](class_mip_policyprofile_settings.md)  |  [Paramètres](class_mip_policyprofile_settings.md) utilisés par [PolicyProfile](class_mip_policyprofile.md) lors de sa création et tout au long de sa durée de vie.
[PolicyProfile](class_mip_policyprofile.md)  |  La classe [PolicyProfile](class_mip_policyprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [PolicyProfile](class_mip_policyprofile.md), mais elle peut créer plusieurs profils si nécessaire.
[PolicySyncError](class_mip_policysyncerror.md)  |  Une tentative de synchronisation des données de stratégie a échoué.
[PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
[ProtectAdhocAction](class_mip_protectadhocaction.md)  |  Classe d’action qui spécifie l’ajout de la protection ad hoc au document.
[ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Classe d’action qui spécifie l’ajout de la protection par modèle au document.
[ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Classe d’action qui spécifie l’ajout de la protection Ne pas transférer au document.
[ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  Description de la protection associée à un élément de contenu.
[ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Construit un [ProtectionDescriptor](class_mip_protectiondescriptor.md) qui décrit la protection associée à un élément de contenu.
[ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  Interface qui reçoit les notifications relatives à [ProtectionEngine](class_mip_protectionengine.md).
[ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  [Settings](class_mip_protectionengine_settings.md) utilisé par [ProtectionEngine](class_mip_protectionengine.md) lors de sa création et tout au long de sa durée de vie.
[ProtectionEngine](class_mip_protectionengine.md)  |  Gère les actions liées à la protection sur une identité spécifique.
[ProtectionHandler::Observer](class_mip_protectionhandler.md)  |  Interface qui reçoit les notifications relatives à [ProtectionHandler](class_mip_protectionhandler.md).
[ProtectionHandler](class_mip_protectionhandler.md)  |  Gère les actions liées à la protection pour une configuration de protection spécifique.
[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  Interface qui reçoit les notifications relatives à [ProtectionProfile](class_mip_protectionprofile.md).
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  [Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de sa création et tout au long de sa durée de vie.
[ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
[RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
[RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Classe d’action qui spécifie la suppression du pied de page de contenu du document.
[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
[RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Classe d’action qui spécifie la suppression de la protection appliquée au document.
[RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Classe d’action qui spécifie la suppression du filigrane du document.
[Flux](class_mip_stream.md)  |  Classe qui définit l’interface entre le SDK MIP et le contenu basé sur le flux de données (Stream).
[TransientNetworkError](class_mip_transientnetworkerror.md)  |  Erreur de mise en réseau temporaire. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service. L’opération peut être retentée, car cette erreur est une erreur temporaire.
[UserRights](class_mip_userrights.md)  |  Groupe d’utilisateurs et droits qui leur sont associés.
[UserRoles](class_mip_userroles.md)  |  Groupe d’utilisateurs et rôles qui leur sont associés.
