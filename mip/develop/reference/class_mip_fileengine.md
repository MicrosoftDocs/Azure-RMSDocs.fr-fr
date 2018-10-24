---
title: mip FileEngine, classe
description: Informations de référence pour la classe mip FileEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7342edf27b19f43881b2e8d378fa243d26f7056
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446071"
---
# <a name="class-mipfileengine"></a>mip::FileEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Retourne les paramètres du moteur.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Retourne une liste d’étiquettes de sensibilité.
 public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
 public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté.
public void CreateFileHandlerAsync(const std::string& inputFilePath, const ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.
public void CreateFileHandlerAsync(const std::shared_ptr<Stream>& inputStream, const std::string& inputFilePath, const mip::ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Retourne les paramètres du moteur.
  
### <a name="label"></a>Étiquette
Retourne une liste d’étiquettes de sensibilité.
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne** : URL au format de chaîne.
  
### <a name="islabelingrequired"></a>IsLabelingRequired
Vérifie si la stratégie détermine qu’un document doit être étiqueté.

  
**Retourne** : True si l’étiquetage est obligatoire ; sinon, False.
  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.

Paramètres :  
* **The** : fichier à ouvrir. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **contentState** : état du contenu pendant que l’application interagit avec celui-ci. 


* **A** : classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context** : contexte client qui est repassé de façon opaque à l’observateur.


  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.

Paramètres :  
* **inputStream** : flux contenant les données de fichier. 


* **inputFilePath** : chemin du fichier. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **contentState** : état du contenu pendant que l’application interagit avec celui-ci. 


* **fileHandlerObserver** : classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context** : contexte client qui est repassé de façon opaque à l’observateur.


  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **level** : description du niveau de journalisation : Info/Erreur/Avertissement 


* **eventType** : description du type d’événement 


* **eventData** : données associées à l’événement

