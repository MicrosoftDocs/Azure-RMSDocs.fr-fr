---
title: 'MIP:: TaskDispatcherDelegate, classe'
description: 'Documente la classe MIP:: taskdispatcherdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 0455f446cddd7db1c05f0f7e7b76b33496810cf1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883023"
---
# <a name="class-miptaskdispatcherdelegate"></a>MIP:: TaskDispatcherDelegate, classe 
Classe qui définit l’interface du répartiteur de tâches du kit de développement logiciel (SDK) MIP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: String & IDTâche, std:: function\<void ()\> Task)  |  Exécuter une tâche sur un thread d’arrière-plan.
public void DispatchTask (const std:: String & IDTâche, std:: function\<void ()\> tâche, int64_t Delay)  |  Exécuter une tâche sur un thread d’arrière-plan avec le délai donné.
public void ExecuteTaskOnIndependentThread (const std:: String & IDTâche, std:: function\<void ()\> Task)  |  Exécuter immédiatement une tâche sur un thread indépendant.
public bool CancelTask (const std:: String & taskId)  |  Annuler une tâche en arrière-plan.
public void CancelAllTasks ()  |  Annule toutes les tâches en arrière-plan.
  
## <a name="members"></a>Membres
  
### <a name="dispatchtask-function"></a>DispatchTask fonction)
Exécuter une tâche sur un thread d’arrière-plan.

Paramètres :  
* **taskId**: ID identifiant une tâche de manière unique 


* **tâche**: Fonction à exécuter


  
### <a name="dispatchtask-function"></a>DispatchTask fonction)
Exécuter une tâche sur un thread d’arrière-plan avec le délai donné.

Paramètres :  
* **taskId**: ID identifiant une tâche de manière unique 


* **tâche**: Fonction à exécuter 


* **délai**: Délai (en secondes) avant l’exécution de la tâche


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread fonction)
Exécuter immédiatement une tâche sur un thread indépendant.

Paramètres :  
* **taskId**: ID identifiant une tâche de manière unique 


* **tâche**: Fonction à exécuter


  
### <a name="canceltask-function"></a>CancelTask fonction)
Annuler une tâche en arrière-plan.

Paramètres :  
* **taskId**: ID de la tâche à annuler



  
**Retourne**: True si la tâche a été annulée avec succès, sinon false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks fonction)
Annule toutes les tâches en arrière-plan.