---
title: HttpRequest de classe
description: 'Documente la classe HttpRequest :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 9384976b01899f6d37b6ac55073014bb4a49e924
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566893"
---
# <a name="class-httprequest"></a>HttpRequest de classe 
Interface qui décrit une seule requête HTTP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de la demande.
public HttpRequestType GetRequestType() const  |  Obtenir le type de requête.
public const std::string& GetUrl() const  |  Obtenir l’URL de la requête.
public const std :: Vector \<uint8_t\>& GetBody () const  |  Obtenir le corps de la requête.
public const std :: map \<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders () const  |  Obtenir les en-têtes de requête.
  
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