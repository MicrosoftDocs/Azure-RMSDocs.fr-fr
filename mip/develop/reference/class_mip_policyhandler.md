---
title: mip PolicyHandler, classe
description: Informations de référence pour la classe mip PolicyHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 23de5616558a298189cb885727d69a20373a3609
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445935"
---
# <a name="class-mippolicyhandler"></a>mip::PolicyHandler, classe 
Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  Obtenir l’étiquette de sensibilité à partir du contenu existant.
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.
 public void NotifyCommittedActions(const ExecutionState& state)  |  Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.
  
## <a name="members"></a>Membres
  
### <a name="contentlabel"></a>ContentLabel
Obtenir l’étiquette de sensibilité à partir du contenu existant.

Paramètres :  
* **state** : état actuel du contenu 



  
**Retourne** : étiquette actuellement appliquée au contenu. En l’absence d’étiquette, retourne une valeur vide.
  
### <a name="action"></a>Action
Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.

Paramètres :  
* **state** : état actuel de l’exécution du contenu auquel les règles sont appliquées. 



  
**Retourne** : une liste des actions à appliquer au contenu.
  
### <a name="notifycommittedactions"></a>NotifyCommittedActions
Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.

Paramètres :  
* **state** : état actuel de l’exécution du contenu une fois que les actions ont été validées 


Cet appel envoie un événement d’audit