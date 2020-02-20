---
title: mip::RemoveWatermarkAction, classe
description: 'Documente la classe MIP :: removewatermarkaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c2e6eb141d213a9ca19a345a4dac68120200abf8
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489484"
---
# <a name="class-mipremovewatermarkaction"></a>mip::RemoveWatermarkAction, classe 
Classe d’action qui spécifie la suppression du filigrane du document.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<std :: String\>& GetUIElementNames ()  |  Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
public ActionType GetType() const  |  Obtient le type d’action.
  
## <a name="members"></a>Membres
  
### <a name="getuielementnames-function"></a>GetUIElementNames fonction)
Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.

  
**Retourne** : une liste de noms d’éléments d’interface utilisateur.
  
### <a name="gettype-function"></a>GetType, fonction
Obtient le type d’action.

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.