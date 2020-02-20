---
title: mip::PolicyProfile::Settings, classe
description: Documente la classe MIP ::p olicyprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 6c2d7f26e12f03bd886f2a3fedab8e0a3d976c45
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489756"
---
# <a name="class-mippolicyprofilesettings"></a>mip::PolicyProfile::Settings, classe 
Paramètres utilisés par PolicyProfile lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std :: shared_ptr\<MipContext\>& mipContext, CacheStorageType cacheStorageType, const std :: shared_ptr\<AuthDelegate\>& authDelegate, const std :: shared_ptr\<PolicyProfile :: observer\>& observer)  |  Interface pour la configuration du profil.
public CacheStorageType GetCacheStorageType () const  |  Déterminez si les caches sont stockés dans la mémoire ou sur le disque.
public const std :: shared_ptr\<AuthDelegate\>& GetAuthDelegate () const  |  Obtenir le délégué d’authentification.
public const std :: shared_ptr\<PolicyProfile :: observer\>& GetObserver () const  |  Obtenir l’observateur d’événements.
public std :: shared_ptr\<MipContext\> GetMipContext () const  |  Obtient le contexte MIP qui représente l’état partagé sur tous les profils.
public std :: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public void SetHttpDelegate (const std :: shared_ptr\<HttpDelegate\>& httpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
public std :: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.
public void SetTaskDispatcherDelegate (const std :: shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Remplacer la gestion de la répartition des tâches asynchrones par défaut avec le propriétaire du client.
public void SetSessionId(const std::string& sessionId)  | _Pas encore documenté._
public const std::string& GetSessionId() const  | _Pas encore documenté._
public void SetCustomSettings (const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetCustomSettings () const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public ~Settings()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Interface pour la configuration du profil.

Paramètres :  
* **mipContext**: paramètres de contexte globaux 


* **cacheStorageType**: stocker tout État mis en cache dans la mémoire ou sur le disque 


* **authDelegate** : délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification. 


* **observer**: classe implémentant l’interface PolicyProfile :: observer. Peut être nullptr.


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType fonction)
Déterminez si les caches sont stockés dans la mémoire ou sur le disque.

  
**Retourne**: type de stockage utilisé
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate fonction)
Obtenir le délégué d’authentification.

  
**Retourne** : le délégué d’authentification.
  
### <a name="getobserver-function"></a>GetObserver fonction)
Obtenir l’observateur d’événements.

  
**Retourne** : l’observateur d’événements.
  
### <a name="getmipcontext-function"></a>GetMipContext fonction)
Obtient le contexte MIP qui représente l’état partagé sur tous les profils.

  
**Retourne**: contexte MIP
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate fonction)
Obtenir le délégué HTTP (le cas échéant) fourni par l’application.

  
**Retourne** : délégué HTTP à utiliser pour les opérations HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate fonction)
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate** : interface de rappel http implémentée par l’application cliente


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate fonction)
Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.

  
**Retourne**: le délégué TaskDispatcher à utiliser pour l’exécution des tâches asynchrones
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate fonction)
Remplacer la gestion de la répartition des tâches asynchrones par défaut avec le propriétaire du client.

Paramètres :  
* **taskDispatcherDelegate**: tâche distribuant l’interface de rappel implémentée par l’application cliente


les tâches peuvent faire référence à des objets de profil empêchant sa destruction, car les files d’attente taskdispatcher ne doivent pas être partagées.
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
_Pas encore documenté._

  
### <a name="getsessionid-function"></a>GetSessionId fonction)
_Pas encore documenté._

  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings** : liste de paires nom/valeur.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

  
**Retourne** : liste de paires nom/valeur.
  
### <a name="settings-function"></a>~ Settings, fonction
_Pas encore documenté._
