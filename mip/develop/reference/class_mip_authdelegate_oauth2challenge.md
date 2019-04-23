---
title: classe mip::AuthDelegate::OAuth2Challenge
description: Décrit la classe mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d404d6f60e7b2472bc97181b45fae3b4dabc387b
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173471"
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