---
title: 'classe AuthDelegate :: OAuth2Token'
description: 'Documente la classe authdelegate :: oauth2token du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 43f3e3d9abdab37620ca852411b2817a3848ba78
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763592"
---
# <a name="class-authdelegateoauth2token"></a>classe AuthDelegate :: OAuth2Token 
Classe contenant les informations de jeton d’accès fournies par une application.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  Construisez un nouvel objet OAuth2Token.
public OAuth2Token (const std :: String& accessToken)  |  Construisez un nouvel objet OAuth2Token à partir du jeton d’accès JWT.
public const std :: String& GetAccessToken () const  |  Obtient la chaîne du jeton d’accès.
public void SetAccessToken (const std :: String& accessToken)  |  Définissez la chaîne du jeton d’accès.
public const std :: String& GetErrorMessage () const  |  Obtient le message d’erreur, le cas échéant.
public void SetErrorMessage (const std :: String& errorMessage)  |  Définir le message d’erreur.
  
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

