---
title: class mip::RecommendLabelAction
description: Décrit la classe mip::recommendlabelaction de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: eeab9022b257ff327e2c83b1d8860662355180e5
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573158"
---
# <a name="class-miprecommendlabelaction"></a>class mip::RecommendLabelAction 
Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  Obtenir l’ID de l’étiquette suggéré.
public const std::vector\<std::string\>& GetClassificationIds() const  |  Obtenir les ID de Classification qui correspondait et a provoqué cette étiquette qui doivent apparaître.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).

## <a name="members"></a>Membres
  
### <a name="getlabelid-function"></a>GetLabelId (fonction)
Obtenir l’ID de l’étiquette suggéré.

  
**Retourne**: L’ID d’étiquette.
  
### <a name="getclassificationids-function"></a>GetClassificationIds function
Obtenir les ID de Classification qui correspondait et a provoqué cette étiquette qui doivent apparaître.

  
**Retourne**: Const std::vector < std::string > et une liste de classification d’ID qui a provoqué cette étiquette qui doivent apparaître.

### <a name="gettype-function"></a>Fonction GetType    
Obtenir le type de [Action](class_mip_action.md).  

**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.