---
title: HttpDelegate de classe
description: 'Documente la classe httpdelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 9240f0ed4eca43d7a6dcd5045c80f9724dc2a11b
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215253"
---
# <a name="class-httpdelegate"></a>HttpDelegate de classe 
Interface pour le remplacement de la gestion HTTP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<HttpOperation\> Send(const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& context)  |  Envoyer une requête HTTP.
public std :: shared_ptr \<HttpOperation\> SendAsync (const std :: shared_ptr \<HttpRequest\>& demande, const std :: shared_ptr \<void\>& contexte, const std :: function \<void(std::shared_ptr\<HttpOperation\> )  |  Envoyer une requête HTTP de manière asynchrone.
public void CancelOperation (const std :: String& requestId)  |  Annule une opération HTTP spécifique.
public void CancelAllOperations ()  |  Annuler les requêtes HTTP en cours.
  
## <a name="members"></a>Membres
  
### <a name="send-function"></a>Send, fonction
Envoyer une requête HTTP.

Paramètres :  
* **request** : requête HTTP 


* **context** : même contexte client opaque qui a été passé à l’API obtenue dans cette requête HTTP



  
**Retourne**: conteneur d’opération http
  
### <a name="sendasync-function"></a>SendAsync, fonction
Envoyer une requête HTTP de manière asynchrone.

Paramètres :  
* **request** : requête HTTP 


* **context** : même contexte client opaque qui a été passé à l’API obtenue dans cette requête HTTP 


* **callbackFn**: fonction qui sera exécutée à la fin



  
**Retourne**: conteneur d’opération http
  
### <a name="canceloperation-function"></a>CancelOperation fonction)
Annule une opération HTTP spécifique.

Paramètres :  
* **RequestId**: ID de la demande à annuler


  
### <a name="cancelalloperations-function"></a>CancelAllOperations fonction)
Annuler les requêtes HTTP en cours.