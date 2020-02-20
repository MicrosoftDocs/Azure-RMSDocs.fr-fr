---
title: 'MIP :: AuthDelegate :: OAuth2Token, classe'
description: 'Documente la classe MIP :: authdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 6053a282d162dc2b0f316b265fe6878a4c535a7f
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490436"
---
# <a name="class-mipauthdelegateoauth2token"></a>MIP :: AuthDelegate :: OAuth2Token, classe 
Classe contenant les informations de jeton d’accès fournies par une application.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Construisez un nouvel objet OAuth2Token.
public OAuth2Token (const std :: String & accessToken)  |  Construisez un nouvel objet OAuth2Token à partir du jeton d’accès JWT.
public const std :: String & GetAccessToken () const  |  Obtient la chaîne du jeton d’accès.
public void SetAccessToken (const std :: String & accessToken)  |  Définissez la chaîne du jeton d’accès.
public const std :: String & GetErrorMessage () const  |  Obtient le message d’erreur, le cas échéant.
public void SetErrorMessage (const std :: String & errorMessage)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="oauth2token-function"></a>OAuth2Token fonction)
Construisez un nouvel objet OAuth2Token.
  
### <a name="oauth2token-function"></a>OAuth2Token fonction)
Construisez un nouvel objet OAuth2Token à partir du jeton d’accès JWT.

Paramètres :  
* **accessToken**: jeton d’accès JWT.


  
### <a name="getaccesstoken-function"></a>GetAccessToken fonction)
Obtient la chaîne du jeton d’accès.

  
**Retourne**: chaîne de jeton d’accès.
  
### <a name="setaccesstoken-function"></a>SetAccessToken fonction)
Définissez la chaîne du jeton d’accès.

Paramètres :  
* **accessToken**: chaîne de jeton d’accès.


  
### <a name="geterrormessage-function"></a>GetErrorMessage fonction)
Obtient le message d’erreur, le cas échéant.

  
**Retourne**: message d’erreur.
  
### <a name="seterrormessage-function"></a>SetErrorMessage fonction)
Définir le message d’erreur.

Paramètres :  
* **ErrorMessage**: message d’erreur.

