---
title: mip::UserRoles, classe
description: Décrit la classe mip::userroles de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 1a060652ea61ed452867bb67d281c9531f4e1b98
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651511"
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