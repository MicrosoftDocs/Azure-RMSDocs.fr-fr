---
title: mip::UserRoles, classe
description: 'Documente la classe MIP:: UserRoles du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: c674882145e5c47233224f470d3b038bca9a40b7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882810"
---
# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Groupe d’utilisateurs et rôles qui leur sont associés.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: Vector\<std:: String\>& Users, const std::\<Vector std::\>String & Roles)  |  Constructeur [UserRoles](class_mip_userroles.md).
public const std:: Vector\<std:: String\>& Users () const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public const std:: Vector\<std:: String\>& Roles () const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles-function"></a>UserRoles fonction)
Constructeur [UserRoles](class_mip_userroles.md).

Paramètres :  
* **utilisateurs**: Groupe d’utilisateurs qui partagent les mêmes rôles 


* **rôles**: Rôles partagés par groupe d’utilisateurs


  
### <a name="users-function"></a>Fonction utilisateurs
Obtient les utilisateurs associés à un ensemble de rôles.

  
**Retourne**: Utilisateurs associés à un ensemble de rôles
  
### <a name="roles-function"></a>Fonction Roles
Obtient les rôles associés à un groupe d’utilisateurs.

  
**Retourne**: Rôles associés à un groupe d’utilisateurs