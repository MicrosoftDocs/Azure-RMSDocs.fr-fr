---
title: mip::HttpResponse, classe
description: Décrit la classe mip::httpresponse de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9cbd899548be15833456a7c1e1fe34c3b5629717
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650290"
---
# <a name="class-miphttpresponse"></a>mip::HttpResponse, classe 
Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public int32_t GetStatusCode() const  |  Obtenir le code d’état de la réponse.
public const std::string& GetBody() const  |  Obtenir le corps de la requête.
public const std::map\<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders() const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getstatuscode-function"></a>GetStatusCode (fonction)
Obtenir le code d’état de la réponse.

  
**Retourne**: Code d'état
  
### <a name="getbody-function"></a>GetBody (fonction)
Obtenir le corps de la requête.

  
**Retourne**: Corps de la demande
  
### <a name="getheaders-function"></a>GetHeaders (fonction)
Obtenir les en-têtes de requête.

  
**Retourne**: En-têtes de demande