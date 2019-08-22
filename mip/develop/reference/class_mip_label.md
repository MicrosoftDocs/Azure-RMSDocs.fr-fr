---
title: mip::Label, classe
description: 'Documente la classe MIP:: label du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 3d746c1f271d75c160ca721ebe6f0fef0f15bd5e
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884047"
---
# <a name="class-miplabel"></a>mip::Label, classe 
Abstraction d’une étiquette unique Microsoft Information Protection.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtenir l’ID de l’étiquette.
public const std::string& GetName() const  |  Obtenir le nom de l’étiquette.
public const std::string& GetDescription() const  |  Obtenir la description de l’étiquette.
public const std::string& GetColor() const  |  Obtenir la couleur d’affichage de l’étiquette.
public int GetSensitivity() const  |  Obtenir la Sensibilité de l’étiquette.
public const std::string& GetTooltip() const  |  Obtenir la description de l’info-bulle de l’étiquette.
public bool IsActive() const  |  Obtient une valeur booléenne signalant si l’étiquette est active.
public std:: weak_ptr\<label\> GetParent () const  |  Obtenir l’étiquette parente.
public const std:: Vector\<std:: shared_ptr\<étiquette\>\>& GetChildren () const  |  Obtenir les étiquettes enfants de l’étiquette actuelle.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient les paramètres personnalisés d’une étiquette.
public ActionSource GetActionSource() const  |  Obtient la source d’action de l’étiquette.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtenir l’ID de l’étiquette.

  
**Retourne**: ID de l’étiquette.
  
### <a name="getname-function"></a>Fonction GetName
Obtenir le nom de l’étiquette.

  
**Retourne**: Nom de l’étiquette.
  
### <a name="getdescription-function"></a>GetDescription, fonction
Obtenir la description de l’étiquette.

  
**Retourne**: Description de l’étiquette.
  
### <a name="getcolor-function"></a>Fonction GetColor
Obtenir la couleur d’affichage de l’étiquette.

  
**Retourne**: Valeur de couleur format de chaîne. « #RRGGBB » où RR, GG et BB sont une valeur au format hexadécimal 0-f.
  
### <a name="getsensitivity-function"></a>GetSensitivity fonction)
Obtenir la Sensibilité de l’étiquette.

  
**Retourne**: Valeur numérique. Les valeurs plus élevées indiquent une Sensibilité plus élevée.
  
### <a name="gettooltip-function"></a>GetTooltip fonction)
Obtenir la description de l’info-bulle de l’étiquette.

  
**Retourne**: Chaîne d’info-bulle.
  
### <a name="isactive-function"></a>IsActive, fonction
Obtient une valeur booléenne signalant si l’étiquette est active.
Seules les étiquettes actives peuvent être appliquées. Les étiquettes inactives ne peuvent pas être appliquées et sont utilisées uniquement à des fins d’affichage. 

  
**Retourne**: True si l’étiquette est active, sinon false.
  
### <a name="getparent-function"></a>GetParent, fonction
Obtenir l’étiquette parente.

  
**Retourne**: Pointeur faible vers l’étiquette parente si existe sinon un pointeur vide.
  
### <a name="getchildren-function"></a>GetChildren, fonction
Obtenir les étiquettes enfants de l’étiquette actuelle.

  
**Retourne**: Vecteur de pointeurs partagés vers des étiquettes.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient les paramètres personnalisés d’une étiquette.

  
**Retourne**: Vecteur de paires clé-valeur représentant des paramètres personnalisés.
  
### <a name="getactionsource-function"></a>GetActionSource fonction)
Obtient la source d’action de l’étiquette.

  
**Retourne**: Source de l' [action](class_mip_action.md)