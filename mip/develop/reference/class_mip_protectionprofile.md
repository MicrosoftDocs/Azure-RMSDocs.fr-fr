---
title: ProtectionProfile de classe
description: 'Documente la classe protectionprofile :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a783a90b64d5829632e2104ff2706fd86a0d9e68
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567109"
---
# <a name="class-protectionprofile"></a>ProtectionProfile de classe 
ProtectionProfile est la classe racine utilisée pour effectuer des opérations de protection.
Une application doit créer un ProtectionProfile avant d’effectuer des opérations de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie.
public std :: shared_ptr \<AsyncControl\> ListEnginesAsync (const std :: shared_ptr \<void\> contexte&)  |  Démarre une opération d’énumération de moteurs.
public std :: Vector \<std::string\> ListEngines ()  |  Répertorie les moteurs.
public std :: shared_ptr \<AsyncControl\> AddEngineAsync (const ProtectionEngine :: settings& Settings, const std :: shared_ptr \<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de protection au profil.
public std::shared_ptr\<ProtectionEngine\> AddEngine(const ProtectionEngine::Settings& settings)  |  Ajoute un nouveau moteur de protection au profil.
public std :: shared_ptr \<AsyncControl\> DeleteEngineAsync (const std :: string& engineId, const std :: shared_ptr \<void\>& Context)  |  Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
public void DeleteEngine(const std::string& engineId)  |  Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtient les paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie.

  
**Retourne**: paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : contexte client qui est repassé de façon opaque aux observateurs



  
**Retourne**: objet de contrôle asynchrone.
ProtectionProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="listengines-function"></a>ListEngines fonction)
Répertorie les moteurs.

  
**Retourne** : ID des moteurs mis en cache
  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de protection au profil.

Paramètres :  
* **settings** : objet mip::ProtectionEngine::Settings qui spécifie les paramètres du moteur. 


* **context** : contexte client qui est repassé de façon opaque aux observateurs



  
**Retourne**: objet de contrôle asynchrone.
ProtectionProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="addengine-function"></a>AddEngine fonction)
Ajoute un nouveau moteur de protection au profil.

Paramètres :  
* **settings** : objet mip::ProtectionEngine::Settings qui spécifie les paramètres du moteur.



  
**Retourne** : ProtectionEngine nouvellement créé
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **ID**: ID de moteur unique. 


* **context** : contexte client qui est repassé de façon opaque aux observateurs



  
**Retourne**: objet de contrôle asynchrone.
ProtectionProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengine-function"></a>DeleteEngine fonction)
Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **ID**: ID de moteur unique.

