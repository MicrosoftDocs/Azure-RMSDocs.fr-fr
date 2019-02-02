---
title: mip::HttpDelegate, classe
description: Décrit la classe mip::httpdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 68d26b23c1e3ea2e29c22316f80e18937ab78d5c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651018"
---
# <a name="class-miphttpdelegate"></a>mip::HttpDelegate, classe 
Interface pour le remplacement de la gestion HTTP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<HttpResponse\> Send(const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& context)  |  Envoyer une requête HTTP.
public void SendAsync(const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& context, const std::function\<void(std::shared_ptr\<HttpResponse\>)\>& fnCallback)  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="send-function"></a>Send, fonction
Envoyer une requête HTTP.

Paramètres :  
* **demande**: Requête HTTP 


* **contexte**: Le même contexte client opaque qui a été passé à l’API qui a entraîné cette requête HTTP



  
**Retourne**: Réponse HTTP
  
### <a name="sendasync-function"></a>SendAsync (fonction)
_Pas encore documenté._
