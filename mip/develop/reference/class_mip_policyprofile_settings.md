---
title: 'classe PolicyProfile :: Settings'
description: 'Documente la classe policyprofile :: Settings du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2ec38a34f2522448704f1be91d03c62761cafdf6
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565600"
---
# <a name="class-policyprofilesettings"></a>classe PolicyProfile :: Settings 
Paramètres utilisés par PolicyProfile lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std :: shared_ptr \<MipContext\>& mipContext, cacheStorageType CacheStorageType, const std :: shared_ptr \<PolicyProfile::Observer\>& observer)  |  Interface pour la configuration du profil.
public CacheStorageType GetCacheStorageType () const  |  Déterminez si les caches sont stockés dans la mémoire ou sur le disque.
public const std :: shared_ptr \<PolicyProfile::Observer\>& GetObserver () const  |  Obtenir l’observateur d’événements.
public std :: shared_ptr \<MipContext\> GetMipContext () const  |  Obtient le contexte MIP qui représente l’état partagé sur tous les profils.
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
public std :: shared_ptr \<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.
public void SetTaskDispatcherDelegate (const std :: shared_ptr \<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Remplacer la gestion de la répartition des tâches asynchrones par défaut avec le propriétaire du client.
public void SetSessionId(const std::string& sessionId)  | _Pas encore documenté._
public const std::string& GetSessionId() const  | _Pas encore documenté._
public void SetCustomSettings (const std :: Vector \<std::pair\<std::string, std::string\> \>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std :: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public ~Settings()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Interface pour la configuration du profil.

Paramètres :  
* **mipContext**: paramètres de contexte globaux 


* **cacheStorageType**: stocker tout État mis en cache dans la mémoire ou sur le disque 


* **observer** : classe qui implémente l’interface PolicyProfile::Observer. Peut être nullptr.


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType fonction)
Déterminez si les caches sont stockés dans la mémoire ou sur le disque.

  
**Retourne**: type de stockage utilisé
  
### <a name="getobserver-function"></a>GetObserver fonction)
Obtenir l’observateur d’événements.

  
**Retourne** : l’observateur d’événements.
  
### <a name="getmipcontext-function"></a>GetMipContext fonction)
Obtient le contexte MIP qui représente l’état partagé sur tous les profils.

  
**Retourne**: contexte MIP
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate fonction)
Obtenir le délégué HTTP (le cas échéant) fourni par l’application.

  
**Retourne**: le délégué http à utiliser pour les opérations http
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate fonction)
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate**: interface de rappel http implémentée par l’application cliente


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate fonction)
Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.

  
**Retourne**: le délégué TaskDispatcher à utiliser pour l’exécution des tâches asynchrones
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate fonction)
Remplacer la gestion de la répartition des tâches asynchrones par défaut avec le propriétaire du client.

Paramètres :  
* **taskDispatcherDelegate**: tâche distribuant l’interface de rappel implémentée par l’application cliente


les tâches peuvent faire référence à des objets de profil empêchant sa destruction, car les files d’attente taskdispatcher ne doivent pas être partagées.
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Pas encore documenté.

  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Pas encore documenté.

  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings** : liste de paires nom/valeur.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

  
**Retourne** : liste de paires nom/valeur.
  
### <a name="settings-function"></a>~ Settings, fonction
Pas encore documenté.
