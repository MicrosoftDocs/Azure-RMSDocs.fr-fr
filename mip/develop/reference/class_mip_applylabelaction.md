---
title: mip ApplyLabelAction, classe
description: Informations de référence pour la classe mip ApplyLabelAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06a17ef1e60503cfb7d690bea9bb72316544f16d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445765"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetLabelId() const  |  Obtenir l’ID de l’étiquette requis.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getlabelid"></a>GetLabelId
Obtenir l’ID de l’étiquette requis.

  
**Retourne** : ID de l’étiquette.
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.