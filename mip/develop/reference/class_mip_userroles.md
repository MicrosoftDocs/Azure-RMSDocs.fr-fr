---
title: UserRoles de classe
description: 'Documente la classe UserRoles :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: ef881f184fd370665006c8fb4d73138b7c5e2f3c
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214131"
---
# <a name="class-userroles"></a>UserRoles de classe 
Groupe d’utilisateurs et rôles qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRoles (const std :: Vector \<std::string\>& Users, const std :: vector \<std::string\>& Roles)  |  Constructeur UserRoles.
public const std :: Vector \<std::string\>& Users () const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public const std :: Vector \<std::string\>& Roles () const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles-function"></a>UserRoles fonction)
Constructeur UserRoles.

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes rôles 


* **rôles**: rôles partagés par groupe d’utilisateurs


  
### <a name="users-function"></a>Fonction utilisateurs
Obtient les utilisateurs associés à un ensemble de rôles.

  
**Retourne** : les utilisateurs associés à un ensemble de rôles
  
### <a name="roles-function"></a>Fonction Roles
Obtient les rôles associés à un groupe d’utilisateurs.

  
**Retourne**: rôles associés à un groupe d’utilisateurs