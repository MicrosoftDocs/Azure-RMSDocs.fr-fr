---
title: TaskDispatcherDelegate de classe
description: 'Documente la classe taskdispatcherdelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: b7cd2267b795540a8bb4035a695f5b34f0580b87
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764278"
---
# <a name="class-taskdispatcherdelegate"></a>TaskDispatcherDelegate de classe 
Classe qui définit l’interface du répartiteur de tâches du kit de développement logiciel (SDK) MIP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std :: String& IDTâche, std :: function\<void ()\> Task)  |  Exécuter une tâche sur un thread d’arrière-plan.
public void DispatchTask (const std :: String& IDTâche, std :: function\<void ()\> Task, int64_t delaySeconds)  |  Exécuter une tâche sur un thread d’arrière-plan avec le délai donné.
public void ExecuteTaskOnIndependentThread (const std :: String& IDTâche, std :: function\<void ()\> Task)  |  Exécuter immédiatement une tâche sur un thread indépendant.
public bool CancelTask (const std :: String& taskId)  |  Annuler une tâche en arrière-plan.
public void CancelAllTasks ()  |  Annule toutes les tâches en arrière-plan.
  
## <a name="members"></a>Membres
  
### <a name="dispatchtask-function"></a>DispatchTask fonction)
Exécuter une tâche sur un thread d’arrière-plan.

Paramètres :  
* **taskId**: ID pour identifier de manière unique une tâche 


* **tâche**: fonction à exécuter


  
### <a name="dispatchtask-function"></a>DispatchTask fonction)
Exécuter une tâche sur un thread d’arrière-plan avec le délai donné.

Paramètres :  
* **taskId**: ID pour identifier de manière unique une tâche 


* **tâche**: fonction à exécuter 


* **delaySeconds**: délai (en secondes) avant l’exécution de la tâche


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread fonction)
Exécuter immédiatement une tâche sur un thread indépendant.

Paramètres :  
* **taskId**: ID pour identifier de manière unique une tâche 


* **tâche**: fonction à exécuter


  
### <a name="canceltask-function"></a>CancelTask fonction)
Annuler une tâche en arrière-plan.

Paramètres :  
* **taskId**: ID de la tâche à annuler



  
**Retourne**la valeur true si la tâche a été annulée avec succès, sinon false.
  
### <a name="cancelalltasks-function"></a>CancelAllTasks fonction)
Annule toutes les tâches en arrière-plan.