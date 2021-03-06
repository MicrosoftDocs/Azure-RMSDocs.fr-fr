---
title: 'classe AuthDelegate :: OAuth2Challenge'
description: 'Documente la classe authdelegate :: oauth2challenge du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 3062130037142ebe3b5c227da0dd12a8f38065c1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212074"
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