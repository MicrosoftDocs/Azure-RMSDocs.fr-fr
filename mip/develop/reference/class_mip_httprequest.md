---
title: mip::HttpRequest, classe
description: Décrit la classe mip::httprequest de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 3c23d37836b241a416cbaf5ee5cd22f8c726794d
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650083"
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