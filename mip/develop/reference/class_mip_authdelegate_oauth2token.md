---
title: 'MIP :: AuthDelegate :: OAuth2Token, classe'
description: 'Documente la classe MIP :: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d8bce56e02778d48e6e3c0cfdb02f1c3f1f4054a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560344"
---
# <a name="class-mipauthdelegateoauth2token"></a>MIP :: AuthDelegate :: OAuth2Token, classe 
Classe définissant comment le kit de développement logiciel MIP s’attend à ce que le jeton oauth2 soit renvoyé dans le kit de développement logiciel (SDK).
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Construisez un nouvel objet OAuth2Token.
public OAuth2Token (const std :: String & accessToken)  |  Construit un nouvel objet OAuth2Token à partir d’un accessToken.
public const std :: String & GetAccessToken () const  |  Obtient la chaîne du jeton d’accès.
public void SetAccessToken (const std :: String & accessToken)  |  Définissez la chaîne du jeton d’accès.
  
## <a name="members"></a>Membres
  
### <a name="oauth2token-function"></a>OAuth2Token fonction)
Construisez un nouvel objet OAuth2Token.
  
### <a name="oauth2token-function"></a>OAuth2Token fonction)
Construit un nouvel objet OAuth2Token à partir d’un accessToken.

Paramètres :  
* **accessToken**: le jeton d’accès réel passé dans le kit de développement logiciel (SDK).


  
### <a name="getaccesstoken-function"></a>GetAccessToken fonction)
Obtient la chaîne du jeton d’accès.

  
**Retourne**: la chaîne du jeton d’accès.
  
### <a name="setaccesstoken-function"></a>SetAccessToken fonction)
Définissez la chaîne du jeton d’accès.

Paramètres :  
* **accessToken**: chaîne de jeton d’accès.

