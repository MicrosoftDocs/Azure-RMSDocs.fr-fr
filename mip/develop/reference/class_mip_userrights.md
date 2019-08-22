---
title: mip::UserRights, classe
description: 'Documente la classe MIP:: UserRights du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: c26c7d1aa31cf8fb2ea562582a2ebaad8417615d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884975"
---
# <a name="class-mipuserrights"></a>mip::UserRights, classe 
Groupe d’utilisateurs et droits qui leur sont associés.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRights (const std:: Vector\<std:: String\>& Users, const std::\<Vector std::\>String & Rights)  |  Constructeur [UserRights](class_mip_userrights.md).
public const std:: Vector\<std:: String\>& Users () const  |  Obtient les utilisateurs associés à un ensemble de droits.
public const std:: Vector\<std:: String\>& droits () const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
## <a name="members"></a>Membres
  
### <a name="userrights-function"></a>UserRights fonction)
Constructeur [UserRights](class_mip_userrights.md).

Paramètres :  
* **utilisateurs**: Groupe d’utilisateurs qui partagent les mêmes droits 


* **droits**: Droits partagés par groupe d’utilisateurs


  
### <a name="users-function"></a>Fonction utilisateurs
Obtient les utilisateurs associés à un ensemble de droits.

  
**Retourne**: Utilisateurs associés à un ensemble de droits
  
### <a name="rights-function"></a>Fonction Rights
Obtient les droits associés à un groupe d’utilisateurs.

  
**Retourne**: Droits associés à un groupe d’utilisateurs