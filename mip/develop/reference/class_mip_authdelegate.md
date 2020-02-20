---
title: 'MIP :: AuthDelegate, classe'
description: 'Documente la classe MIP :: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 30907f3bf4a08f72305a59290c8cbd891def44c9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490606"
---
# <a name="class-mipauthdelegate"></a>MIP :: AuthDelegate, classe 
Délégué pour les opérations liées à l’authentification.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtuel bool AcquireOAuth2Token (const MIP :: Identity & Identity, const OAuth2Challenge & Challenge, OAuth2Token & Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
public virtuel bool AcquireOAuth2Token (const MIP :: Identity & Identity, const OAuth2Challenge & Challenge, const std :: shared_ptr\<void\>& contexte, OAuth2Token & Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
  
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