---
title: 'MIP:: Identity, classe'
description: 'Documente la classe MIP:: Identity du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: d2fefceb87a1bab042fc8b0aeb817421cd9025f1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885557"
---
# <a name="class-mipidentity"></a>MIP:: Identity, classe 
Abstraction pour l’identité.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Identité publique ()  |  Constructeur d' [identité](class_mip_identity.md) par défaut utilisé lorsqu’une adresse de messagerie utilisateur n’est pas connue.
Identité publique (const Identity & Other)  |  Constructeur de copie d' [identité](class_mip_identity.md) .
public Explicit Identity (const std:: String & email)  |  Constructeur d' [identité](class_mip_identity.md) utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.
public const std:: String & GetEmail () const  |  Recevez le message électronique.
  
## <a name="members"></a>Membres
  
### <a name="identity-function"></a>Identity (fonction)
Constructeur d' [identité](class_mip_identity.md) par défaut utilisé lorsqu’une adresse de messagerie utilisateur n’est pas connue.
  
### <a name="identity-function"></a>Identity (fonction)
Constructeur de copie d' [identité](class_mip_identity.md) .

Paramètres :  
* **[Identity](class_mip_identity.md)** : utilisé pour créer la copie.


  
### <a name="identity-function"></a>Identity (fonction)
Constructeur d' [identité](class_mip_identity.md) utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.

Paramètres :  
* **e-mail**: adresse de messagerie de l’utilisateur.


  
### <a name="getemail-function"></a>GetEmail fonction)
Recevez le message électronique.

  
**Retourne**: E-mail.