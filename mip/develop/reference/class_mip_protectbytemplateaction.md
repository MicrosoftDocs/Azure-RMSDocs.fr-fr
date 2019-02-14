---
title: class mip::ProtectByTemplateAction
description: Décrit la classe mip::protectbytemplateaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9c7114bcceceef537675ca04499cdb1710456b82
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252365"
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
