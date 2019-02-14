---
title: classe mip::AuthDelegate
description: Décrit la classe mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cf6ea43b36518f2eec74b9ed0f8682466aa6b64d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258009"
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

