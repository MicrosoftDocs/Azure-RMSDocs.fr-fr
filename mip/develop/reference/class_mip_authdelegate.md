---
title: classe mip::AuthDelegate
description: Décrit la classe mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bcc38bf4b55ca99cf926138279223a4140f7bbf4
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330608"
---
# <a name="class-mipauthdelegate"></a>classe mip::AuthDelegate 
Délégué pour l’authentification des opérations associées.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public bool AcquireOAuth2Token (mip::Identity const & identité, OAuth2Challenge const & défi, OAuth2Token & jeton)  |  Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le défi donné. Le client doit retourner si l’acquisition de jeton a réussi. En cas de réussite, il doit initialiser l’objet de jeton donné.
  
## <a name="members"></a>Membres
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token (fonction)
Cette méthode est appelée lorsqu’un jeton d’authentification est requis pour le moteur de stratégie avec l’identité donnée et le défi donné. Le client doit retourner si l’acquisition de jeton a réussi. En cas de réussite, il doit initialiser l’objet de jeton donné.

Paramètres :  
* **identité**: 


* **défi**: 


* **jeton**:

