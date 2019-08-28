---
title: 'MIP:: AuthDelegate:: OAuth2Token, classe'
description: 'Documente la classe MIP:: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 93c73f632410bf6b1c6898746d1fcbd2c4f67e72
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056250"
---
# <a name="class-mipauthdelegateoauth2token"></a>MIP:: AuthDelegate:: OAuth2Token, classe 
Classe définissant comment le kit de développement logiciel MIP s’attend à ce que le jeton oauth2 soit renvoyé dans le kit de développement logiciel (SDK).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Construisez un nouvel objet [OAuth2Token](class_mip_authdelegate_oauth2token.md) .
public OAuth2Token (const std:: String & accessToken)  |  Construit un nouvel objet [OAuth2Token](class_mip_authdelegate_oauth2token.md) à partir d’un accessToken.
public const std:: String & GetAccessToken () const  |  Obtient la chaîne du jeton d’accès.
public void SetAccessToken (const std:: String & accessToken)  |  Définissez la chaîne du jeton d’accès.
  
## <a name="members"></a>Membres
  
### <a name="oauth2token-function"></a>OAuth2Token fonction)
Construisez un nouvel objet [OAuth2Token](class_mip_authdelegate_oauth2token.md) .
  
### <a name="oauth2token-function"></a>OAuth2Token fonction)
Construit un nouvel objet [OAuth2Token](class_mip_authdelegate_oauth2token.md) à partir d’un accessToken.

Paramètres :  
* **accessToken**: Le jeton d’accès réel passé dans le kit de développement logiciel (SDK).


  
### <a name="getaccesstoken-function"></a>GetAccessToken fonction)
Obtient la chaîne du jeton d’accès.

  
**Retourne**: Chaîne du jeton d’accès.
  
### <a name="setaccesstoken-function"></a>SetAccessToken fonction)
Définissez la chaîne du jeton d’accès.

Paramètres :  
* **accessToken**: chaîne de jeton d’accès.

