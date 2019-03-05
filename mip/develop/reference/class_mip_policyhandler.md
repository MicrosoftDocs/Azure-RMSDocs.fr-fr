---
title: mip::PolicyHandler, classe
description: Décrit la classe mip::policyhandler de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6c5979706b9868bd7d0b6b1adad5d96bd5d3e0ce
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329588"
---
# <a name="class-mippolicyhandler"></a>mip::PolicyHandler, classe 
Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<ContentLabel\> GetSensitivityLabel (ExecutionState const & state)  |  Obtenir l’étiquette de sensibilité à partir du contenu existant.
public std::vector\<std::shared_ptr\<Action\> \> ComputeActions (ExecutionState const & state)  |  Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.
public void NotifyCommittedActions(const ExecutionState& state)  |  Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.
  
## <a name="members"></a>Membres
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel (fonction)
Obtenir l’étiquette de sensibilité à partir du contenu existant.

Paramètres :  
* **state** : État actuel du contenu 



  
**Retourne**: L’étiquette actuellement appliqué au contenu. En l’absence d’étiquette, retourne une valeur vide.
  
### <a name="computeactions-function"></a>ComputeActions (fonction)
Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.

Paramètres :  
* **state** : état actuel de l’exécution du contenu auquel les règles sont appliquées. 



  
**Retourne**: Liste des actions qui doivent être appliquées sur le contenu.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions (fonction)
Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.

Paramètres :  
* **state** : état actuel de l’exécution du contenu une fois que les actions ont été validées 


: Cet appel envoie un événement d’audit
