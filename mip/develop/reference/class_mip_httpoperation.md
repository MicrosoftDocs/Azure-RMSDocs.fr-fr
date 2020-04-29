---
title: HttpOperation de classe
description: 'Documente la classe httpoperation :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 09fac96f16bf18e72d6217842728d48244b9c412
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762809"
---
# <a name="class-httpoperation"></a>HttpOperation de classe 
Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors du remplacement de HttpDelegate.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de l’opération.
public std :: shared_ptr\<HttpResponse\> GetResponse ()  |  Obtient la réponse, le cas échéant.
public bool IsCancelled ()  |  Obtient l’état de l’annulation de l’opération.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtient l’ID de l’opération.

  
**Retourne**: l’ID de l’opération, les [HttpRequest](class_mip_httprequest.md) et [HTTPRESPONSE](class_mip_httpresponse.md) correspondants ont le même ID
  
### <a name="getresponse-function"></a>GetResponse, fonction
Obtient la réponse, le cas échéant.

  
**Retourne**: réponse
  
### <a name="iscancelled-function"></a>IsCancelled, fonction
Obtient l’état de l’annulation de l’opération.

  
**Retourne**: état d’annulation