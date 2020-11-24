---
title: UserRoles de classe
description: 'Documente la classe UserRoles :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: fc6e5f77c68ecde2582cfd622624c0c6b986500b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565573"
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