---
title: 'MIP:: AuthDelegate, classe'
description: 'Documente la classe MIP:: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f1f2a9f1f1f61d381cbf0da58cfdef9cad6044e2
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056295"
---
# <a name="class-mipauthdelegate"></a>MIP:: AuthDelegate, classe 
Délégué pour les opérations liées à l’authentification.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtuel bool AcquireOAuth2Token (const MIP:: Identity & Identity, const OAuth2Challenge & Challenge, OAuth2Token & Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
public virtuel bool AcquireOAuth2Token (const MIP:: Identity & Identity, const OAuth2Challenge & Challenge, const std:\<:\>shared_ptr void & Context, OAuth2Token & Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
  
## <a name="members"></a>Membres
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token fonction)
Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.

Paramètres :  
* **identité**: 


* **défi**: 


* **jeton**: 


> Déconseillé Cette méthode sera bientôt dépréciée en faveur de celle qui accepte un paramètre de contexte. Si la nouvelle version a été implémentée, il n’est pas nécessaire d’implémenter cette version.
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token fonction)
Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.

Paramètres :  
* **identité**: Utilisateur pour lequel un jeton est demandé 


* **défi**: Défi OAuth2 


* **contexte**: Contexte opaque passé à l’API MIP par l’application hôte 


* **jeton**: [sortie] jeton OAuth2 encodé en base64

