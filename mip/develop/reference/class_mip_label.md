---
title: mip::Label, classe
description: Décrit la classe mip::label de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 5a2444ab0abd944418a8d55eae35c5f6023282f7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253225"
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
public std::weak_ptr\<Label\> GetParent() const  |  Obtenir l’étiquette parente.
public const std::vector\<std::shared_ptr\<Label\>\>& GetChildren() const  |  Obtenir les étiquettes enfants de l’étiquette actuelle.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtenir les paramètres personnalisés d’une étiquette.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId (fonction)
Obtenir l’ID de l’étiquette.

  
**Retourne**: L’ID d’étiquette.
  
### <a name="getname-function"></a>GetName (fonction)
Obtenir le nom de l’étiquette.

  
**Retourne**: Le nom d’étiquette.
  
### <a name="getdescription-function"></a>GetDescription (fonction)
Obtenir la description de l’étiquette.

  
**Retourne**: La description de l’étiquette.
  
### <a name="getcolor-function"></a>GetColor (fonction)
Obtenir la couleur d’affichage de l’étiquette.

  
**Retourne**: Valeur de couleur du format de chaîne. « #RRGGBB » où RR, GG et BB sont une valeur au format hexadécimal 0-f.
  
### <a name="getsensitivity-function"></a>GetSensitivity (fonction)
Obtenir la Sensibilité de l’étiquette.

  
**Retourne**: Une valeur numérique. Les valeurs plus élevées indiquent une Sensibilité plus élevée.
  
### <a name="gettooltip-function"></a>GetTooltip (fonction)
Obtenir la description de l’info-bulle de l’étiquette.

  
**Retourne**: Une chaîne d’info-bulle.
  
### <a name="isactive-function"></a>IsActive (fonction)
Obtient une valeur booléenne signalant si l’étiquette est active.
Seules les étiquettes actives peuvent être appliquées. Les étiquettes inactives ne peuvent pas être appliquées et sont utilisées uniquement à des fins d’affichage. 

  
**Retourne**: True si l’étiquette est active ; sinon, false.
  
### <a name="getparent-function"></a>GetParent (fonction)
Obtenir l’étiquette parente.

  
**Retourne**: Un pointeur faible vers le parent de l’étiquette si un pointeur vide a été défini.
  
### <a name="getchildren-function"></a>GetChildren (fonction)
Obtenir les étiquettes enfants de l’étiquette actuelle.

  
**Retourne**: Un vecteur de pointeurs partagés vers étiquettes.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (fonction)
Obtenir les paramètres personnalisés d’une étiquette.

  
**Retourne**: Un vecteur de paires clé / valeur représentant les paramètres personnalisés.
