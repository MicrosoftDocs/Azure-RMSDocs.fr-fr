---
title: PolicyHandler de classe
description: 'Documente la classe policyhandler :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: b70643c9db84cef329b64e515bef5c7c47801718
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567378"
---
# <a name="class-policyhandler"></a>PolicyHandler de classe 
Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<ContentLabel\> GetSensitivityLabel(const ExecutionState& state)  |  Obtenir l’étiquette de sensibilité à partir du contenu existant.
public std :: Vector \<std::shared_ptr\<Action\> \> ComputeActions (const ExecutionState& State)  |  Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.
public void NotifyCommittedActions(const ExecutionState& state)  |  Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.
  
## <a name="members"></a>Membres
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel fonction)
Obtenir l’étiquette de sensibilité à partir du contenu existant.

Paramètres :  
* **État**: état actuel du contenu. 



  
**Retourne** : étiquette actuellement appliquée au contenu. En l’absence d’étiquette, retourne une valeur vide.
  
### <a name="computeactions-function"></a>ComputeActions fonction)
Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.

Paramètres :  
* **state** : état actuel de l’exécution du contenu auquel les règles sont appliquées. 



  
**Retourne** : une liste des actions à appliquer au contenu.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions fonction)
Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.

Paramètres :  
* **État**: état d’exécution actuel du contenu une fois que les actions ont été validées. 


: Cet appel envoie un événement d’audit.