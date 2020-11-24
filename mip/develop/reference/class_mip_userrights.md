---
title: UserRights de classe
description: 'Documente la classe UserRights :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 37943d284eaa00524797605158e320c25e52e17b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567390"
---
# <a name="class-userrights"></a>UserRights de classe 
Groupe d’utilisateurs et droits qui leur sont associés.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public UserRights (const std :: Vector \<std::string\>& Users, const std :: vector \<std::string\>& Rights)  |  Constructeur UserRights.
public const std :: Vector \<std::string\>& Users () const  |  Obtient les utilisateurs associés à un ensemble de droits.
public const std :: Vector \<std::string\>& droits () const  |  Obtient les droits associés à un groupe d’utilisateurs.
  
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