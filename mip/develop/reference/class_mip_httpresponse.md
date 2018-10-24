---
title: mip HttpResponse, classe
description: Informations de référence pour la classe mip HttpResponse
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a19ea78b048cafe94501d452bb9c7409237f6ffd
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445347"
---
# <a name="class-miphttpresponse"></a>mip::HttpResponse, classe 
Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public int32_t GetStatusCode() const  |  Obtenir le code d’état de la réponse.
 public const std::string& GetBody() const  |  Obtenir le corps de la requête.
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getstatuscode"></a>GetStatusCode
Obtenir le code d’état de la réponse.

  
**Retourne** : code d’état
  
### <a name="getbody"></a>GetBody
Obtenir le corps de la requête.

  
**Retourne** : corps de la requête
  
### <a name="getheaders"></a>GetHeaders
Obtenir les en-têtes de requête.

  
**Retourne** : en-têtes de requête