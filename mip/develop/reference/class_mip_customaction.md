---
title: mip::CustomAction, classe
description: Décrit la classe mip::customaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 49840aebf5d49e91671145d0c5dc9e3b6d8e4694
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650644"
---
# <a name="class-mipcustomaction"></a>mip::CustomAction, classe 
[CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Obtenir le nom de l’action.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetProperties() const  |  Obtenir la liste de paires clé/valeur des propriétés.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getname-function"></a>GetName (fonction)
Obtenir le nom de l’action.

  
**Retourne**: Un nom d’action s’il existe ; sinon une chaîne vide.
  
### <a name="getproperties-function"></a>GetProperties (fonction)
Obtenir la liste de paires clé/valeur des propriétés.

  
**Retourne**: Une liste de paires de valeur de clé.
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.