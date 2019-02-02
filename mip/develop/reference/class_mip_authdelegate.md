---
title: classe mip::AuthDelegate
description: Décrit la classe mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b6278d605dfbb9a9c4cf0cf1282a159c456c5561
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651994"
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

