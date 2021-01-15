---
title: TelemetryEvent de classe
description: 'Documente la classe telemetryevent :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8776eff24a889a1132fc71d11c38b02c49822263
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224949"
---
# <a name="class-telemetryevent"></a>TelemetryEvent de classe 
Événement de télémétrie unique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Obtient le nom de l’événement.
public EventLevel GetLevel () const  |  Obtient le niveau d’événement, indiquant s’il est considéré comme les données de service nécessaires (NSD) ou non.
public const std :: Chrono :: steady_clock :: time_point& GetStartTime () const  |  Obtient l’heure de début de l’événement.
public void AddProperty (const std :: shared_ptr \<EventProperty\>& prop)  |  Ajoutez une propriété à l’événement.
public void AddProperty (const std :: String& Name, bool value)  |  Ajoutez une propriété bool à l’événement.
public void AddProperty (const std :: String& Name, double value, PII PII)  |  Ajoutez une propriété double à l’événement.
public void AddProperty (const std :: String& Name, int64_t value, PII PII)  |  Ajoutez une propriété Int64 à l’événement.
public void AddProperty (const std :: String& nom, const std :: String& value, PII PII)  |  Ajoutez une propriété de type chaîne à l’événement.
public void AddAuditOnlyProperty (const std :: String& nom, const std :: String& value)  |  Ajoutez une propriété de chaîne d’audit uniquement à l’événement.
public std :: Vector \<std::shared_ptr\<EventProperty\> \> GetProperties () const  |  Obtient toutes les propriétés d’événement.
public std :: shared_ptr \<EventProperty\> GetProperty (const std :: string& Name)  |  Obtient la propriété portant le nom donné, le cas échéant.
  
## <a name="members"></a>Membres
  
### <a name="getname-function"></a>Fonction GetName
Obtient le nom de l’événement.

  
**Retourne**: nom de l’événement
  
### <a name="getlevel-function"></a>GetLevel fonction)
Obtient le niveau d’événement, indiquant s’il est considéré comme les données de service nécessaires (NSD) ou non.

  
**Retourne**: niveau d’événement
  
### <a name="getstarttime-function"></a>GetStartTime fonction)
Obtient l’heure de début de l’événement.

  
**Retourne**: heure de début de l’événement
  
### <a name="addproperty-function"></a>AddProperty, fonction
Ajoutez une propriété à l’événement.

Paramètres :  
* **prop**: propriété à ajouter


  
### <a name="addproperty-function"></a>AddProperty, fonction
Ajoutez une propriété bool à l’événement.

Paramètres :  
* **nom**: nom de la propriété 


* **valeur**: valeur de propriété


  
### <a name="addproperty-function"></a>AddProperty, fonction
Ajoutez une propriété double à l’événement.

Paramètres :  
* **nom**: nom de la propriété 


* **valeur**: valeur de propriété 


* **PII**: classification PII


  
### <a name="addproperty-function"></a>AddProperty, fonction
Ajoutez une propriété Int64 à l’événement.

Paramètres :  
* **nom**: nom de la propriété 


* **valeur**: valeur de propriété 


* **PII**: classification PII


  
### <a name="addproperty-function"></a>AddProperty, fonction
Ajoutez une propriété de type chaîne à l’événement.

Paramètres :  
* **nom**: nom de la propriété 


* **valeur**: valeur de propriété 


* **PII**: classification PII


  
### <a name="addauditonlyproperty-function"></a>AddAuditOnlyProperty fonction)
Ajoutez une propriété de chaîne d’audit uniquement à l’événement.

Paramètres :  
* **nom**: nom de la propriété 


* **valeur**: valeur de propriété


Une propriété auditer uniquement contient des informations sensibles et ne doit pas être écrite dans des journaux de fichiers ou dans un pipeline à l’exception de l’audit jusqu’à ce qu’elle soit nettoyée manuellement.
  
### <a name="getproperties-function"></a>GetProperties, fonction
Obtient toutes les propriétés d’événement.

  
**Retourne**: propriétés de l’événement
  
### <a name="getproperty-function"></a>GetProperty, fonction
Obtient la propriété portant le nom donné, le cas échéant.

Paramètres :  
* **nom**: nom de la propriété à récupérer



  
**Retourne**: la propriété portant le nom donné, ou nullptr si aucune