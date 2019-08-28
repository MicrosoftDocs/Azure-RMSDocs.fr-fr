---
title: 'MIP:: TaskDispatcherDelegate, classe'
description: 'Documente la classe MIP:: taskdispatcherdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d5237bf999f7ad704fd303783a9fbdc506b58ed2
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056759"
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