---
title: struct ApplicationInfo
description: Documentation des structures associées au kit de développement logiciel (MIP) Microsoft Information Protection.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 4971d7cf0891308733dafd0dc64d58c02343f1e4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565528"
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