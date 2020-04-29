---
title: UserRoles de classe
description: 'Documente la classe UserRoles :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: bbff817578bb5ba1fe143c850632e25df8f78708
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764203"
---
# <a name="class-userroles"></a>UserRoles de classe 
Groupe d’utilisateurs et rôles qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRoles (const std :: Vector\<std :: String\>& Users, const std ::\<Vector std ::\> String& Roles)  |  Constructeur UserRoles.
public const std :: Vector\<std :: String\>& Users () const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public const std :: Vector\<std :: String\>& Roles () const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
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