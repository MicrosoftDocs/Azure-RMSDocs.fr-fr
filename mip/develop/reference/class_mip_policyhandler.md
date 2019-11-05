---
title: mip::PolicyHandler, classe
description: Documente la classe MIP ::p olicyhandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 71b1a9dff879cde728e7fa1aa9e1f871d292ec4c
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560920"
---
# <a name="class-mippolicyhandler"></a>mip::PolicyHandler, classe 
Cette classe fournit une interface pour toutes les fonctions de gestionnaire de stratégie sur un fichier.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr\<ContentLabel\> GetSensitivityLabel (const ExecutionState & État)  |  Obtenir l’étiquette de sensibilité à partir du contenu existant.
public std :: Vector\<std :: shared_ptr\<action\>\> ComputeActions (const ExecutionState & State)  |  Exécute les règles dans le gestionnaire en fonction de l’état fourni et retourne la liste des actions à exécuter.
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