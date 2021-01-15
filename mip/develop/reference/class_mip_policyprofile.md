---
title: PolicyProfile de classe
description: 'Documente la classe policyprofile :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 89bac003d9a4924d5b854826b53eaa787f770a7c
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213366"
---
# <a name="class-policyprofile"></a>PolicyProfile de classe 
La classe PolicyProfile est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe PolicyProfile, mais elle peut créer plusieurs profils si nécessaire.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtenir les paramètres définis sur le profil.
public std :: shared_ptr \<AsyncControl\> ListEnginesAsync (const std :: shared_ptr \<void\> contexte&)  |  Démarre une opération d’énumération de moteurs.
public std :: Vector \<std::string\> ListEngines ()  |  Liste des moteurs.
public std :: shared_ptr \<AsyncControl\> UnloadEngineAsync (const std :: string& ID, const std :: shared_ptr \<void\>& Context)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public void UnloadEngine (const std :: String& ID)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public std :: shared_ptr \<AsyncControl\> AddEngineAsync (const PolicyEngine :: settings& Settings, const std :: shared_ptr \<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de stratégie au profil.
public std :: shared_ptr \<PolicyEngine\> AddEngine (const PolicyEngine :: settings& Settings, const std :: shared_ptr \<void\>& Context)  |  Ajoutez un nouveau moteur de stratégie au profil.
public std :: shared_ptr \<AsyncControl\> DeleteEngineAsync (const std :: string& ID, const std :: shared_ptr \<void\>& Context)  |  Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
public void DeleteEngine(const std::string& engineId)  |  Supprimer le moteur de stratégie avec l’ID donné. Toutes les données du moteur spécifié seront supprimées.
public void AcquireAuthToken (Cloud Cloud, const std :: shared_ptr \<AuthDelegate\>& authDelegate) const  |  Déclenchez un rappel d’authentification.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtenir les paramètres définis sur le profil.

  
**Retourne** : paramètres définis sur le profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


PolicyProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="listengines-function"></a>ListEngines fonction)
Liste des moteurs.

  
**Retourne** : ID des moteurs mis en cache
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync fonction)
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.

Paramètres :  
* **ID**: ID de moteur unique. 


* **context** : paramètre qui sera transféré de façon opaque vers les fonctions de l’observateur. 


PolicyProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengine-function"></a>UnloadEngine fonction)
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.

Paramètres :  
* **ID**: ID de moteur unique.


  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de stratégie au profil.

Paramètres :  
* **settings** : objet mip::PolicyEngine::Settings qui spécifie les paramètres du moteur. 


* **Context**: paramètre qui sera transféré de manière opaque aux fonctions observateur et aux HttpDelegate facultatifs. 


PolicyProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="addengine-function"></a>AddEngine fonction)
Ajoutez un nouveau moteur de stratégie au profil.

Paramètres :  
* **settings** : objet mip::PolicyEngine::Settings qui spécifie les paramètres du moteur. 


* **Context**: paramètre qui sera transféré de manière opaque au HttpDelegate facultatif



  
**Retourne**: PolicyEngine nouvellement créé
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.

Paramètres :  
* **ID**: ID de moteur unique. 


* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


PolicyProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengine-function"></a>DeleteEngine fonction)
Supprimer le moteur de stratégie avec l’ID donné. Toutes les données du moteur spécifié seront supprimées.

Paramètres :  
* **ID**: ID de moteur unique.


  
### <a name="acquireauthtoken-function"></a>AcquireAuthToken fonction)
Déclenchez un rappel d’authentification.

Paramètres :  
* **Cloud**: Cloud Azure 


* **authDelegate**: rappel d’authentification qui sera appelé


MIP ne met pas en cache ou ne fait rien d’autre avec la valeur retournée par le délégué auth. Cette fonction est recommandée pour les applications qui ne sont pas « connectées » jusqu’à ce que MIP demande un jeton d’authentification. Elle permet à une application d’extraire un jeton avant que MIP en ait réellement besoin.