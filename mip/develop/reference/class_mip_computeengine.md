---
title: 'MIP :: ComputeEngine, classe'
description: 'Documente la classe MIP :: computeengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 1faae8e64bbc2e2f2de54f8152b1227148c7d3de
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490385"
---
# <a name="class-mipcomputeengine"></a>MIP :: ComputeEngine, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<std :: shared_ptr\<étiquette\>\>& ListSensitivityLabels ()  | _Pas encore documenté._
public std :: shared_ptr\<ContentLabel\> GetSensitivityLabel (ComputeEngineContext & Context, const DocumentState & State)  | _Pas encore documenté._
public std :: Vector\<std :: shared_ptr\<action\>\> ComputeActions (ComputeEngineContext & Context, const DocumentState & documentState, const ApplicationActionState & actionState)  | _Pas encore documenté._
STD public ::p air\<std :: Vector\<std :: shared_ptr\<action\>\>, bool\> ComputeActionsWithRemoteState (ComputeEngineContext & Context, const DocumentState & localDocumentState, const DocumentState & remoteDocumentState, const ApplicationActionState & actionState)  |  Calcule les actions lors du choix entre l’État distant et l’état local.
public void NotifyCommittedActions (ComputeEngineContext & Context, const DocumentState & documentState, const ApplicationActionState & actionState)  | _Pas encore documenté._
virtuel public ~ ComputeEngine ()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels fonction)
_Pas encore documenté._

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel fonction)
_Pas encore documenté._

  
### <a name="computeactions-function"></a>ComputeActions fonction)
_Pas encore documenté._

  
### <a name="computeactionswithremotestate-function"></a>ComputeActionsWithRemoteState fonction)
Calcule les actions lors du choix entre l’État distant et l’état local.
L’État est sélectionné à l’aide de cette priorité. Types de protection inconnus (modèle ou ad-hoc absents de la stratégie). L’état de protection est toujours préférable à l’état non protégé. L’état du document avec l’étiquette est préférable à un autre sans. Ordre des étiquettes, la valeur la plus élevée est préférée. Horodatage de l’étiquette, préférer le document étiqueté le plus récent. DocumentState LastModifiedTime éventuellement implémenté, préférer le fichier nouvellement modifié.

Paramètres :  
* **Context**: contexte du moteur de calcul. 


* **localDocumentState**: état du document local. 


* **remoteDocumentState**: état du document distant. 


* **actionState**: état d’action de l’application.



  
**Retourne**: les méthodes retournent une paire. tout d’abord contient une liste de l’action, le second est s’il doit être appliqué sur le local, si des actions fausses doivent être appliquées sur le document distant et que l’état du document doit être utilisé.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions fonction)
_Pas encore documenté._

  
### <a name="computeengine-function"></a>~ ComputeEngine fonction)
_Pas encore documenté._
