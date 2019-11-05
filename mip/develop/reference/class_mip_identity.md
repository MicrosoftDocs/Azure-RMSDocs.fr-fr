---
title: 'MIP :: Identity, classe'
description: 'Documente la classe MIP :: Identity du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 633a0ac8536f7bbd285eee67934f27d65b399bf4
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560158"
---
# <a name="class-mipidentity"></a>MIP :: Identity, classe 
Abstraction pour l’identité.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Identité publique ()  |  Constructeur d’identité par défaut utilisé lorsqu’une adresse de messagerie utilisateur n’est pas connue.
Identité publique (const Identity & Other)  |  Constructeur de copie d’identité.
public Explicit Identity (const std :: String & email)  |  Constructeur d’identité utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.
public const std :: String & GetEmail () const  |  Recevez le message électronique.
  
## <a name="members"></a>Membres
  
### <a name="identity-function"></a>Identity (fonction)
Constructeur d’identité par défaut utilisé lorsqu’une adresse de messagerie utilisateur n’est pas connue.
  
### <a name="identity-function"></a>Identity (fonction)
Constructeur de copie d’identité.

Paramètres :  
* **Identity**: utilisé pour créer la copie.


  
### <a name="identity-function"></a>Identity (fonction)
Constructeur d’identité utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.

Paramètres :  
* **e-mail**: adresse de messagerie de l’utilisateur.


  
### <a name="getemail-function"></a>GetEmail fonction)
Recevez le message électronique.

  
**Retourne**: l’e-mail.