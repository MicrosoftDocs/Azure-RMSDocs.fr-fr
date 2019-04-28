---
title: mip::HttpDelegate, classe
description: Décrit la classe mip::httpdelegate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6dedd5e52b0599a58acabd85f7bd076169b3758e
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60174049"
---
# <a name="class-miphttpdelegate"></a>mip::HttpDelegate, classe 
Interface pour le remplacement de la gestion HTTP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<HttpOperation\> Send(const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& context)  |  Envoyer une requête HTTP.
public std::shared_ptr\<HttpOperation\> SendAsync (const std::shared_ptr\<HttpRequest\>& demande, const std::shared_ptr\<void\>& contexte, const std :: fonction\<void (std::shared_ptr\<HttpOperation\>)\>& callbackFn)  |  Envoyer une requête HTTP en mode asynchrone.
publique CancelOperation void (const std::string & requestId)  |  Annuler une opération HTTP spécifique.
CancelAllOperations() void publique  |  Annuler les demandes HTTP en cours.
  
## <a name="members"></a>Membres
  
### <a name="send-function"></a>Send, fonction
Envoyer une requête HTTP.

Paramètres :  
* **demande**: Requête HTTP 


* **contexte**: Le même contexte client opaque qui a été passé à l’API qui a entraîné cette requête HTTP



  
**Retourne**: Conteneur d’opération HTTP
  
### <a name="sendasync-function"></a>SendAsync (fonction)
Envoyer une requête HTTP en mode asynchrone.

Paramètres :  
* **demande**: Requête HTTP 


* **contexte**: Le même contexte client opaque qui a été passé à l’API qui a entraîné cette requête HTTP 


* **callbackFn**: Fonction qui sera exécutée à l’achèvement



  
**Retourne**: Conteneur d’opération HTTP
  
### <a name="canceloperation-function"></a>CancelOperation (fonction)
Annuler une opération HTTP spécifique.

Paramètres :  
* **requestId**: ID de demande d’annulation


  
### <a name="cancelalloperations-function"></a>CancelAllOperations (fonction)
Annuler les demandes HTTP en cours.