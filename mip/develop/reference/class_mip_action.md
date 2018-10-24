---
title: mip Action, classe
description: Informations de référence pour la classe mip Action
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 97b082a0a3da1e8b6726d181f42e741f002a7e29
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445969"
---
# <a name="class-mipaction"></a>mip::Action, classe 
Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.