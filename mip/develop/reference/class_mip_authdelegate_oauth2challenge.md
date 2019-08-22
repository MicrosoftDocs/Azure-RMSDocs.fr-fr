---
title: 'MIP:: AuthDelegate:: OAuth2Challenge, classe'
description: 'Documente la classe MIP:: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 836704d51d1afa55bc296681c863ee10a072ea79
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885911"
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