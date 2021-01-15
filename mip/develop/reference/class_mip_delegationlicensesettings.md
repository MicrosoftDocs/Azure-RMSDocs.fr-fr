---
title: DelegationLicenseSettings de classe
description: 'Documente la classe delegationlicensesettings :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 947accd8104f8eda9f7b7320a1fbdb956810f34d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224923"
---
# <a name="class-delegationlicensesettings"></a>DelegationLicenseSettings de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr \<const PublishingLicenseInfo\> GetLicenseInfo () const  |  Obtient le PublishingLicenseInfo, la licence de publication.
public const std :: Vector \<std::string\>& GetUsers () const  |  Obtient la liste des utilisateurs de la requête.
public bool GetAquireEndUserLicenses () const  |  Obtient la valeur booléenne qui indique s’il faut ou non obtenir la licence de l’utilisateur final en plus de la licence du délégué.
  
## <a name="members"></a>Membres
  
### <a name="getlicenseinfo-function"></a>GetLicenseInfo fonction)
Obtient le PublishingLicenseInfo, la licence de publication.

  
**Retourne**: PublishingLicenseInfo
  
### <a name="getusers-function"></a>GetUsers fonction)
Obtient la liste des utilisateurs de la requête.

  
**Retourne**: les utilisateurs
  
### <a name="getaquireenduserlicenses-function"></a>GetAquireEndUserLicenses fonction)
Obtient la valeur booléenne qui indique s’il faut ou non obtenir la licence de l’utilisateur final en plus de la licence du délégué.

  
**Retourne**: indique s’il faut acquérir des licences utilisateur final