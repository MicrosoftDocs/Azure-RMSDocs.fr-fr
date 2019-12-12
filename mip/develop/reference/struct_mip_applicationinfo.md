---
title: 'MIP, struct :: ApplicationInfo'
description: Documentation des structures associées au kit de développement logiciel (MIP) Microsoft Information Protection.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6bee61bc72de35aeaefd9ef1e7639450392b70a7
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73567423"
---
# <a name="struct-mipapplicationinfo"></a>MIP, struct :: ApplicationInfo 
Struct qui inclut des informations spécifiques à l’application.
  
## <a name="summary"></a>Table des matières
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