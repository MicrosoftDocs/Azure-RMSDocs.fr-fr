---
title: mip::RemoveContentFooterAction, classe
description: Décrit la classe mip::removecontentfooteraction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cff3c01b01f5e02f7df3376fc2cb10fc0a6858fa
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259522"
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
