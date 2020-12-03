---
title: struct ApplicationInfo
description: Documente la structure ApplicationInfo
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d56fdcaccf67f46b2d6632ec6586e2b140717696
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535584"
---
# <a name="struct-applicationinfo"></a>struct ApplicationInfo 
Struct qui inclut des informations spécifiques à l’application.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificateur d’application tel qu’il est défini dans le portail AAD, (doit être un GUID sans crochets).
public std::string applicationName  |  Nom de l’application, (doit contenir uniquement des caractères ASCII valides, à l’exception de « ; »)
public std::string applicationVersion  |  Version de l’application utilisée, (ne doit contenir que des caractères ASCII valides, à l’exclusion de « ; »)
  
## <a name="members"></a>Membres
  
### <a name="applicationid-struct-member"></a>applicationId, membre de struct
Identificateur d’application tel qu’il est défini dans le portail AAD, (doit être un GUID sans crochets).
  
### <a name="applicationname-struct-member"></a>applicationName, membre struct
Nom de l’application, (doit contenir uniquement des caractères ASCII valides, à l’exception de « ; »)
  
### <a name="applicationversion-struct-member"></a>applicationVersion, membre de struct
Version de l’application utilisée, (ne doit contenir que des caractères ASCII valides, à l’exclusion de « ; »)