---
title: mip::ProtectionProfile, classe
description: Documente la classe MIP ::p rotectionprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a6c78e7311f3af3920df19d7a3a6ca92bb09e819
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560059"
---
# <a name="class-mipprotectionprofile"></a>mip::ProtectionProfile, classe 
ProtectionProfile est la classe racine pour effectuer des opérations de protection.
Une application doit créer un ProtectionProfile avant d’effectuer des opérations de protection
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie.
public void ListEnginesAsync (const std :: shared_ptr\<void\>& Context)  |  Démarre une opération d’énumération de moteurs.
public std::vector\<std::string\> ListEngines()  |  Répertorie les moteurs.
public void AddEngineAsync (const ProtectionEngine :: Settings & Settings, const std :: shared_ptr\<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de protection au profil.
public std :: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine :: Settings & Settings)  |  Ajoute un nouveau moteur de protection au profil.
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr\<void\>& context)  |  Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
public void DeleteEngine(const std::string& engineId)  |  Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.
public static MIP_API void __CDECL MIP ::P rotectionProfile :: LoadAsync | Paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie
public static MIP_API std :: shared_ptr&lt;ProtectionProfile&gt; __CDECL MIP ::P rotectionProfile :: Load | Chargement d’un profil en fonction des paramètres fournis.
public static const MIP_API char * __CDECL MIP ::P rotectionProfile :: GetVersion | Obtient la version de la bibliothèque.
public static MIP_API std :: shared_ptr&lt;PublishingLicenseInfo&gt; __CDECL MIP ::P rotectionProfile :: GetPublishingLicenseInfo | Crée un conteneur pour les détails d’une licence de publication et peut être utilisé pour créer un gestionnaire de protection. 

## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtient les paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie.

  
**Retourne**: paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : contexte client qui est repassé de façon opaque aux observateurs


ProtectionProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="listengines-function"></a>ListEngines fonction)
Répertorie les moteurs.

  
**Retourne** : ID des moteurs mis en cache
  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de protection au profil.

Paramètres :  
* **paramètres**: l’objet mip ::P rotectionengine :: Settings qui spécifie les paramètres du moteur. 


* **context** : contexte client qui est repassé de façon opaque aux observateurs


ProtectionProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="addengine-function"></a>AddEngine fonction)
Ajoute un nouveau moteur de protection au profil.

Paramètres :  
* **paramètres**: l’objet mip ::P rotectionengine :: Settings qui spécifie les paramètres du moteur.



  
**Retourne**: ProtectionEngine nouvellement créé
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : contexte client qui est repassé de façon opaque aux observateurs


ProtectionProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengine-function"></a>DeleteEngine fonction)
Supprime le moteur de protection avec l’ID spécifié. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur.

### <a name="loadasync-function"></a>LoadAsync, fonction
Paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie 

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.

Paramètres :
* **paramètres**: paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie.
* **contexte**: ce même contexte sera transféré à ProtectionProfile :: observer :: OnLoadSuccess ou ProtectionProfile :: observer :: OnLoadFailure en l'.

### <a name="load-function"></a>Load, fonction
Chargement d’un profil en fonction des paramètres fournis.

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) est appelé en cas de réussite ou d’échec.

Paramètres :
* **paramètres**: paramètres utilisés par ProtectionProfile lors de son initialisation et tout au long de sa durée de vie.

**Retourne**: profil nouvellement créé.

### <a name="getversion-function"></a>GetVersion, fonction
Obtient la version de la bibliothèque. 

**Retourne**: version de la bibliothèque.

### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo fonction)
Crée un conteneur pour les détails d’une licence de publication et peut être utilisé pour créer un gestionnaire de protection. 

Paramètres :
* **serializedPublishingLicense**: la licence de publication sérialisée..

**Retourne**: un conteneur pour les détails d’une licence de publication 