---
title: class mip::RecommendLabelAction
description: Décrit la classe mip::recommendlabelaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ec1f82ab5951a5b7813fff2ebd5be6650a80203b
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651341"
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