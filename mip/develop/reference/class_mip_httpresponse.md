---
title: mip::HttpResponse, classe
description: 'Documente la classe MIP :: HttpResponse du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e24eef471b11daffadb84235edbc93ff14696c25
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488056"
---
# <a name="class-miphttpresponse"></a>mip::HttpResponse, classe 
Interface qui décrit une réponse HTTP unique, implémentée par l’application cliente lors du remplacement de HttpDelegate.
  
## <a name="summary"></a>Résumé
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