---
title: class mip::ProtectByTemplateAction
description: Décrit la classe mip::protectbytemplateaction de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 18bdf3caa5eba2f335376d81f525fe93da4d0352
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173234"
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