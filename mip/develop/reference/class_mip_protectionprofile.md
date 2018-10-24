---
title: mip ProtectionProfile, classe
description: Informations de référence pour la classe mip ProtectionProfile
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7dffb4a6b1490ef185eb9a5062f394f4509f00a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446683"
---
# <a name="class-mipprotectionprofile"></a>mip::ProtectionProfile, classe 
[ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
Une application doit créer un [ProtectionProfile](class_mip_protectionprofile.md) avant d’effectuer des opérations de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtient les paramètres utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Démarre une opération d’énumération de moteurs.
public std::vector<std::string> ListEngines()  |  Répertorie les moteurs.
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Démarre l’ajout d’un nouveau moteur de protection au profil.
public std::shared_ptr<ProtectionEngine> AddEngine(const ProtectionEngine::Settings& settings)  |  Ajoute un nouveau moteur de protection au profil.
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
 public void DeleteEngine(const std::string& engineId)  |  Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtient les paramètres utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie.

  
**Retourne** : les [paramètres](class_mip_protectionprofile_settings.md) utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie
  
### <a name="listenginesasync"></a>ListEnginesAsync
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : contexte client qui est repassé de façon opaque aux observateurs


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="listengines"></a>ListEngines
Répertorie les moteurs.

  
**Retourne** : ID des moteurs mis en cache
  
### <a name="addengineasync"></a>AddEngineAsync
Démarre l’ajout d’un nouveau moteur de protection au profil.

Paramètres :  
* **settings** : objet [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) qui spécifie les paramètres du moteur. 


* **context** : contexte client qui est repassé de façon opaque aux observateurs


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="protectionengine"></a>ProtectionEngine
Ajoute un nouveau moteur de protection au profil.

Paramètres :  
* **settings** : objet [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) qui spécifie les paramètres du moteur.



  
**Retourne** : [ProtectionEngine](class_mip_protectionengine.md) nouvellement créé
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : contexte client qui est repassé de façon opaque aux observateurs


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengine"></a>DeleteEngine
Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur.

