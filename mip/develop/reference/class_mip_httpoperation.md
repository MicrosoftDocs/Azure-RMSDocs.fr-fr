---
title: 'MIP :: HttpOperation, classe'
description: 'Documente la classe MIP :: httpoperation du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6f0c3cc726d72d89a8682907ebc350270db5daee
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558791"
---
# <a name="class-miphttpoperation"></a>MIP :: HttpOperation, classe 
Interface qui décrit une seule opération HTTP, implémentée par l’application cliente lors du remplacement de HttpDelegate.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de l’opération.
public std :: shared_ptr\<HttpResponse\> GetResponse ()  |  Obtient la réponse, le cas échéant.
public bool IsCancelled ()  |  Obtient l’état de l’annulation de l’opération.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtient l’ID de l’opération.

  
**Retourne**: l’ID de l’opération, les HttpRequest et HttpResponse correspondants ont le même ID
  
### <a name="getresponse-function"></a>GetResponse, fonction
Obtient la réponse, le cas échéant.

  
**Retourne**: réponse
  
### <a name="iscancelled-function"></a>IsCancelled, fonction
Obtient l’état de l’annulation de l’opération.

  
**Retourne**: état d’annulation