---
title: class mip::JustifyAction
description: Décrit la classe mip::justifyaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: e52a38f8ca25ecb8cc8ae470cb77164abb2b6ec8
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650680"
---
# <a name="class-mipjustifyaction"></a>class mip::JustifyAction 
Justify [Action](class_mip_action.md) nécessite de fournir une justification de rétrogradation d’une étiquette et de définir la réponse dans l’état d’exécution.
  
**Voir aussi**: [mip::ExecutionState::IsDowngradeJustified](class_mip_executionstate.md#isdowngradejustified-function)
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.