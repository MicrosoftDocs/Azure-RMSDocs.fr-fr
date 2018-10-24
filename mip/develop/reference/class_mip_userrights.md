---
title: mip UserRights, classe
description: Informations de référence pour la classe mip UserRights
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c1ef7aaba00bf595d80f07f318aa5808f3a56409
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445119"
---
# <a name="class-mipuserrights"></a>mip::UserRights, classe 
Groupe d’utilisateurs et droits qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRights(const std::vector<std::string>& users, const std::vector<std::string>& rights)  |  Constructeur [UserRights](class_mip_userrights.md).
public const std::vector<std::string>& Users() const  |  Obtient les utilisateurs associés à un ensemble de droits.
public const std::vector<std::string>& Rights() const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userrights"></a>UserRights
Constructeur [UserRights](class_mip_userrights.md).

Paramètres :  
* **users** : groupe d’utilisateurs qui partagent les mêmes droits 


* **rights** : droits partagés par le groupe d’utilisateurs


  
### <a name="users"></a>Utilisateurs
Obtient les utilisateurs associés à un ensemble de droits.

  
**Retourne** : les utilisateurs associés à un ensemble de droits
  
### <a name="rights"></a>Droits
Obtient les droits associés à un groupe d’utilisateurs.

  
**Retourne** : les droits associés à un groupe d’utilisateurs