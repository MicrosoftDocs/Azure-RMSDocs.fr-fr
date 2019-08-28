---
title: 'MIP:: AuthDelegate:: OAuth2Challenge, classe'
description: 'Documente la classe MIP:: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2e96fb769a1b917715daa872736c6d2b81e2626e
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055427"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>MIP:: AuthDelegate:: OAuth2Challenge, classe 
classe qui contient toutes les informations requises de l’application appelante afin de générer un jeton oauth2.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std:: String & autorité, const std:: String & ressource, const std:: String & portée, const std:: String & les revendications)  |  Construisez un nouvel objet [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) .
public const std:: String & GetAuthority () const  |  Obtient la chaîne d’autorité.
public const std:: String & GetResource () const  |  Obtient la chaîne de ressource.
public const std:: String & GetScope, () const  |  Obtient la chaîne de portée.
public const std:: String & GetClaims () const  |  Obtient la chaîne de revendications.
  
## <a name="members"></a>Membres
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge fonction)
Construisez un nouvel objet [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) .

Paramètres :  
* **Authority**: autorité sur laquelle le jeton doit être généré. 


* **ressource**: la ressource à laquelle le jeton est défini. 


* **portée**: étendue à laquelle le jeton a la valeur.


  
### <a name="getauthority-function"></a>GetAuthority fonction)
Obtient la chaîne d’autorité.

  
**Retourne**: Chaîne d’autorité.
  
### <a name="getresource-function"></a>GetResource, fonction
Obtient la chaîne de ressource.

  
**Retourne**: Chaîne de ressource.
  
### <a name="getscope-function"></a>GetScope, fonction)
Obtient la chaîne de portée.

  
**Retourne**: Chaîne de portée.
  
### <a name="getclaims-function"></a>GetClaims fonction)
Obtient la chaîne de revendications.

  
**Retourne**: Chaîne de revendications.