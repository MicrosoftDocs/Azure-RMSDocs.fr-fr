---
title: mip HttpRequest, classe
description: Informations de référence pour la classe mip HttpRequest
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e838eb247bc00d43da72db1de03304e89a1b1da5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445238"
---
# <a name="class-miphttprequest"></a>mip::HttpRequest, classe 
Interface qui décrit une seule requête HTTP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public HttpRequestType GetRequestType() const  |  Obtenir le type de requête.
 public const std::string& GetUrl() const  |  Obtenir l’URL de la requête.
 public const std::string& GetBody() const  |  Obtenir le corps de la requête.
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="httprequesttype"></a>HttpRequestType
Obtenir le type de requête.

  
**Retourne** : type de requête
  
### <a name="geturl"></a>GetUrl
Obtenir l’URL de la requête.

  
**Retourne** : URL de la requête
  
### <a name="getbody"></a>GetBody
Obtenir le corps de la requête.

  
**Retourne** : corps de la requête
  
### <a name="getheaders"></a>GetHeaders
Obtenir les en-têtes de requête.

  
**Retourne** : en-têtes de requête