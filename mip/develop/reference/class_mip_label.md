---
title: mip Label, classe
description: Informations de référence pour la classe mip Label
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 2a80748430df83a16a4d5ee716344d17ce7deee4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446275"
---
# <a name="class-miplabel"></a>mip::Label, classe 
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
 public bool IsActive() const  |  Obtient une valeur booléenne signalant si l’étiquette est active.
public std::weak_ptr<Label> GetParent() const  |  Obtenir l’étiquette parente.
public const std::vector<std::shared_ptr<Label>>& GetChildren() const  |  Obtenir les étiquettes enfants de l’étiquette actuelle.
  
## <a name="members"></a>Membres
  
### <a name="getid"></a>GetId
Obtenir l’ID de l’étiquette.

  
**Retourne** : ID de l’étiquette.
  
### <a name="getname"></a>GetName
Obtenir le nom de l’étiquette.

  
**Retourne** : le nom de l’étiquette.
  
### <a name="getdescription"></a>GetDescription
Obtenir la description de l’étiquette.

  
**Retourne** : la description de l’étiquette.
  
### <a name="getcolor"></a>GetColor
Obtenir la couleur d’affichage de l’étiquette.

  
**Retourne** : la valeur de la couleur au format chaîne. « #RRGGBB » où RR, GG et BB sont une valeur au format hexadécimal 0-f.
  
### <a name="getsensitivity"></a>GetSensitivity
Obtenir la Sensibilité de l’étiquette.

  
**Retourne** : une valeur numérique. Les valeurs plus élevées indiquent une Sensibilité plus élevée.
  
### <a name="gettooltip"></a>GetTooltip
Obtenir la description de l’info-bulle de l’étiquette.

  
**Retourne** : une chaîne d’info-bulle.
  
### <a name="isactive"></a>IsActive
Obtient une valeur booléenne signalant si l’étiquette est active.
Seules les étiquettes actives peuvent être appliquées. Les étiquettes inactives ne peuvent pas être appliquées et sont utilisées uniquement à des fins d’affichage. 

  
**Retourne** : true si l’étiquette est active ; sinon, false.
  
### <a name="label"></a>Étiquette
Obtenir l’étiquette parente.

  
**Retourne** : un pointeur faible vers l’étiquette parent si elle existe ; sinon, un pointeur vide.
  
### <a name="label"></a>Étiquette
Obtenir les étiquettes enfants de l’étiquette actuelle.

  
**Retourne** : un vecteur de pointeurs partagés vers des étiquettes.