---
title: mip::UserRights, classe
description: Décrit la classe mip::userrights de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2a45f7bc9947984f9189b10bd886a53807b3abdb
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332666"
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
