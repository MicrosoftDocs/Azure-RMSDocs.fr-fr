---
title: 'classe AuthDelegate :: OAuth2Token'
description: 'Documente la classe authdelegate :: oauth2token du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 4db3d2fbb2299b30b85516047ec237d2f23d7cd9
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212040"
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

