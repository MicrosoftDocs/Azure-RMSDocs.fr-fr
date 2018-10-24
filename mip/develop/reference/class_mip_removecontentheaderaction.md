---
title: mip RemoveContentHeaderAction, classe
description: Informations de référence pour la classe mip RemoveContentHeaderAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: dc79ebf5d5c7cd35a8fc5ed854315179ed9190f0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446445"
---
# <a name="class-mipremovecontentheaderaction"></a>mip::RemoveContentHeaderAction, classe 
Classe d’action qui spécifie la suppression de l’en-tête de contenu du document.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetUIElementNames()  |  Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementnames"></a>GetUIElementNames
Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.

  
**Retourne** : une liste de noms d’éléments d’interface utilisateur.
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.