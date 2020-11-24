---
title: LoggerDelegate de classe
description: 'Documente la classe loggerdelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 48b01649d3c9b3e8089294d0012fa6393362e98e
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565688"
---
# <a name="class-loggerdelegate"></a>LoggerDelegate de classe 
Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  Initialise l’enregistreur d’événements.
public void Flush()  |  Vider le l’enregistreur d’événements.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Écrire une instruction de journal dans le fichier journal.
  
## <a name="members"></a>Membres
  
### <a name="init-function"></a>Fonction init
Initialise l’enregistreur d’événements.

Paramètres :  
* **storagePath** : le chemin d’accès à l’emplacement où l’état persistant, notamment les journaux, peut être stocké.


  
### <a name="flush-function"></a>Flush, fonction
Vider le l’enregistreur d’événements.
  
### <a name="writetolog-function"></a>WriteToLog fonction)
Écrire une instruction de journal dans le fichier journal.

Paramètres :  
* **level** : niveau de journalisation pour l’instruction de journal. 


* **message** : message pour l’instruction de journal. 


* **function** : nom de la fonction pour l’instruction de journal. 


* **file** : nom du fichier où l’instruction de journal a été générée. 


* **line** : numéro de ligne où l’instruction de journal a été générée.

