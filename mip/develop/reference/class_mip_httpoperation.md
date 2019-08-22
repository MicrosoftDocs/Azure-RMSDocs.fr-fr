---
title: 'MIP:: HttpOperation, classe'
description: 'Documente la classe MIP:: httpoperation du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 8503a5466fe180fc6831e85e1b53954ba99f55c7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884105"
---
# <a name="class-miphttpoperation"></a>MIP:: HttpOperation, classe 
Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de l’opération.
public std:: shared_ptr\<HttpResponse\> GetResponse ()  |  Obtient la réponse, le cas échéant.
public bool IsCancelled ()  |  Obtient l’état de l’annulation de l’opération.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtient l’ID de l’opération.

  
**Retourne**: ID de l’opération les HttpRequest et HttpResponse correspondants auront le même ID
  
### <a name="getresponse-function"></a>GetResponse, fonction
Obtient la réponse, le cas échéant.

  
**Retourne**: response
  
### <a name="iscancelled-function"></a>IsCancelled, fonction
Obtient l’état de l’annulation de l’opération.

  
**Retourne**: État de l’annulation