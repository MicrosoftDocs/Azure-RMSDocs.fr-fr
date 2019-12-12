---
title: 'MIP :: AuthDelegate, classe'
description: 'Documente la classe MIP :: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 3dc5679893c0de02eb9b9cb4f197c5ea39bf356f
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560335"
---
# <a name="class-mipauthdelegate"></a>MIP :: AuthDelegate, classe 
Délégué pour les opérations liées à l’authentification.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtuel bool AcquireOAuth2Token (const MIP :: Identity & Identity, const OAuth2Challenge & Challenge, OAuth2Token & Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
public virtuel bool AcquireOAuth2Token (const MIP :: Identity & Identity, const OAuth2Challenge & Challenge, const std :: shared_ptr\<void\>& contexte, OAuth2Token & Token)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.
  
## <a name="members"></a>Membres
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token fonction)
Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.

Paramètres :  
* **identité**: 


* **défi**: 


* **token** : 


> Déconseillé : cette méthode sera bientôt dépréciée en faveur de celle qui accepte un paramètre de contexte. Si la nouvelle version a été implémentée, il n’est pas nécessaire d’implémenter cette version.
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token fonction)
Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le Challenge donné. Le client doit retourner une valeur indiquant si l’acquisition du jeton a réussi. En cas de réussite, elle doit initialiser l’objet de jeton donné.

Paramètres :  
* **identité**: utilisateur pour lequel un jeton est demandé 


* **défi**: OAuth2 Challenge 


* **Context**: contexte opaque passé à l’API MIP par l’application hôte 


* **jeton**: [sortie] jeton OAuth2 encodé en base64

