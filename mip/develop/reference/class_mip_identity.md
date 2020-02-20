---
title: 'MIP :: Identity, classe'
description: 'Documente la classe MIP :: Identity du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d50092be5277d5e88e6ec408280ca76bbc333a4c
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488022"
---
# <a name="class-mipidentity"></a>MIP :: Identity, classe 
Abstraction pour l’identité.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Identité publique ()  |  Constructeur d’identité par défaut utilisé lorsqu’une adresse de messagerie utilisateur n’est pas connue.
Identité publique (const Identity & Other)  |  Constructeur de copie d’identité.
public Explicit Identity (const std :: String & email)  |  Constructeur d’identité utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.
public Explicit Identity (const std :: String & e-mail, const std :: String & name)  |  Constructeur d’identité utilisé lorsqu’une adresse de messagerie utilisateur et un nom d’utilisateur sont connus.
public const std :: String & GetEmail () const  |  Recevez le message électronique.
public const std::string& GetName() const  |  Obtient le nom convivial de l’utilisateur. utilisé pour le marquage de texte.
  
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
* **adresse de messagerie : doit**être une adresse e-mail valide.


  
### <a name="identity-function"></a>Identity (fonction)
Constructeur d’identité utilisé lorsqu’une adresse de messagerie utilisateur et un nom d’utilisateur sont connus.

Paramètres :  
* **adresse de messagerie : doit**être une adresse e-mail valide. 


* **nom**: nom d’utilisateur.


  
### <a name="getemail-function"></a>GetEmail fonction)
Recevez le message électronique.

  
**Retourne**: l’e-mail.
  
### <a name="getname-function"></a>Fonction GetName
Obtient le nom convivial de l’utilisateur. utilisé pour le marquage de texte.

  
**Retourne**: nom convivial.