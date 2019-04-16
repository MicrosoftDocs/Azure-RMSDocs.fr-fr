---
title: classe mip::Identity
description: Décrit la classe mip::identity de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 75d11fae7d79cadc4dd8909be371cbde2e87f289
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573613"
---
# <a name="class-mipidentity"></a>classe mip::Identity 
Abstraction d’identité.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Identity() ne publique  |  Par défaut [identité](class_mip_identity.md) constructeur utilisé lorsqu’une adresse de messagerie d’utilisateur n’est pas connue.
Identité publique (const Identity & autres)  |  [Identité](class_mip_identity.md) constructeur de copie.
Identité explicite publique (const std::string & e-mail)  |  [Identité](class_mip_identity.md) constructeur utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.
public const std::string & GetEmail() const  |  Obtention de l’e-mail.
public void SetDelegatedEmail(const std::string& delegatedEmail)  |  Définit l’e-mail déléguée, une adresse de messagerie déléguée est agissant pour le compte d’utilisateur pour lequel les opertations sont effectuées.
public const std::string& GetDelegatedEmail() const  |  Obtention de l’e-mail déléguée, une adresse de messagerie déléguée est agissant pour le compte d’utilisateur pour lequel les opertations sont effectuées.
  
## <a name="members"></a>Membres
  
### <a name="identity-function"></a>Fonction d’identité
Par défaut [identité](class_mip_identity.md) constructeur utilisé lorsqu’une adresse de messagerie d’utilisateur n’est pas connue.
  
### <a name="identity-function"></a>Fonction d’identité
[Identité](class_mip_identity.md) constructeur de copie.

Paramètres :  
* **[Identité](class_mip_identity.md)**: permet de créer la copie.


  
### <a name="identity-function"></a>Fonction d’identité
[Identité](class_mip_identity.md) constructeur utilisé lorsqu’une adresse de messagerie d’utilisateur est connue.

Paramètres :  
* **e-mail**: adresse de messagerie d’utilisateur.


  
### <a name="getemail-function"></a>GetEmail (fonction)
Obtention de l’e-mail.

  
**Retourne**: Adresse de messagerie.
  
### <a name="setdelegatedemail-function"></a>SetDelegatedEmail (fonction)
Définit l’e-mail déléguée, une adresse de messagerie déléguée est agissant pour le compte d’utilisateur pour lequel les opertations sont effectuées.

Paramètres :  
* **delegatedEmail**: l’e-mail de délégation.


  
### <a name="getdelegatedemail-function"></a>GetDelegatedEmail (fonction)
Obtention de l’e-mail déléguée, une adresse de messagerie déléguée est agissant pour le compte d’utilisateur pour lequel les opertations sont effectuées.

  
**Retourne**: L’e-mail de délégué.