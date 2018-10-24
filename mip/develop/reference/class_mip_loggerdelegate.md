---
title: mip LoggerDelegate, classe
description: Informations de référence pour la classe mip LoggerDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b25cdb177735feccfa5c4d344613e4747d18b77f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445850"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath, LogLevel logLevel)  |  Initialiser l’enregistreur d’événements.
 public LogLevel GetLogLevel() const  |  Obtenir le niveau de journalisation le plus bas qui doit déclencher un événement de journalisation.
 public void Flush()  |  Vider le l’enregistreur d’événements.
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Écrire une instruction de journal dans le fichier journal.
  
## <a name="members"></a>Membres
  
### <a name="init"></a>Init
Initialiser l’enregistreur d’événements.

Paramètres :  
* **storagePath** : le chemin d’accès à l’emplacement où l’état persistant, notamment les journaux, peut être stocké. 


* **logLevel** : niveau de journalisation le plus bas qui doit déclencher un événement de journalisation.


  
### <a name="loglevel"></a>LogLevel
Obtenir le niveau de journalisation le plus bas qui doit déclencher un événement de journalisation.

  
**Retourne** : niveau de journalisation le plus bas qui doit déclencher un événement de journalisation.
  
### <a name="flush"></a>Purge
Vider le l’enregistreur d’événements.
  
### <a name="writetolog"></a>WriteToLog
Écrire une instruction de journal dans le fichier journal.

Paramètres :  
* **level** : niveau de journalisation pour l’instruction de journal. 


* **message** : message pour l’instruction de journal. 


* **function** : nom de la fonction pour l’instruction de journal. 


* **file** : nom du fichier où l’instruction de journal a été générée. 


* **line** : numéro de ligne où l’instruction de journal a été générée.

