---
title: EventProperty de classe
description: 'Documente la classe EventProperty :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 5ee28e454aa5d7854c572df8ef6e4642482c1104
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224963"
---
# <a name="class-eventproperty"></a>EventProperty de classe 
Propriété d’audit/de télémétrie unique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public EventPropertyType GetPropertyType () const  |  Obtient le type de données sous-jacent pour cette propriété.
public const std::string& GetName() const  |  Obtient le nom de la propriété.
GetPii PII public () const  |  Obtient la classification des informations d’identification personnelle (PII), le cas échéant.
public bool IsAuditOnly () const  |  Obtient une valeur indiquant si cette propriété est limitée au pipeline d’audit.
constante double GetDouble () publique  |  Obtient la valeur de la propriété (double)
public int64_t GetInt64 () const  |  Obtient la valeur de la propriété (Int64)
public const std :: String& GetString () const  |  Obtient la valeur de la propriété (String)
  
## <a name="members"></a>Membres
  
### <a name="getpropertytype-function"></a>GetPropertyType fonction)
Obtient le type de données sous-jacent pour cette propriété.

  
**Retourne**: type de données sous-jacent
  
### <a name="getname-function"></a>Fonction GetName
Obtient le nom de la propriété.

  
**Retourne**: nom de la propriété
  
### <a name="getpii-function"></a>GetPii fonction)
Obtient la classification des informations d’identification personnelle (PII), le cas échéant.

  
**Retourne**: classification PII
  
### <a name="isauditonly-function"></a>IsAuditOnly fonction)
Obtient une valeur indiquant si cette propriété est limitée au pipeline d’audit.

  
**Retourne**: que ces propriétés soient ou non limitées au pipeline d’audit si la valeur est true, la propriété contient des informations sensibles et ne doit pas être écrite dans des journaux de fichiers ou dans un pipeline à l’exception de l’audit jusqu’à ce qu’elle soit nettoyée manuellement.
  
### <a name="getdouble-function"></a>GetDouble, fonction
Obtient la valeur de la propriété (double)

  
**Retourne**: valeur de propriété
  
### <a name="getint64-function"></a>GetInt64, fonction
Obtient la valeur de la propriété (Int64)

  
**Retourne**: valeur de propriété
  
### <a name="getstring-function"></a>GetString, fonction
Obtient la valeur de la propriété (String)

  
**Retourne**: valeur de propriété