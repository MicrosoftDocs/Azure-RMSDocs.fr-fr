---
title: AuthDelegate de classe
description: 'Documente la classe authdelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: a7cbc6789fc6baa8fbb01ffb8c6d6ea7e9294d4f
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763628"
---
# <a name="class-authdelegate"></a>AuthDelegate de classe 
Délégué pour les opérations liées à l’authentification.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtuel bool AcquireOAuth2Token (const Identity& Identity, const OAuth2Challenge& Challenge, OAuth2Token& Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
public virtuel bool AcquireOAuth2Token (const Identity& Identity, const OAuth2Challenge& Challenge, const std :\<:\> shared_ptr void& Context, OAuth2Token& Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
  
## <a name="members"></a>Membres
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token fonction)
Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.

Paramètres :  
* **identité**: utilisateur pour lequel un jeton est demandé 


* **défi**: OAuth2 Challenge 


* **jeton**: [sortie] jeton OAuth2 encodé en base64



  
**Retourne**: true si le jeton a été acquis avec succès, sinon false en cas d’échec, si le paramètre de sortie du jeton contient un message d’erreur, il est inclus dans l’exception NoAuthTokenError qui sera ensuite déclenchée par l’application.
> Déconseillé : cette méthode sera bientôt dépréciée en faveur de celle qui accepte un paramètre de contexte. Si la nouvelle version a été implémentée, il n’est pas nécessaire d’implémenter cette version.
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token fonction)
Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.

Paramètres :  
* **identité**: utilisateur pour lequel un jeton est demandé 


* **défi**: OAuth2 Challenge 


* **Context**: contexte opaque passé à l’API MIP par l’application hôte 


* **jeton**: [sortie] jeton OAuth2 encodé en base64



  
**Retourne**: true si le jeton a été acquis avec succès, sinon false en cas d’échec, si le paramètre de sortie du jeton contient un message d’erreur, il est inclus dans l’exception NoAuthTokenError qui sera ensuite déclenchée par l’application.