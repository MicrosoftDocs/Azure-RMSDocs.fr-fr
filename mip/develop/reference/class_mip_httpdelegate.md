---
title: mip::HttpDelegate, classe
description: 'Documente la classe MIP:: httpdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f5f5bc13f3c01e40b0034d4fae1bd698da8426c5
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054883"
---
# <a name="class-miphttpdelegate"></a>mip::HttpDelegate, classe 
Interface pour le remplacement de la gestion HTTP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std:: shared_ptr\<HttpRequest\>& request, const std:: shared_ptr\<void\>& Context)  |  Envoyer une requête HTTP.
public std:: shared_ptr\<HttpOperation\> SendAsync (const std:: shared_ptr\<HttpRequest\>& demande, const std:: shared_ptr\<void\>& contexte, const std:: fonction\<void (std:: shared_ptr\<HttpOperation\>)\>& callbackFn)  |  Envoyer une requête HTTP de manière asynchrone.
public void CancelOperation (const std:: String & requestId)  |  Annule une opération HTTP spécifique.
public void CancelAllOperations ()  |  Annuler les requêtes HTTP en cours.
  
## <a name="members"></a>Membres
  
### <a name="send-function"></a>Send, fonction
Envoyer une requête HTTP.

Paramètres :  
* **demande**: Requête HTTP 


* **contexte**: Le même contexte de client opaque qui a été passé à l’API qui a entraîné cette requête HTTP



  
**Retourne**: Conteneur d’opération HTTP
  
### <a name="sendasync-function"></a>SendAsync, fonction
Envoyer une requête HTTP de manière asynchrone.

Paramètres :  
* **demande**: Requête HTTP 


* **contexte**: Le même contexte de client opaque qui a été passé à l’API qui a entraîné cette requête HTTP 


* **callbackFn**: Fonction qui sera exécutée à la fin



  
**Retourne**: Conteneur d’opération HTTP
  
### <a name="canceloperation-function"></a>CancelOperation fonction)
Annule une opération HTTP spécifique.

Paramètres :  
* **ID**de la: ID de la demande d’annulation


  
### <a name="cancelalloperations-function"></a>CancelAllOperations fonction)
Annuler les requêtes HTTP en cours.