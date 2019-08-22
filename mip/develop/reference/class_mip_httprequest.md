---
title: mip::HttpRequest, classe
description: 'Documente la classe MIP:: HttpRequest du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 28584ffa19c2ceb00f4ab3839f945adf737bdb3b
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885574"
---
# <a name="class-miphttprequest"></a>mip::HttpRequest, classe 
Interface qui décrit une seule requête HTTP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de la demande.
public HttpRequestType GetRequestType() const  |  Obtenir le type de requête.
public const std::string& GetUrl() const  |  Obtenir l’URL de la requête.
public const std:: Vector\<uint8_t\>& GetBody () const  |  Obtenir le corps de la requête.
public const std:: map\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtient l’ID de la demande.

  
**Retourne**: ID de la requête la HttpResponse correspondante aura le même ID
  
### <a name="getrequesttype-function"></a>GetRequestType fonction)
Obtenir le type de requête.

  
**Retourne**: Type de demande
  
### <a name="geturl-function"></a>GetUrl, fonction
Obtenir l’URL de la requête.

  
**Retourne**: URL de la requête
  
### <a name="getbody-function"></a>GetBody fonction)
Obtenir le corps de la requête.

  
**Retourne**: Corps de la demande
  
### <a name="getheaders-function"></a>GetHeaders fonction)
Obtenir les en-têtes de requête.

  
**Retourne**: En-têtes de requête