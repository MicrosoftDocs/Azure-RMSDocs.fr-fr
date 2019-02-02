---
title: mip::RemoveWatermarkAction, classe
description: Décrit la classe mip::removewatermarkaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8bd17001426c826b9ce2f0d627177ef783d09046
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651069"
---
# <a name="class-mipremovewatermarkaction"></a>mip::RemoveWatermarkAction, classe 
Classe d’action qui spécifie la suppression du filigrane du document.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetUIElementNames()  |  Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementnames-function"></a>GetUIElementNames (fonction)
Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.

  
**Retourne**: Une liste de noms d’éléments de l’interface utilisateur.
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.