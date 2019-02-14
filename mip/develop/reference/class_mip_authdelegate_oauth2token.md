---
title: classe mip::AuthDelegate::OAuth2Token
description: Décrit la classe mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: bef28489d16b040ff910103d9e0bf5a4719c66ff
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255969"
---
# <a name="class-mipauthdelegateoauth2token"></a>classe mip::AuthDelegate::OAuth2Token 
Classe définissant comment le SDK MIP attend le jeton oauth2 à passer dans le Kit de développement.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Token()  |  Construire une nouvelle [OAuth2Token](class_mip_authdelegate_oauth2token.md) objet.
OAuth2Token public (const std::string & accessToken)  |  Construire une nouvelle [OAuth2Token](class_mip_authdelegate_oauth2token.md) objet à partir d’un accessToken.
public const std::string & GetAccessToken() const  |  Obtenir la chaîne de jeton d’accès.
public SetAccessToken void (const std::string & accessToken)  |  Définir la chaîne de jeton d’accès.
  
## <a name="members"></a>Membres
  
### <a name="oauth2token-function"></a>OAuth2Token (fonction)
Construire une nouvelle [OAuth2Token](class_mip_authdelegate_oauth2token.md) objet.
  
### <a name="oauth2token-function"></a>OAuth2Token (fonction)
Construire une nouvelle [OAuth2Token](class_mip_authdelegate_oauth2token.md) objet à partir d’un accessToken.

Paramètres :  
* **accessToken**: Le jeton d’accès réel passé dans le Kit de développement.


  
### <a name="getaccesstoken-function"></a>GetAccessToken (fonction)
Obtenir la chaîne de jeton d’accès.

  
**Retourne**: La chaîne de jeton d’accès.
  
### <a name="setaccesstoken-function"></a>SetAccessToken (fonction)
Définir la chaîne de jeton d’accès.

Paramètres :  
* **accessToken**: la chaîne de jeton d’accès.

