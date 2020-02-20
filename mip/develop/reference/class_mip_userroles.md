---
title: mip::UserRoles, classe
description: 'Documente la classe MIP :: UserRoles du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d22f66c8fff22b54e5e7e30f425adc2c889e5db0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489280"
---
# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Groupe d’utilisateurs et rôles qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRoles (const std :: Vector\<std :: String\>& Users, const std :: Vector\<std :: String\>& Roles)  |  Constructeur UserRoles.
public const std :: Vector\<std :: String\>& Users () const  |  Obtient les utilisateurs associés à un ensemble de rôles.
public const std :: Vector\<std :: String\>& Roles () const  |  Obtient les rôles associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userroles-function"></a>UserRoles fonction)
Constructeur UserRoles.

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes rôles 


* **roles** : rôles partagés par un groupe d’utilisateurs


  
### <a name="users-function"></a>Fonction utilisateurs
Obtient les utilisateurs associés à un ensemble de rôles.

  
**Retourne** : les utilisateurs associés à un ensemble de rôles
  
### <a name="roles-function"></a>Fonction Roles
Obtient les rôles associés à un groupe d’utilisateurs.

  
**Retourne** : les rôles associés à un groupe d’utilisateurs