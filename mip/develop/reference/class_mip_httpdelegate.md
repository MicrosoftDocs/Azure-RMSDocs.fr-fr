---
title: mip HttpDelegate, classe
description: Informations de référence pour la classe mip HttpDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3e55f9aff5a9ebd97731ec21e408a33f22905648
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445352"
---
# <a name="class-miphttpdelegate"></a>mip::HttpDelegate, classe 
Interface pour le remplacement de la gestion HTTP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr<HttpResponse> Send(const std::shared_ptr<HttpRequest>& request, const std::shared_ptr<void>& context)  |  Envoyer une requête HTTP.
  
## <a name="members"></a>Membres
  
### <a name="httpresponse"></a>HttpResponse
Envoyer une requête HTTP.

Paramètres :  
* **request** : requête HTTP 


* **context** : même contexte client opaque qui a été passé à l’API obtenue dans cette requête HTTP



  
**Retourne** : réponse HTTP