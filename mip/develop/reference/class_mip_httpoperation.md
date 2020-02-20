---
title: 'MIP :: HttpOperation, classe'
description: 'Documente la classe MIP :: httpoperation du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 4be7b54dd5df255c488043d84ebcfebbce7e6ac2
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489994"
---
# <a name="class-miphttpoperation"></a>MIP :: HttpOperation, classe 
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

  
**Retourne**: l’ID de l’opération, les HttpRequest et HttpResponse correspondants ont le même ID
  
### <a name="getresponse-function"></a>GetResponse, fonction
Obtient la réponse, le cas échéant.

  
**Retourne**: réponse
  
### <a name="iscancelled-function"></a>IsCancelled, fonction
Obtient l’état de l’annulation de l’opération.

  
**Retourne**: état d’annulation