---
title: mip::HttpDelegate, classe
description: 'Documente la classe MIP :: httpdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e629e15ed3a4754123f8ca71adee04d32bc3785f
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488107"
---
# <a name="class-miphttpdelegate"></a>mip::HttpDelegate, classe 
Interface pour le remplacement de la gestion HTTP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr\<HttpOperation\> Send (const std :: shared_ptr\<HttpRequest\>& demande, const std :: shared_ptr\<void\>& contexte)  |  Envoyer une requête HTTP.
public std :: shared_ptr\<HttpOperation\> SendAsync (const std :: shared_ptr\<HttpRequest\>& demande, const std :: shared_ptr\<void\>& contexte, const std :: function\<void (std :: shared_ptr\<HttpOperation\>)  |  Envoyer une requête HTTP de manière asynchrone.
public void CancelOperation (const std :: String & requestId)  |  Annule une opération HTTP spécifique.
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