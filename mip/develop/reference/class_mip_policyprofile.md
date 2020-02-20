---
title: mip::PolicyProfile, classe
description: Documente la classe MIP ::p olicyprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 515f780c269025175e99caed72e8da381ef88104
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489773"
---
# <a name="class-mippolicyprofile"></a>mip::PolicyProfile, classe 
La classe PolicyProfile est la classe racine pour l’utilisation des opérations Microsoft Information Protection. Une application classique n’A besoin que d’un seul PolicyProfile, mais elle peut créer plusieurs profils si nécessaire.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtenir les paramètres définis sur le profil.
public std :: shared_ptr\<AsyncControl\> ListEnginesAsync (const std :: shared_ptr\<void\>& contexte)  |  Démarre une opération d’énumération de moteurs.
public std :: Vector\<std :: String\> ListEngines ()  |  Liste des moteurs.
public std :: shared_ptr\<AsyncControl\> UnloadEngineAsync (const std :: String & ID, const std :: shared_ptr\<void\>contexte &)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public void UnloadEngine (const std :: String & ID)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public std :: shared_ptr\<AsyncControl\> AddEngineAsync (const PolicyEngine :: Settings & Settings, const std :: shared_ptr\<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de stratégie au profil.
public std :: shared_ptr\<PolicyEngine\> AddEngine (const PolicyEngine :: Settings & Settings, const std :: shared_ptr\<void\>& Context)  |  Ajoutez un nouveau moteur de stratégie au profil.
public std :: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std :: String & ID, const std :: shared_ptr\<void\>contexte &)  |  Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
public void DeleteEngine(const std::string& engineId)  |  Supprimer le moteur de stratégie avec l’ID donné. Toutes les données du moteur spécifié seront supprimées.
  
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


* **Context**: paramètre qui sera transféré de manière opaque aux fonctions observateur et aux HttpDelegate facultatifs. 


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

