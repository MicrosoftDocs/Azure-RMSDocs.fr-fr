---
title: Identité de la classe
description: 'Documente la classe Identity :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d1ec599e486466a1e5016025d1c5e04ae09e64ee
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215236"
---
# <a name="class-identity"></a>Identité de la classe 
Abstraction pour l’identité.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Identité publique ()  |  Constructeur d’identité par défaut utilisé lorsqu’une adresse de messagerie utilisateur n’est pas connue.
Identité publique (const Identity& other)  |  Constructeur de copie d’identité.
public Explicit Identity (const std :: String& email)  |  Constructeur d’identité utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.
public Explicit Identity (const std :: String& e-mail, const std :: String& Name)  |  Constructeur d’identité utilisé lorsqu’une adresse de messagerie utilisateur et un nom d’utilisateur sont connus.
public const std :: String& GetEmail () const  |  Recevez le message électronique.
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
* **adresse de messagerie : doit** être une adresse e-mail valide.


  
### <a name="identity-function"></a>Identity (fonction)
Constructeur d’identité utilisé lorsqu’une adresse de messagerie utilisateur et un nom d’utilisateur sont connus.

Paramètres :  
* **adresse de messagerie : doit** être une adresse e-mail valide. 


* **nom**: nom d’utilisateur.


  
### <a name="getemail-function"></a>GetEmail fonction)
Recevez le message électronique.

  
**Retourne**: l’e-mail.
  
### <a name="getname-function"></a>Fonction GetName
Obtient le nom convivial de l’utilisateur. utilisé pour le marquage de texte.

  
**Retourne**: nom convivial.