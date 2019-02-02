---
title: class mip::ProtectByTemplateAction
description: Décrit la classe mip::protectbytemplateaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 1c05a04df39e6454eb934b5db48e96339afdac0c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650814"
---
# <a name="class-mipprotectbytemplateaction"></a>class mip::ProtectByTemplateAction 
Classe d’action qui spécifie l’ajout de la protection par modèle au document.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetTemplateId() const  |  Obtenir l’ID du modèle de protection associé à l’action.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="gettemplateid-function"></a>GetTemplateId (fonction)
Obtenir l’ID du modèle de protection associé à l’action.

  
**Retourne**: L’ID de modèle de protection.
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.