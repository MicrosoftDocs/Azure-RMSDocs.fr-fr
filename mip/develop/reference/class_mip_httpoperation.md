---
title: 'MIP:: HttpOperation, classe'
description: 'Documente la classe MIP:: httpoperation du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d0f72a60233b05eab2c9e4b9e9cec2bf8bcda495
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056028"
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