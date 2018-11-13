---
title: Concepts - Audit dans l’API de stratégie du kit SDK Microsoft Information Protection
description: Cet article vous aide à comprendre comment utiliser le kit SDK Microsoft Information Protection pour envoyer les événements d’audit de l’API de stratégie aux fonctionnalités d’analyse Azure Information Protection.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/07/2018
ms.author: tommos
ms.openlocfilehash: c660a5f58acd87ff9047a21fea26cc2732667493
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297817"
---
# <a name="auditing-in-the-mip-sdk"></a>Audit dans le kit SDK MIP

Le portail d’administration Azure Information Protection permet d’accéder aux rapports de l’administrateur. Ces rapports fournissent une visibilité des étiquettes que les utilisateurs appliquent, manuellement ou automatiquement, dans les applications où le kit SDK MIP est intégré. Les partenaires de développement qui tirent parti du kit SDK peuvent facilement activer cette fonctionnalité, ce qui leur permet de faire figurer les informations de leurs applications dans les rapports des clients.

## <a name="event-types"></a>Types d'événements

Il existe trois types d’événement pouvant être envoyés via le kit SDK aux fonctionnalités d’analyse Azure Information Protection. **Événements de pulsation**, **événements de détection** et **événements de changement**

### <a name="heartbeat-events"></a>Événements de pulsation

Les événements de pulsation sont générés automatiquement pour toutes les applications auxquelles l’API de stratégie a été intégrée. Les événements de pulsation sont les suivants :

* TenantId
* Heure de la génération
* Nom d'utilisateur principal
* Nom de la machine sur laquelle l’audit a été généré
* Nom du processus
* Plate-forme
* ID d’application - Correspond à l’ID d’application Azure AD.

Ces événements permettent de détecter les applications de votre entreprise qui utilisent le kit SDK Microsoft Information Protection.

### <a name="discovery-events"></a>Événements de détection

Les événements de détection fournissent des détails sur les informations étiquetées qui sont lues ou consommées par l’API de stratégie. Ces événements sont utiles, car ils indiquent les appareils et leur localisation, ainsi que les utilisateurs qui accèdent aux informations d’une organisation.

Vous générez les événements de détection dans l’API de stratégie en définissant un indicateur booléen durant la création de l’objet `mip::PolicyHandler` via `mip::PolicyEngine`. Dans l’exemple ci-dessous, **isAuditDiscoveryEnabled** a la valeur true. Quand `mip::ExecutionState` est passé à `ComputeActions()` ou `GetSensitivityLabel()` (avec les informations de métadonnées et l’identificateur de contenu existants), ces informations de détection sont envoyées aux fonctionnalités d’analyse Azure Information Protection.

L’événement de détection d’audit est généré une fois que l’application a appelé `ComputeActions()` ou `GetSensitivityLabel()`, et qu’elle a fourni `mip::ExecutionState`. Cet événement est généré une seule fois par gestionnaire.

Pour plus d’informations sur l’état d’exécution, consultez la documentation relative aux concepts `mip::ExecutionState`.

```cpp
// Create PolicyHandler, passing in true for isAuditDiscoveryEnabled
auto handler = mEngine->CreatePolicyHandler(true);

// Returns vector of mip::Action and generates discovery event.
auto actions = handler->ComputeActions(*state);

//Or, get the label for a given state
auto label = handler->GetSensitivityLabel(*state);
```

En pratique, **isAuditDiscoveryEnabled** doit avoir la valeur `true` durant la construction de `mip::PolicyHandler` pour permettre l’envoi des informations d’accès aux fichiers vers les fonctionnalités d’analyse Azure Information Protection.

## <a name="change-event"></a>Événement de changement

Les événements de changement fournissent des informations sur le fichier, l’étiquette appliquée ou changée, ainsi que les justifications fournies par l’utilisateur. Les événements de changement sont générés via l’appel de `NotifyCommittedActions()` sur `mip::PolicyHandler`. L’appel est effectué une fois qu’un changement a été correctement validé dans un fichier, en passant le `mip::ExecutionState` utilisé pour calculer les actions.

> Si l’application ne parvient pas à appeler cette fonction, aucun événement n’est envoyé aux fonctionnalités d’analyse Azure Information Protection.

```cpp
handler->NotifyCommittedActions(*state);
```

## <a name="audit-dashboard"></a>Tableau de bord d’audit

Les événements envoyés au pipeline d’audit Azure Information Protection apparaissent dans les rapports sur https://portal.azure.com. Les fonctionnalités d’analyse Azure Information Protection sont en préversion publique et sont susceptibles de changer.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’expérience utilisateur d’audit dans Azure Information Protection, consultez le [blog d’annonces de la préversion sur Tech Community](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854).

