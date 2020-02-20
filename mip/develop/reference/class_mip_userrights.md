---
title: mip::UserRights, classe
description: 'Documente la classe MIP :: UserRights du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f44ff30c890a5a8ab3dbce2426a6c1898df1f0e5
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489297"
---
# <a name="class-mipuserrights"></a>mip::UserRights, classe 
Groupe d’utilisateurs et droits qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRights (const std :: Vector\<std :: String\>& Users, const std :: Vector\<std :: String\>& Rights)  |  Constructeur UserRights.
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