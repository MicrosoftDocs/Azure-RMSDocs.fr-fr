---
title: mip::UserRoles, classe
description: Décrit la classe mip::userroles de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 45b2b5170fac04364af1a0418da5d6e1f5e488a3
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56260049"
---
# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Groupe d’utilisateurs et rôles qui leur sont associés.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector\<std::string\>& users, const std::vector\<std::string\>& roles)  |  Constructeur [UserRoles](class_mip_userroles.md).
public const std::vector\<std::string\>& Users() const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public const std::vector\<std::string\>& Roles() const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles-function"></a>Rôles d’utilisateur (fonction)
Constructeur [UserRoles](class_mip_userroles.md).

Paramètres :  
* **les utilisateurs**: Groupe d’utilisateurs qui partagent les mêmes rôles 


* **rôles**: Rôles partagés par un groupe d’utilisateurs


  
### <a name="users-function"></a>Fonction d’utilisateurs
Obtient les utilisateurs associés à un ensemble de rôles.

  
**Retourne**: Utilisateurs associés à un ensemble de rôles
  
### <a name="roles-function"></a>Fonction de rôles
Obtient les rôles associés à un groupe d’utilisateurs.

  
**Retourne**: Rôles associés à un groupe d’utilisateurs
