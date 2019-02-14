---
title: mip::UserRights, classe
description: Décrit la classe mip::userrights de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: aadf12606f74d508ba3ebdc1ce0770febd49e142
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251298"
---
# <a name="class-mipuserrights"></a>mip::UserRights, classe 
Groupe d’utilisateurs et droits qui leur sont associés.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
UserRights public (const std::vector\<std::string\>& users, const std::vector\<std::string\>& rights)  |  Constructeur [UserRights](class_mip_userrights.md).
public const std::vector\<std::string\>& Users() const  |  Obtient les utilisateurs associés à un ensemble de droits.
public const std::vector\<std::string\>& Rights() const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userrights-function"></a>UserRights (fonction)
Constructeur [UserRights](class_mip_userrights.md).

Paramètres :  
* **les utilisateurs**: Groupe d’utilisateurs qui partagent les mêmes droits 


* **droits**: Droits partagés par un groupe d’utilisateurs


  
### <a name="users-function"></a>Fonction d’utilisateurs
Obtient les utilisateurs associés à un ensemble de droits.

  
**Retourne**: Utilisateurs associés à un ensemble de droits
  
### <a name="rights-function"></a>Droits (fonction)
Obtient les droits associés à un groupe d’utilisateurs.

  
**Retourne**: Droits associés à un groupe d’utilisateurs
