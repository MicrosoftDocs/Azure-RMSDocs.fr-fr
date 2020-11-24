---
title: 'classe AuthDelegate :: OAuth2Token'
description: 'Documente la classe authdelegate :: oauth2token du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a8532e1950977e421fa25b426fa4e4061e610d8d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567263"
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

