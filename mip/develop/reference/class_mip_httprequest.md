---
title: HttpRequest de classe
description: 'Documente la classe HttpRequest :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: af302a760ee6b8f24b077b2c45bfe86ab0a80dac
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762710"
---
# <a name="class-httprequest"></a>HttpRequest de classe 
Interface qui décrit une seule requête HTTP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de la demande.
public HttpRequestType GetRequestType() const  |  Obtenir le type de requête.
public const std::string& GetUrl() const  |  Obtenir l’URL de la requête.
public const std :: Vector\<Uint8_t\>& GetBody () const  |  Obtenir le corps de la requête.
public const std :: map\<std :: String, std :: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Obtenir les en-têtes de requête.
  
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