---
title: mip::HttpRequest, classe
description: Décrit la classe mip::httprequest de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 56c736d985e7c8bd258fcb7c1f7e42b5db3801fd
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256938"
---
# <a name="class-miphttprequest"></a>mip::HttpRequest, classe 
Interface qui décrit une seule requête HTTP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public HttpRequestType GetRequestType() const  |  Obtenir le type de requête.
public const std::string& GetUrl() const  |  Obtenir l’URL de la requête.
public const std::string& GetBody() const  |  Obtenir le corps de la requête.
public const std::map\<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders() const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getrequesttype-function"></a>GetRequestType (fonction)
Obtenir le type de requête.

  
**Retourne**: Type de demande
  
### <a name="geturl-function"></a>GetUrl (fonction)
Obtenir l’URL de la requête.

  
**Retourne**: Url de la demande
  
### <a name="getbody-function"></a>GetBody (fonction)
Obtenir le corps de la requête.

  
**Retourne**: Corps de la demande
  
### <a name="getheaders-function"></a>GetHeaders (fonction)
Obtenir les en-têtes de requête.

  
**Retourne**: En-têtes de demande
