---
title: 'MIP :: TaskDispatcherDelegate, classe'
description: 'Documente la classe MIP :: taskdispatcherdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e73a03b842b1216bcc4ef71941ca4bc0b0233945
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559956"
---
# <a name="class-miptaskdispatcherdelegate"></a>MIP :: TaskDispatcherDelegate, classe 
Classe qui définit l’interface du répartiteur de tâches du kit de développement logiciel (SDK) MIP.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std :: String & IDTâche, std :: function\<void ()\> Task)  |  Exécuter une tâche sur un thread d’arrière-plan.
public void DispatchTask (const std :: String & IDTâche, std :: function\<void ()\> Task, int64_t delaySeconds)  |  Exécuter une tâche sur un thread d’arrière-plan avec le délai donné.
public void ExecuteTaskOnIndependentThread (const std :: String & IDTâche, std :: function\<void ()\> Task)  |  Exécuter immédiatement une tâche sur un thread indépendant.
public bool CancelTask (const std :: String & taskId)  |  Annuler une tâche en arrière-plan.
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