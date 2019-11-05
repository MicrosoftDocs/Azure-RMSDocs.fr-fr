---
title: 'MIP :: AuthDelegate :: OAuth2Challenge, classe'
description: 'Documente la classe MIP :: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8205d207a48d90832b5961b14d37c7a7226293a2
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559016"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>MIP :: AuthDelegate :: OAuth2Challenge, classe 
classe qui contient toutes les informations requises de l’application appelante afin de générer un jeton oauth2.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std :: String & autorité, const std :: String & ressource, const std :: String & portée, const std :: String & les revendications)  |  Construisez un nouvel objet OAuth2Challenge.
public const std :: String & GetAuthority () const  |  Obtient la chaîne d’autorité.
public const std :: String & GetResource () const  |  Obtient la chaîne de ressource.
public const std :: String & GetScope, () const  |  Obtient la chaîne de portée.
public const std :: String & GetClaims () const  |  Obtient la chaîne de revendications.
  
## <a name="members"></a>Membres
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge fonction)
Construisez un nouvel objet OAuth2Challenge.

Paramètres :  
* **Authority**: autorité sur laquelle le jeton doit être généré. 


* **ressource**: la ressource à laquelle le jeton est défini. 


* **portée**: étendue à laquelle le jeton a la valeur.


  
### <a name="getauthority-function"></a>GetAuthority fonction)
Obtient la chaîne d’autorité.

  
**Retourne**: chaîne d’autorité.
  
### <a name="getresource-function"></a>GetResource, fonction
Obtient la chaîne de ressource.

  
**Retourne**: la chaîne de ressource.
  
### <a name="getscope-function"></a>GetScope, fonction)
Obtient la chaîne de portée.

  
**Retourne**: la chaîne de portée.
  
### <a name="getclaims-function"></a>GetClaims fonction)
Obtient la chaîne de revendications.

  
**Retourne**: chaîne de revendications.