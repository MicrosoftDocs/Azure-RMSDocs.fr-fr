---
title: mip::HttpResponse, classe
description: 'Documente la classe MIP :: HttpResponse du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 876de8047abc4e2f13ee8e103cdfa1648738aa84
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558755"
---
# <a name="class-miphttpresponse"></a>mip::HttpResponse, classe 
Interface qui décrit une réponse HTTP unique, implémentée par l’application cliente lors du remplacement de HttpDelegate.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de réponse.
public int32_t GetStatusCode() const  |  Obtenir le code d’état de la réponse.
public const std :: Vector\<uint8_t\>& GetBody () const  |  Obtenir le corps de la requête.
public const std :: Map\<std :: String, std :: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtient l’ID de réponse.

  
**Retourne**: ID de réponse auquel les HttpRequest correspondants auront le même ID
  
### <a name="getstatuscode-function"></a>GetStatusCode fonction)
Obtenir le code d’état de la réponse.

  
**Retourne** : code d’état
  
### <a name="getbody-function"></a>GetBody fonction)
Obtenir le corps de la requête.

  
**Retourne** : corps de la requête
  
### <a name="getheaders-function"></a>GetHeaders fonction)
Obtenir les en-têtes de requête.

  
**Retourne** : en-têtes de requête