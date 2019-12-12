---
title: mip::Action, classe
description: 'Documente la classe MIP :: action du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d3cc1aecfb5ca8bf2d78dd9d6c8c280b5541389d
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560412"
---
# <a name="class-mipaction"></a>mip::Action, classe 
Interface pour une action. Chaque action se traduit par une étape qui doit être effectuée par l’application pour appliquer l’étiquette (comme défini dans la stratégie)
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public ActionType GetType() const  |  Obtient le type d’action.
  
## <a name="members"></a>Membres
  
### <a name="gettype-function"></a>GetType, fonction
Obtient le type d’action.

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.