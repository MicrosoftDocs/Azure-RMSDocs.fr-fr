---
title: ProxyAuthenticationError de classe
description: 'Documente la classe proxyauthenticationerror :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 04915e74cc09f271a2ca3bb256b906bc442bb3fd
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214301"
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

Catégorie d’erreur réseau.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Unknown            | Défaillance réseau inconnue
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
