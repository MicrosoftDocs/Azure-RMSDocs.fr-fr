---
title: classe mip::HttpOperation
description: Décrit la classe mip::httpoperation de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: e3eaedbf508f116b19521286b686bc955d108efe
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173556"
---
# <a name="class-miphttpoperation"></a>classe mip::HttpOperation 
Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors de la substitution [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID d’opération.
public std::shared_ptr\<HttpResponse\> GetResponse()  |  Obtenez la réponse, le cas échéant.
public bool IsCancelled()  |  Obtenir l’état de l’annulation de l’opération.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId (fonction)
Obtient l’ID d’opération.

  
**Retourne**: ID d’opération correspondant [HttpRequest](class_mip_httprequest.md) et [HttpResponse](class_mip_httpresponse.md) aura le même ID
  
### <a name="getresponse-function"></a>GetResponse (fonction)
Obtenez la réponse, le cas échéant.

  
**Retourne**: Réponse
  
### <a name="iscancelled-function"></a>IsCancelled (fonction)
Obtenir l’état de l’annulation de l’opération.

  
**Retourne**: État de l’annulation