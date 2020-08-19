---
title: ProxyAuthenticationError de classe
description: 'Documente la classe proxyauthenticationerror :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 0da14f6a13632c0bf45ac3a409b0033a9ee1c603
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564414"
---
# <a name="class-proxyauthenticationerror"></a>ProxyAuthenticationError de classe 
Échec de l’authentification du proxy.
  
## <a name="summary"></a>Récapitulatif

| Membres                                       | Descriptions
|-----------------------------------------------|---------------------------------------------
| GetCategory de catégorie publique () const           |  Obtient la catégorie de défaillance du réseau.
| int32_t public GetResponseStatusCode () const  |  Obtient le code d’état de réponse HTTP.
| Catégorie d’énumération                                 |  Catégorie d’erreur réseau.
  
## <a name="members"></a>Membres
  
### <a name="getcategory-function"></a>GetCategory fonction)

Obtient la catégorie de défaillance du réseau.

**Retourne**: catégorie de défaillance réseau
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode fonction)

Obtient le code d’état de réponse HTTP.

**Retourne**: code d’état de réponse http, 0 si aucun
  
### <a name="category-enum"></a>Enum de catégorie

Catégorie d’erreur réseau.

| Valeurs                   | Descriptions
|--------------------------|---------------------------------------------
| Unknown                  | Défaillance réseau inconnue
| FailureResponseCode      | Le code de réponse HTTP indique un échec
| BadResponse              | Impossible de lire la réponse HTTP
| UnexpectedResponse       | La réponse HTTP est terminée, mais contient des données inattendues
| NoConnection             | Échec de l’établissement d’une connexion
| Proxy                    | Échec du proxy
| SSL                      | Échec SSL
| Délai d'expiration                  | Délai de connexion dépassé
| Hors connexion                  | L’opération requiert une connectivité réseau
| Throttled                | Échec de l’opération HTTP en raison de la limitation du trafic du serveur
| Annulé                | L’opération HTTP a été annulée par l’application
