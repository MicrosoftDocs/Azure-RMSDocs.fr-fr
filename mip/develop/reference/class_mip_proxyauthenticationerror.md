---
title: ProxyAuthenticationError de classe
description: 'Documente la classe proxyauthenticationerror :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d4468fe243f7120630d0a34d453ff4e9a5bf6527
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567078"
---
# <a name="class-proxyauthenticationerror"></a>ProxyAuthenticationError de classe 
Échec de l’authentification du proxy.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
GetCategory de catégorie publique () const  |  Obtient la catégorie de défaillance du réseau.
int32_t public GetResponseStatusCode () const  |  Obtient le code d’état de réponse HTTP.
Catégorie d’énumération  |  Catégorie d’erreur réseau.
  
## <a name="members"></a>Membres
  
### <a name="getcategory-function"></a>GetCategory fonction)
Obtient la catégorie de défaillance du réseau.

  
**Retourne**: catégorie de défaillance réseau
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode fonction)
Obtient le code d’état de réponse HTTP.

  
**Retourne**: code d’état de réponse http, 0 si aucun
  
### <a name="category-enum"></a>Enum de catégorie

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Inconnu            | Défaillance réseau inconnue
FailureResponseCode            | Le code de réponse HTTP indique un échec
BadResponse            | Impossible de lire la réponse HTTP
UnexpectedResponse            | La réponse HTTP est terminée, mais contient des données inattendues
NoConnection            | Échec de l’établissement d’une connexion
Proxy            | Échec du proxy
SSL            | Échec SSL
Délai d'expiration            | Délai de connexion dépassé
Hors connexion            | L’opération requiert une connectivité réseau
Throttled            | Échec de l’opération HTTP en raison de la limitation du trafic du serveur
Annulé            | L’opération HTTP a été annulée par l’application

Catégorie d’erreur réseau.