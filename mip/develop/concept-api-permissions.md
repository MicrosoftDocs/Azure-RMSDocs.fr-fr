---
title: Autorisations d’API requises-Kit de développement logiciel (SDK) Microsoft Information Protection
description: Détails techniques sur les autorisations d’API nécessaires pour les opérations du kit de développement logiciel (SDK) Microsoft Information Protection.
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: ce44c0d8b65f477fdd7b08f34cfe2aacc890d259
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567924"
---
# <a name="api-permissions-for-the-microsoft-information-protection-sdk"></a>Autorisations d’API pour le kit de développement logiciel (SDK) Microsoft Information Protection

Le kit de développement logiciel MIP utilise deux services Azure principaux pour l’étiquetage et la protection. Dans le panneau Azure Active Directory les autorisations de l’application, ces services sont les suivants :

- Service Rights Management Azure
- Service de synchronisation de Information Protection Microsoft

Les autorisations d’application doivent être accordées à une ou plusieurs API lors de l’utilisation du kit de développement logiciel (SDK) MIP pour l’étiquetage et la protection. Différents scénarios d’authentification d’application peuvent nécessiter des autorisations d’application différentes. Pour les scénarios d’authentification d’application, reportez-vous à [scénarios d’authentification](/azure/active-directory/develop/authentication-flows-app-scenarios).

Le consentement de l’administrateur au niveau du locataire doit être accordé aux autorisations de l’application lorsque le consentement de l’administrateur est requis, comme décrit dans [la documentation AAD](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations).

## <a name="application-permissions"></a>Autorisations de l’application

Les autorisations d’application permettent à une application de Azure Active Directory d’agir en tant qu’entité propre, plutôt qu’au nom d’un utilisateur spécifique.

| Service                         | Nom de l'autorisation           | Description                                  | Consentement de l’administrateur requis |
| ------------------------------- | ------------------------- | -------------------------------------------- | ---------------------- |
| Service Rights Management Azure | Contenu. superutilisateur         | Lire tout le contenu protégé pour ce locataire   | Yes                    |
| Service Rights Management Azure | Contenu. DelegatedReader   | Lire du contenu protégé pour le compte d’un utilisateur   | Yes                    |
| Service Rights Management Azure | Contenu. DelegatedWriter   | Créer du contenu protégé pour le compte d’un utilisateur | Yes                    |
| Service Rights Management Azure | Content. Writer            | Créer du contenu protégé                     | Yes                    |
| Service de synchronisation MIP                | UnifiedPolicy. locataire. Read | Lire toutes les stratégies unifiées du locataire      | Yes                    |

### <a name="contentsuperuser"></a>Contenu. superutilisateur

Cette autorisation est requise lorsqu’une application doit être autorisée à déchiffrer tout le contenu protégé pour le locataire spécifique. Des exemples de services qui requièrent des droits de super utilisateur sont les services de protection contre la perte de données ou de service Broker pour la sécurité d’accès au Cloud qui doivent être en mesure d’afficher tout le contenu en texte brut pour prendre des décisions de stratégie concernant l’emplacement de stockage des données ou leur stockage.  

### <a name="contentdelegatedwriter"></a>Contenu. DelegatedWriter

Cette autorisation est requise lorsqu’une application doit être autorisée à chiffrer le contenu protégé par un utilisateur spécifique. Les exemples de services qui requièrent des droits d’écriture délégués sont des applications métier qui doivent chiffrer du contenu en fonction des stratégies d’étiquette de l’utilisateur pour appliquer des étiquettes et chiffrer ou chiffrer le contenu en mode natif. Cette autorisation permet à l’application de chiffrer le contenu dans le contexte de l’utilisateur.

### <a name="contentdelegatedreader"></a>Contenu. DelegatedReader

Cette autorisation est requise lorsqu’une application doit être autorisée à déchiffrer tout le contenu protégé pour un utilisateur spécifique. Les exemples de services qui requièrent des droits de lecture délégués sont des applications métier qui doivent déchiffrer le contenu en fonction des stratégies d’étiquette de l’utilisateur pour afficher le contenu en mode natif. Cette autorisation permet à l’application de déchiffrer et de lire le contenu dans le contexte de l’utilisateur.

### <a name="contentwriter"></a>Content. Writer

Cette autorisation est requise lorsqu’une application doit être autorisée à chiffrer du contenu. Les exemples de services qui requièrent l’enregistreur sont des applications métier qui appliquent des étiquettes de classification aux fichiers lors de l’exportation. Content. Writer chiffre le contenu en tant qu’identité du principal du service et, par conséquent, le propriétaire des fichiers protégés est l’identité du principal du service.

### <a name="unifiedpolicytenantread"></a>UnifiedPolicy. locataire. Read

Cette autorisation est requise lorsqu’une application doit être autorisée à télécharger des stratégies d’étiquetage unifiées pour le locataire. Les applications qui nécessitent l’utilisation d’étiquettes en tant qu’identité de principal du service sont des exemples de services nécessitant une lecture de locataire de stratégie unifiée.

## <a name="delegated-permissions"></a>Autorisations déléguées

Les autorisations déléguées permettent à une application de Azure Active Directory d’effectuer des actions pour le compte d’un utilisateur particulier.

| Service                         | Nom de l'autorisation         | Description                                      | Consentement de l’administrateur requis |
| ------------------------------- | ----------------------- | ------------------------------------------------ | ---------------------- |
| Service Rights Management Azure | user_impersonation      | Créer et accéder à du contenu protégé pour l’utilisateur | No                     |
| Service de synchronisation MIP                | UnifiedPolicy. utilisateur. Read | Lire toutes les stratégies unifiées auxquelles un utilisateur a accès   | No                     |

### <a name="user_impersonation"></a>user_impersonation

Cette autorisation est requise lorsqu’une application doit être autorisée à utiliser les services Azure Rights Management pour le compte de l’utilisateur. Les applications qui doivent chiffrer ou accéder au contenu en fonction des stratégies d’étiquette de l’utilisateur sont des exemples de services nécessitant des droits d’User_Impersonation pour appliquer des étiquettes ou chiffrer du contenu en mode natif.
  
### <a name="unifiedpolicyuserread"></a>UnifiedPolicy. utilisateur. Read

Cette autorisation est requise lorsqu’une application doit être autorisée à lire des stratégies d’étiquetage unifiées associées à un utilisateur. chiffrer le contenu protégé par un utilisateur spécifique. Des exemples de services qui requièrent des droits d’écriture délégués sont des applications qui doivent chiffrer du contenu en fonction des stratégies d’étiquette de l’utilisateur pour appliquer des étiquettes et ou chiffrer le contenu en mode natif.