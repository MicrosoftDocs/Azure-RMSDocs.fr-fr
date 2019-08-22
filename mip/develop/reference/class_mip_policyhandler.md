---
title: mip::PolicyHandler, classe
description: Documente la classe MIP::p olicyhandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 7185af867a94e4b72663f818d5d1f7233e4219b3
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883804"
---
# <a name="class-mippolicyhandler"></a>mip::PolicyHandler, classe 
Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (const ExecutionState & State)  |  Obtenir l’étiquette de sensibilité à partir du contenu existant.
public std:: Vector\<std:: shared_ptr\<action\> \> ComputeActions (const ExecutionState & State)  |  Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.
public void NotifyCommittedActions(const ExecutionState& state)  |  Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.
  
## <a name="members"></a>Membres
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel fonction)
Obtenir l’étiquette de sensibilité à partir du contenu existant.

Paramètres :  
* **state** : État actuel du contenu. 



  
**Retourne**: Étiquette actuellement appliquée au contenu. En l’absence d’étiquette, retourne une valeur vide.
  
### <a name="computeactions-function"></a>ComputeActions fonction)
Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.

Paramètres :  
* **state** : état actuel de l’exécution du contenu auquel les règles sont appliquées. 



  
**Retourne**: Liste des actions qui doivent être appliquées au contenu.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions fonction)
Appelé une fois que les actions calculées ont été appliquées et les données validées sur le disque.

Paramètres :  
* **État**: état d’exécution actuel du contenu une fois que les actions ont été validées. 


: Cet appel envoie un événement d’audit.