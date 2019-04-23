---
title: class mip::LoggerDelegate
description: Décrit la classe mip::loggerdelegate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 511c8dabc8ff31c70c8343a80d423b76c43fa946
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184618"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
Une classe qui définit l’interface de l’enregistreur d’événements SDK MIP.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath, LogLevel logLevel)  |  Initialiser l’enregistreur d’événements.
public LogLevel GetLogLevel() const  |  Obtenir le niveau de journalisation le plus bas qui doit déclencher un événement de journalisation.
public void Flush()  |  Vider le l’enregistreur d’événements.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Écrire une instruction de journal dans le fichier journal.
  
## <a name="members"></a>Membres
  
### <a name="init-function"></a>Init (fonction)
Initialiser l’enregistreur d’événements.

Paramètres :  
* **storagePath** : le chemin d’accès à l’emplacement où l’état persistant, notamment les journaux, peut être stocké. 


* **logLevel** : niveau de journalisation le plus bas qui doit déclencher un événement de journalisation.


  
### <a name="getloglevel-function"></a>GetLogLevel (fonction)
Obtenir le niveau de journalisation le plus bas qui doit déclencher un événement de journalisation.

  
**Retourne**: Le niveau de journalisation la plus basse qui déclenche un événement de journalisation.
  
### <a name="flush-function"></a>Flush (fonction)
Vider le l’enregistreur d’événements.
  
### <a name="writetolog-function"></a>WriteToLog (fonction)
Écrire une instruction de journal dans le fichier journal.

Paramètres :  
* **level** : niveau de journalisation pour l’instruction de journal. 


* **message** : message pour l’instruction de journal. 


* **function** : nom de la fonction pour l’instruction de journal. 


* **file** : nom du fichier où l’instruction de journal a été générée. 


* **line** : numéro de ligne où l’instruction de journal a été générée.

