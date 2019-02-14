---
title: mip::RemoveContentHeaderAction, classe
description: Décrit la classe mip::removecontentheaderaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 5025b35d9c8edd7e01a6799bd5b08a8703784086
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259244"
---
# <a name="class-mipremovecontentheaderaction"></a>mip::RemoveContentHeaderAction, classe 
Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
  
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
