---
title: mip UserRoles, classe
description: Informations de référence pour la classe mip UserRoles
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 1cc1da6f443fa22095f216bb2ec2f0e51e75bf78
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445255"
---
# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Groupe d’utilisateurs et rôles qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector<std::string>& users, const std::vector<std::string>& roles)  |  Constructeur [UserRoles](class_mip_userroles.md).
public const std::vector<std::string>& Users() const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public const std::vector<std::string>& Roles() const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles"></a>UserRoles
Constructeur [UserRoles](class_mip_userroles.md).

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes rôles 


* **roles** : rôles partagés par un groupe d’utilisateurs


  
### <a name="users"></a>Utilisateurs
Obtient les utilisateurs associés à un ensemble de rôles.

  
**Retourne** : les utilisateurs associés à un ensemble de rôles
  
### <a name="roles"></a>Rôles
Obtient les rôles associés à un groupe d’utilisateurs.

  
**Retourne** : les rôles associés à un groupe d’utilisateurs