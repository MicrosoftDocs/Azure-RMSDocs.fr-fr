---
title: mip::HttpResponse, classe
description: Décrit la classe mip::httpresponse de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 00a6d7dd3728edbf6fb1dbb4e59c537d7b6cf911
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252994"
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
