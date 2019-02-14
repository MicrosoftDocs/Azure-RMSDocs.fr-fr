---
title: classe mip::AuthDelegate::OAuth2Challenge
description: Décrit la classe mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 64a485c30dc6fdb8154c85c3afbd548bbc78ce9a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259406"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>classe mip::AuthDelegate::OAuth2Challenge 
une classe qui contient toutes les informations requises à partir de l’application appelante afin de générer un jeton oauth2.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
OAuth2Challenge public (const std::string & autorité, const std::string & ressource, const std::string & étendue)  |  Construire une nouvelle [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) objet.
public const std::string & GetAuthority() const  |  Obtenir la chaîne d’autorité.
public const std::string & GetResource() const  |  Obtenir la chaîne de ressource.
public const std::string& GetScope() const  |  Obtenir la chaîne de portée.
  
## <a name="members"></a>Membres
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge (fonction)
Construire une nouvelle [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) objet.

Paramètres :  
* **autorité**: l’autorité le jeton doit être généré par rapport. 


* **ressource**: la ressource que le jeton a la valeur. 


* **étendue**: l’étendue que le jeton a la valeur.


  
### <a name="getauthority-function"></a>GetAuthority (fonction)
Obtenir la chaîne d’autorité.

  
**Retourne**: La chaîne d’autorité.
  
### <a name="getresource-function"></a>GetResource (fonction)
Obtenir la chaîne de ressource.

  
**Retourne**: La chaîne de ressource.
  
### <a name="getscope-function"></a>GetScope (fonction)
Obtenir la chaîne de portée.

  
**Retourne**: La chaîne de portée.
