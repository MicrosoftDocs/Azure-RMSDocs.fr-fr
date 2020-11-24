---
title: AuthDelegate de classe
description: 'Documente la classe authdelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 9a971a7d0e8cf78baa5231225da620c9e1c8fa47
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567269"
---
# <a name="class-authdelegate"></a>AuthDelegate de classe 
Délégué pour les opérations liées à l’authentification.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtuel bool AcquireOAuth2Token (const Identity& Identity, const OAuth2Challenge& Challenge, OAuth2Token& Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
public virtuel bool AcquireOAuth2Token (const Identity& Identity, const OAuth2Challenge& Challenge, const std :: shared_ptr \<void\>& Context, OAuth2Token& Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
  
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