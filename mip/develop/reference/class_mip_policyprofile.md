---
title: mip::PolicyProfile, classe
description: Documente la classe MIP ::p olicyprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8feb0b93982a00c4843ea914f969ef27cf8e5ca2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560915"
---
# <a name="class-mippolicyprofile"></a>mip::PolicyProfile, classe 
La classe PolicyProfile est la classe racine pour l’utilisation des opérations Microsoft Information Protection. Une application classique n’A besoin que d’un seul PolicyProfile, mais elle peut créer plusieurs profils si nécessaire.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtenir les paramètres définis sur le profil.
public void ListEnginesAsync (const std :: shared_ptr\<void\>& Context)  |  Démarre une opération d’énumération de moteurs.
public std::vector\<std::string\> ListEngines()  |  Liste des moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public void UnloadEngine (const std :: String & ID)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public void AddEngineAsync (const PolicyEngine :: Settings & Settings, const std :: shared_ptr\<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de stratégie au profil.
public std :: shared_ptr\<PolicyEngine\> AddEngine (const PolicyEngine :: Settings & Settings, const std :: shared_ptr\<void\>& Context)  |  Ajoutez un nouveau moteur de stratégie au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
public void DeleteEngine(const std::string& engineId)  |  Supprimer le moteur de stratégie avec l’ID donné. Toutes les données du moteur spécifié seront supprimées.
public static MIP_API void __CDECL MIP ::P olicyProfile :: LoadAsync | Démarre le chargement d’un profil en fonction des paramètres fournis.
public static const MIP_API char * __CDECL MIP ::P olicyProfile :: GetVersion | Obtient la version de la bibliothèque

## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtenir les paramètres définis sur le profil.

  
**Retourne** : paramètres définis sur le profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


PolicyProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="listengines-function"></a>ListEngines fonction)
Liste des moteurs.

  
**Retourne** : ID des moteurs mis en cache
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync fonction)
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera transféré de façon opaque vers les fonctions de l’observateur. 


PolicyProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengine-function"></a>UnloadEngine fonction)
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.

Paramètres :  
* **id** : ID unique du moteur.


  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de stratégie au profil.

Paramètres :  
* **paramètres**: l’objet mip ::P olicyengine :: Settings qui spécifie les paramètres du moteur. 


* **Context**: paramètre qui sera fowarded de manière opaque aux fonctions observateur et aux HttpDelegate facultatifs. 


PolicyProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="addengine-function"></a>AddEngine fonction)
Ajoutez un nouveau moteur de stratégie au profil.

Paramètres :  
* **paramètres**: l’objet mip ::P olicyengine :: Settings qui spécifie les paramètres du moteur. 


* **Context**: paramètre qui sera transféré de manière opaque au HttpDelegate facultatif



  
**Retourne**: PolicyEngine nouvellement créé
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


PolicyProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengine-function"></a>DeleteEngine fonction)
Supprimer le moteur de stratégie avec l’ID donné. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur.

### <a name="loadasync-function"></a>LoadAsync, fonction
Démarre le chargement d’un profil en fonction des paramètres fournis.

Paramètres :  
* **paramètres**: paramètres de profil utilisés pour charger l’objet de profil. </para>
* **Context**: paramètre de contexte qui sera passé dans les fonctions observateur.

### <a name="getversion-function"></a>GetVersion, fonction
Obtient la version de la bibliothèque

**Retourne**: une chaîne de version.