---
title: LoggerDelegate de classe
description: 'Documente la classe loggerdelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: e213f243a0e46bb804b224c7a0752a0b9b270103
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761815"
---
# <a name="class-loggerdelegate"></a>LoggerDelegate de classe 
Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  Initialiser l’enregistreur d’événements.
public void Flush()  |  Vider le l’enregistreur d’événements.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Écrire une instruction de journal dans le fichier journal.
  
## <a name="members"></a>Membres
  
### <a name="init-function"></a>Fonction init
Initialiser l’enregistreur d’événements.

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

