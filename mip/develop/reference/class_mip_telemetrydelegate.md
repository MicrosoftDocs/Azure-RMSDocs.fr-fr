---
title: TelemetryDelegate de classe
description: 'Documente la classe telemetrydelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 40e9c3a695f70af8051ef2a6e89ad232a7c09f54
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224957"
---
# <a name="class-telemetrydelegate"></a>TelemetryDelegate de classe 
Classe qui définit l’interface pour les notifications d’audit/de télémétrie du kit de développement logiciel (SDK) MIP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void WriteEvent (const std :: shared_ptr \<TelemetryEvent\>& Event)  |  Consigner un événement de diagnostic.
public void Flush()  |  Vider les événements mis en file d’attente (par exemple, en raison de l’arrêt)
  
## <a name="members"></a>Membres
  
### <a name="writeevent-function"></a>Fonction WriteEvent
Consigner un événement de diagnostic.

Paramètres :  
* **événement**: événement à journaliser


  
### <a name="flush-function"></a>Flush, fonction
Vider les événements mis en file d’attente (par exemple, en raison de l’arrêt)