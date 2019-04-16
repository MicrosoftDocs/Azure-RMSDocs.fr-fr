---
title: mip::HttpResponse, classe
description: Décrit la classe mip::httpresponse de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 06bc3f52bdecd85412dc0c35df46c7847167aa1b
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573752"
---
# <a name="class-miphttpresponse"></a>mip::HttpResponse, classe 
Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient le code de réponse.
public int32_t GetStatusCode() const  |  Obtenir le code d’état de la réponse.
public const std::vector\<uint8_t\>& GetBody() const  |  Obtenir le corps de la requête.
public const std::map\<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders() const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId (fonction)
Obtient le code de réponse.

  
**Retourne**: ID de réponse correspondants [HttpRequest](class_mip_httprequest.md) ont le même ID
  
### <a name="getstatuscode-function"></a>GetStatusCode (fonction)
Obtenir le code d’état de la réponse.

  
**Retourne**: Code d'état
  
### <a name="getbody-function"></a>GetBody (fonction)
Obtenir le corps de la requête.

  
**Retourne**: Corps de demande
  
### <a name="getheaders-function"></a>GetHeaders (fonction)
Obtenir les en-têtes de requête.

  
**Retourne**: En-têtes de demande