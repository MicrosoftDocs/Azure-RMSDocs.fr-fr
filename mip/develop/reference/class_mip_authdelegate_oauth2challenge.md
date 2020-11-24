---
title: 'classe AuthDelegate :: OAuth2Challenge'
description: 'Documente la classe authdelegate :: oauth2challenge du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: f422b99674213904316eab622bfc915f128228ec
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567270"
---
# <a name="class-authdelegateoauth2challenge"></a>classe AuthDelegate :: OAuth2Challenge 
classe qui contient toutes les informations requises de l’application appelante afin de générer un jeton oauth2.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std :: String& autorité, const std :: String& ressource, const std :: String& portée, const std :: String& les revendications)  |  Construisez un nouvel objet OAuth2Challenge.
public const std :: String& GetAuthority () const  |  Obtient la chaîne d’autorité.
public const std :: String& GetResource () const  |  Obtient la chaîne de ressource.
public const std :: String& GetScope, () const  |  Obtient la chaîne de portée.
public const std :: String& GetClaims () const  |  Obtient la chaîne de revendications.
  
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