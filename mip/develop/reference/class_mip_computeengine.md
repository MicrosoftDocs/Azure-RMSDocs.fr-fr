---
title: ComputeEngine de classe
description: 'Documente la classe computeengine :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3b33c9a91f40422c29282ddee9292f6bbbad90c9
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763504"
---
# <a name="class-computeengine"></a>ComputeEngine de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<std :: shared_ptr\<étiquette\> \>& ListSensitivityLabels ()  | _Pas encore documenté._
public std :: shared_ptr\<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& contexte, const DocumentState& État)  | _Pas encore documenté._
public std :: Vector\<std :: shared_ptr\<action\> \> ComputeActions (ComputeEngineContext& Context, const DocumentState& DocumentState, const ApplicationActionState& actionState)  | _Pas encore documenté._
STD public ::p air\<std :: Vector\<std :: shared_ptr\<action\>\>, bool\> ComputeActionsWithRemoteState (ComputeEngineContext& Context, const DocumentState& localDocumentState, const DocumentState& remoteDocumentState, const ApplicationActionState& actionState)  |  Calcule les actions lors du choix entre l’État distant et l’état local.
public void NotifyCommittedActions (ComputeEngineContext& Context, const DocumentState& documentState, const ApplicationActionState& actionState)  | _Pas encore documenté._
public const std :: shared_ptr\<étiquette\>& GetDefaultLabel () const  | _Pas encore documenté._
public const std::string& GetMoreInfoUrl() const  | _Pas encore documenté._
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
L’État est sélectionné à l’aide de cette priorité. Types de protection inconnus (modèle ou ad-hoc absents de la stratégie). L’état de protection est toujours préférable à l’état non protégé. L’état du document avec l’étiquette est préférable à un autre sans. Ordre des étiquettes, la valeur la plus élevée est préférée. Horodatage de l’étiquette, préférer le document étiqueté le plus récent. [DocumentState](class_mip_documentstate.md) LastModifiedTime implémenté éventuellement, préférer le fichier nouvellement modifié.

Paramètres :  
* **Context**: contexte du moteur de calcul. 


* **localDocumentState**: état du document local. 


* **remoteDocumentState**: état du document distant. 


* **actionState**: état d’action de l’application.



  
**Retourne**: les méthodes retournent une paire. tout d’abord contient une liste de l’action, le second est s’il doit être appliqué sur le local, si des actions fausses doivent être appliquées sur le document distant et que l’état du document doit être utilisé.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions fonction)
_Pas encore documenté._

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel fonction)
_Pas encore documenté._

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl fonction)
_Pas encore documenté._

  
### <a name="computeengine-function"></a>~ ComputeEngine fonction)
_Pas encore documenté._
