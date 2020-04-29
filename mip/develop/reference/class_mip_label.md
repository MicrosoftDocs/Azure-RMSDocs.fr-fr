---
title: Étiquette de la classe
description: 'Documente la classe Label :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 95eb7c523e7e627aff767169b9d35479839ac72d
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762195"
---
# <a name="class-label"></a>Étiquette de la classe 
Abstraction d’une étiquette unique Microsoft Information Protection.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtenir l’ID de l’étiquette.
public const std::string& GetName() const  |  Obtenir le nom de l’étiquette.
public const std::string& GetDescription() const  |  Obtenir la description de l’étiquette.
public const std::string& GetColor() const  |  Obtenir la couleur d’affichage de l’étiquette.
public int GetSensitivity() const  |  Obtenir la Sensibilité de l’étiquette.
public const std::string& GetTooltip() const  |  Obtenir la description de l’info-bulle de l’étiquette.
public const std :: String& GetAutoTooltip () const  |  Obtient la description de l’info-bulle de la classification qui entraîne l’application de cette étiquette.
public bool IsActive() const  |  Obtient une valeur booléenne signalant si l’étiquette est active.
public std :: weak_ptr\<,\> étiquette GetParent () const  |  Obtenir l’étiquette parente.
public const std :: Vector\<std :: shared_ptr\<étiquette\> \>& GetChildren () const  |  Obtenir les étiquettes enfants de l’étiquette actuelle.
public const std :: Vector\<std ::p air\<std :: String, std :: String\> \>& GetCustomSettings () const  |  Obtient les paramètres personnalisés d’une étiquette.
public ActionSource GetActionSource() const  |  Obtient la source d’action de l’étiquette.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtenir l’ID de l’étiquette.

  
**Retourne** : ID de l’étiquette.
  
### <a name="getname-function"></a>Fonction GetName
Obtenir le nom de l’étiquette.

  
**Retourne** : le nom de l’étiquette.
  
### <a name="getdescription-function"></a>GetDescription, fonction
Obtenir la description de l’étiquette.

  
**Retourne** : la description de l’étiquette.
  
### <a name="getcolor-function"></a>Fonction GetColor
Obtenir la couleur d’affichage de l’étiquette.

  
**Retourne** : la valeur de la couleur au format chaîne. « #RRGGBB » où RR, GG et BB sont une valeur au format hexadécimal 0-f.
  
### <a name="getsensitivity-function"></a>GetSensitivity fonction)
Obtenir la Sensibilité de l’étiquette.

  
**Retourne** : une valeur numérique. Les valeurs plus élevées indiquent une Sensibilité plus élevée.
  
### <a name="gettooltip-function"></a>GetTooltip fonction)
Obtenir la description de l’info-bulle de l’étiquette.

  
**Retourne** : une chaîne d’info-bulle.
  
### <a name="getautotooltip-function"></a>GetAutoTooltip fonction)
Obtient la description de l’info-bulle de la classification qui entraîne l’application de cette étiquette.

  
**Retourne** : une chaîne d’info-bulle.
  
### <a name="isactive-function"></a>IsActive, fonction
Obtient une valeur booléenne signalant si l’étiquette est active.
Seules les étiquettes actives peuvent être appliquées. Les étiquettes inactives ne peuvent pas être appliquées et sont utilisées uniquement à des fins d’affichage. 

  
**Retourne** : true si l’étiquette est active ; sinon, false.
  
### <a name="getparent-function"></a>GetParent, fonction
Obtenir l’étiquette parente.

  
**Retourne** : un pointeur faible vers l’étiquette parent si elle existe ; sinon, un pointeur vide.
  
### <a name="getchildren-function"></a>GetChildren, fonction
Obtenir les étiquettes enfants de l’étiquette actuelle.

  
**Retourne** : un vecteur de pointeurs partagés vers des étiquettes.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient les paramètres personnalisés d’une étiquette.

  
**Retourne**: un vecteur de paires clé-valeur représentant des paramètres personnalisés.
  
### <a name="getactionsource-function"></a>GetActionSource fonction)
Obtient la source d’action de l’étiquette.

  
**Retourne**: source de l’action