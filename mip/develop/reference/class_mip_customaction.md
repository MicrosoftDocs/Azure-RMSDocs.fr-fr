---
title: mip CustomAction, classe
description: Informations de référence pour la classe mip CustomAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a94a41c0e7f7848201e2af44187cce2540579b27
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444706"
---
# <a name="class-mipcustomaction"></a>mip::CustomAction, classe 
[CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetName() const  |  Obtenir le nom de l’action.
public const std::vector<std::pair<std::string, std::string>>& GetProperties() const  |  Obtenir la liste de paires clé/valeur des propriétés.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getname"></a>GetName
Obtenir le nom de l’action.

  
**Retourne** : nom de l’action s’il existe ; sinon une chaîne vide.
  
### <a name="getproperties"></a>GetProperties
Obtenir la liste de paires clé/valeur des propriétés.

  
**Retourne** : une liste de paires clé/valeur.
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.