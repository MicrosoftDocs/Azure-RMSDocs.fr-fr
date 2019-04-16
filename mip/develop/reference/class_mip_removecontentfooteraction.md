---
title: mip::RemoveContentFooterAction, classe
description: Décrit la classe mip::removecontentfooteraction de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 14afd4688c13f419ab3019e9c268ba7d355121c8
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574259"
---
# <a name="class-mipremovecontentfooteraction"></a>mip::RemoveContentFooterAction, classe 
Classe d’action qui spécifie la suppression du pied de page de contenu du document.
  
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