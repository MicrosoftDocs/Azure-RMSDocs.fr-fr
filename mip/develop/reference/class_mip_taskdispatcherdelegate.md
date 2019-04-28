---
title: classe mip::TaskDispatcherDelegate
description: Décrit la classe mip::taskdispatcherdelegate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 568a6df614370769556cd3634070e199beb4da5b
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184278"
---
# <a name="class-miptaskdispatcherdelegate"></a>classe mip::TaskDispatcherDelegate 
Une classe qui définit l’interface pour le répartiteur de tâche du SDK MIP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void DispatchTask(const std::string& taskId, std::function\<void()\> task)  |  Exécuter une tâche sur un thread d’arrière-plan.
public void DispatchTask(const std::string& taskId, std::function\<void()\> task, int64_t delay)  |  Exécuter une tâche sur un thread d’arrière-plan avec le délai donné.
public void ExecuteTaskOnIndependentThread(const std::string& taskId, std::function\<void()\> task)  |  Exécuter immédiatement une tâche sur un thread indépendant.
public bool CancelTask (const std::string & ID de tâche)  |  Annuler une tâche en arrière-plan.
CancelAllTasks() void publique  |  Annuler toutes les tâches en arrière-plan.
  
## <a name="members"></a>Membres
  
### <a name="dispatchtask-function"></a>DispatchTask (fonction)
Exécuter une tâche sur un thread d’arrière-plan.

Paramètres :  
* **ID de tâche**: ID pour identifier de manière unique une tâche 


* **tâche**: Fonction à exécuter


  
### <a name="dispatchtask-function"></a>DispatchTask (fonction)
Exécuter une tâche sur un thread d’arrière-plan avec le délai donné.

Paramètres :  
* **ID de tâche**: ID pour identifier de manière unique une tâche 


* **tâche**: Fonction à exécuter 


* **délai**: Délai d’attente (en secondes) avant l’exécution de tâche


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread (fonction)
Exécuter immédiatement une tâche sur un thread indépendant.

Paramètres :  
* **ID de tâche**: ID pour identifier de manière unique une tâche 


* **tâche**: Fonction à exécuter


  
### <a name="canceltask-function"></a>CancelTask (fonction)
Annuler une tâche en arrière-plan.

Paramètres :  
* **ID de tâche**: ID de tâche à annuler



  
**Retourne**: True si la tâche a été correctement annulée ; sinon, false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks (fonction)
Annuler toutes les tâches en arrière-plan.