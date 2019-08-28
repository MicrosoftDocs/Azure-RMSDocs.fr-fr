---
title: mip::ProtectionProfile, classe
description: Documente la classe MIP::p rotectionprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: aa660990885356f887bb310e7049d166e3bdc190
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057490"
---
# <a name="class-mipprotectionprofile"></a>mip::ProtectionProfile, classe 
[ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
Une application doit créer un [ProtectionProfile](class_mip_protectionprofile.md) avant d’effectuer des opérations de protection
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie.
public void ListEnginesAsync (const std:: shared_ptr\<void\>& Context)  |  Démarre une opération d’énumération de moteurs.
public std::vector\<std::string\> ListEngines()  |  Répertorie les moteurs.
public void AddEngineAsync (const ProtectionEngine:: Settings & Settings, const std:\<:\>shared_ptr void & Context)  |  Démarre l’ajout d’un nouveau moteur de protection au profil.
public std:: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine:: Settings & Settings)  |  Ajoute un nouveau moteur de protection au profil.
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr\<void\>& context)  |  Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
public void DeleteEngine(const std::string& engineId)  |  Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtient les paramètres utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie.

  
**Retourne**: [Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **contexte**: Contexte client qui sera retourné de manière opaque aux observateurs


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="listengines-function"></a>ListEngines fonction)
Répertorie les moteurs.

  
**Retourne**: ID de moteur mis en cache
  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de protection au profil.

Paramètres :  
* **settings** : objet [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) qui spécifie les paramètres du moteur. 


* **contexte**: Contexte client qui sera retourné de manière opaque aux observateurs


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengine-function"></a>AddEngine fonction)
Ajoute un nouveau moteur de protection au profil.

Paramètres :  
* **settings** : objet [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) qui spécifie les paramètres du moteur.



  
**Retourne**: [ProtectionEngine](class_mip_protectionengine.md) nouvellement créé
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur. 


* **contexte**: Contexte client qui sera retourné de manière opaque aux observateurs


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengine-function"></a>DeleteEngine fonction)
Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur.

