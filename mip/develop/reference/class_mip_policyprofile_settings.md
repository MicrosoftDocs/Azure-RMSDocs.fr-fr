---
title: mip::PolicyProfile::Settings, classe
description: Documente la classe MIP ::p olicyprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 324b31a9589cff75a758da2936a3aba242fd63c2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560874"
---
# <a name="class-mippolicyprofilesettings"></a>mip::PolicyProfile::Settings, classe 
Paramètres utilisés par PolicyProfile lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Table des matières
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
public void SetTaskDispatcherDelegate (const std :: shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.
public void SetSessionId(const std::string& sessionId)  | Pas encore documenté.
public const std::string& GetSessionId() const  | Pas encore documenté.
public void SetCustomSettings (const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public ~Settings()  | Pas encore documenté.
  
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
Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.

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
