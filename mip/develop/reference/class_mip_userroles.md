---
title: mip::UserRoles, classe
description: 'Documente la classe MIP :: UserRoles du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e77ed6ae4d4b5467964f855a081cc22780d9869c
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560458"
---
# <a name="class-mipuserroles"></a>mip::UserRoles, classe 
Groupe d’utilisateurs et rôles qui leur sont associés.
  
## <a name="summary"></a>Table des matières
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