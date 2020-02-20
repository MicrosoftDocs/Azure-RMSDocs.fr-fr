---
title: mip::HttpRequest, classe
description: 'Documente la classe MIP :: HttpRequest du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f3b26ad07b8b3bfc556646cfd96a71aa9188bbb0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488090"
---
# <a name="class-miphttprequest"></a>mip::HttpRequest, classe 
Interface qui décrit une seule requête HTTP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de la demande.
public HttpRequestType GetRequestType() const  |  Obtenir le type de requête.
public const std::string& GetUrl() const  |  Obtenir l’URL de la requête.
public const std :: Vector\<uint8_t\>& GetBody () const  |  Obtenir le corps de la requête.
public const std :: Map\<std :: String, std :: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtient l’ID de la demande.

  
**Retourne**: l’ID de la demande, la HttpResponse correspondante a le même ID
  
### <a name="getrequesttype-function"></a>GetRequestType fonction)
Obtenir le type de requête.

  
**Retourne** : type de requête
  
### <a name="geturl-function"></a>GetUrl, fonction
Obtenir l’URL de la requête.

  
**Retourne** : URL de la requête
  
### <a name="getbody-function"></a>GetBody fonction)
Obtenir le corps de la requête.

  
**Retourne** : corps de la requête
  
### <a name="getheaders-function"></a>GetHeaders fonction)
Obtenir les en-têtes de requête.

  
**Retourne** : en-têtes de requête