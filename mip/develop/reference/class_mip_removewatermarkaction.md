---
title: RemoveWatermarkAction de classe
description: 'Documente la classe removewatermarkaction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 2c140461d0cf8b01b25893900191563b1fe3c8b0
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213162"
---
# <a name="class-removewatermarkaction"></a>RemoveWatermarkAction de classe 
Classe d’action qui spécifie la suppression du filigrane du document.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector \<std::string\>& GetUIElementNames ()  |  Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
public ActionType GetType() const  |  Obtenir le type de Action.
  
## <a name="members"></a>Membres
  
### <a name="getuielementnames-function"></a>GetUIElementNames fonction)
Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.

  
**Retourne** : une liste de noms d’éléments d’interface utilisateur.
  
### <a name="gettype-function"></a>GetType, fonction
Obtenir le type de Action.

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.