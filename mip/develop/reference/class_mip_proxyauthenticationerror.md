---
title: MIP de classe ::P roxyAuthenticationError
description: Documente la classe MIP ::p roxyauthenticationerror du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c0289f9b2f2a8a1163e62e6c6a96e3023f297194
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489620"
---
# <a name="class-mipproxyauthenticationerror"></a>MIP de classe ::P roxyAuthenticationError 
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
Inconnu.            | Défaillance réseau inconnue
FailureResponseCode            | Le code de réponse HTTP indique un échec
BadResponse            | Impossible de lire la réponse HTTP
UnexpectedResponse            | La réponse HTTP est terminée, mais contient des données inattendues
NoConnection            | Échec de l’établissement d’une connexion
Proxy            | Échec du proxy
SSL            | Échec SSL
Délai d'expiration            | Délai de connexion dépassé
Offline            | L’opération requiert une connectivité réseau
Limitée            | Échec de l’opération HTTP en raison de la limitation du trafic du serveur
Annulé            | L’opération HTTP a été annulée par l’application
Catégorie d’erreur réseau.