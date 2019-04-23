---
title: class mip::ApplyLabelAction
description: Décrit la classe mip::applylabelaction de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 70f226cc112062582b5441f6c3ae7fc3dc7de118
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173318"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  Obtenir l’ID de l’étiquette requis.
public const std::vector\<std::string\>& GetClassificationIds() const  |  Obtenir les ID de Classification qui correspondait et a provoqué cette étiquette qui doivent apparaître.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).

## <a name="members"></a>Membres
  
### <a name="getlabelid-function"></a>GetLabelId (fonction)
Obtenir l’ID de l’étiquette requis.

  
**Retourne**: L’ID d’étiquette.
  
### <a name="getclassificationids-function"></a>GetClassificationIds function
Obtenir les ID de Classification qui correspondait et a provoqué cette étiquette qui doivent apparaître.

  
**Retourne**: Const std::vector < std::string > et une liste de classification d’ID qui a provoqué cette étiquette qui doivent apparaître.

### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.