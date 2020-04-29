---
title: RemoveWatermarkAction de classe
description: 'Documente la classe removewatermarkaction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 93c99a0bd66df636de618629ff25d7f37d0cddd8
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760514"
---
# <a name="class-removewatermarkaction"></a>RemoveWatermarkAction de classe 
Classe d’action qui spécifie la suppression du filigrane du document.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<std :: String\>& GetUIElementNames ()  |  Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
public ActionType GetType() const  |  Obtenir le type de Action.
  
## <a name="members"></a>Membres
  
### <a name="getuielementnames-function"></a>GetUIElementNames fonction)
Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.

  
**Retourne** : une liste de noms d’éléments d’interface utilisateur.
  
### <a name="gettype-function"></a>GetType, fonction
Obtenir le type de Action.

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.