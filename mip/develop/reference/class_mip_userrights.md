---
title: UserRights de classe
description: 'Documente la classe UserRights :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 1a3bf2c6c8f417d30fac24263f672f2603347960
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764248"
---
# <a name="class-userrights"></a>UserRights de classe 
Groupe d’utilisateurs et droits qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRights (const std :: Vector\<std :: String\>& Users, const std ::\<Vector std ::\> String& Rights)  |  Constructeur UserRights.
public const std :: Vector\<std :: String\>& Users () const  |  Obtient les utilisateurs associés à un ensemble de droits.
public const std :: Vector\<std :: String\>& droits () const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userrights-function"></a>UserRights fonction)
Constructeur UserRights.

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes droits 


* **rights** : droits partagés par le groupe d’utilisateurs


  
### <a name="users-function"></a>Fonction utilisateurs
Obtient les utilisateurs associés à un ensemble de droits.

  
**Retourne** : les utilisateurs associés à un ensemble de droits
  
### <a name="rights-function"></a>Fonction Rights
Obtient les droits associés à un groupe d’utilisateurs.

  
**Retourne** : les droits associés à un groupe d’utilisateurs