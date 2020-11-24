---
title: 'classe ProtectionProfile :: Settings'
description: 'Documente la classe protectionprofile :: Settings du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 8808aeeea19c854ef72a9e6f91dd496906c2e2db
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567094"
---
# <a name="class-protectionprofilesettings"></a>classe ProtectionProfile :: Settings 
Settings utilisé par ProtectionProfile lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std :: shared_ptr \<MipContext\>& mipContext, cacheStorageType CacheStorageType, const std :: shared_ptr \<ConsentDelegate\>& consentDelegate, const std :: shared_ptr \<ProtectionProfile::Observer\>& observer)  |  Constructeur ProtectionProfile::Settings qui spécifie un observateur à utiliser pour les opérations asynchrones.
Paramètres publics (const std :: shared_ptr \<MipContext\>& mipContext, cacheStorageType CacheStorageType, const std :: shared_ptr \<ConsentDelegate\>& consentDelegate)  |  Constructeur ProtectionProfile::Settings utilisé pour les opérations synchrones.
public CacheStorageType GetCacheStorageType () const  |  Déterminez si les caches sont stockés dans la mémoire ou sur le disque.
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  Obtient le délégué de consentement utilisé pour la connexion aux services.
public std::shared_ptr\<ProtectionProfile::Observer\> GetObserver() const  |  Obtient l’observateur qui reçoit les notifications des événements liés à ProtectionProfile.
public std :: shared_ptr \<MipContext\> GetMipContext () const  |  Obtient le contexte MIP qui représente l’état partagé sur tous les profils.
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
public std :: shared_ptr \<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.
public void SetTaskDispatcherDelegate (const std :: shared_ptr \<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de la session.
public const std::string& GetSessionId() const  |  Obtient l’ID de session.
public void SetCanCacheLicenses (bool canCacheLicenses)  |  Configure si les licences utilisateur final (LUF) sont mises en cache localement.
public bool CanCacheLicenses () const  |  Obtient une valeur indiquant si les licences d’utilisateur final (LUF) sont mises en cache localement.
public void SetCustomSettings (const std :: Vector \<std::pair\<std::string, std::string\> \>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std :: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Constructeur ProtectionProfile::Settings qui spécifie un observateur à utiliser pour les opérations asynchrones.

Paramètres :  
* **mipContext**: paramètres de contexte globaux 


* **cacheStorageType**: stocker tout État mis en cache dans la mémoire ou sur le disque 


* **consentDelegate**: délégué utilisé pour obtenir l’autorisation de l’utilisateur pour accéder aux ressources externes 


* **Observateur**: instance observer qui recevra les notifications des événements liés à ProtectionProfile


* **applicationInfo** : informations sur l’application qui utilise le SDK de protection


  
### <a name="settings-function"></a>Fonction Settings
Constructeur ProtectionProfile::Settings utilisé pour les opérations synchrones.

Paramètres :  
* **mipContext**: paramètres de contexte globaux 


* **cacheStorageType**: stocker tout État mis en cache dans la mémoire ou sur le disque 


* **consentDelegate**: délégué utilisé pour obtenir l’autorisation de l’utilisateur pour accéder aux ressources externes 


* **applicationInfo** : informations sur l’application qui utilise le SDK de protection


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType fonction)
Déterminez si les caches sont stockés dans la mémoire ou sur le disque.

  
**Retourne**: type de stockage utilisé
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate fonction)
Obtient le délégué de consentement utilisé pour la connexion aux services.

  
**Retourne** : le délégué de consentement utilisé pour la connexion aux services
  
### <a name="getobserver-function"></a>GetObserver fonction)
Obtient l’observateur qui reçoit les notifications des événements liés à ProtectionProfile.

  
**Retourne**: observer qui reçoit des notifications d’événements liés à ProtectionProfile
  
### <a name="getmipcontext-function"></a>GetMipContext fonction)
Obtient le contexte MIP qui représente l’état partagé sur tous les profils.

  
**Retourne**: contexte MIP
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate fonction)
Obtenir le délégué HTTP (le cas échéant) fourni par l’application.

  
**Retourne**: le délégué http à utiliser pour les opérations http
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate fonction)
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate** : interface de rappel HTTP implémentée par l’application cliente


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate fonction)
Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.

  
**Retourne**: le délégué TaskDispatcher à utiliser pour l’exécution des tâches asynchrones
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate fonction)
Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.

Paramètres :  
* **taskDispatcherDelegate**: tâche distribuant l’interface de rappel implémentée par l’application cliente


les tâches peuvent faire référence à des objets de profil empêchant sa destruction, car les files d’attente taskdispatcher ne doivent pas être partagées.
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Définit l’ID de la session.

Paramètres :  
* **sessionId** : ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie


  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Obtient l’ID de session.

  
**Retourne** : ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses fonction)
Configure si les licences utilisateur final (LUF) sont mises en cache localement.

Paramètres :  
* **canCacheLicenses**: indique si le moteur doit mettre en cache une licence lors de l’ouverture du contenu protégé


Si la valeur est true, l’ouverture du contenu protégé met en cache la licence associée localement. Si la valeur est false, l’ouverture du contenu protégé effectue toujours l’opération HTTP pour acquérir la licence du service RMS.
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses fonction)
Obtient une valeur indiquant si les licences d’utilisateur final (LUF) sont mises en cache localement.

  
**Retourne**: configuration de la mise en cache de licences
  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings** : liste de paires nom/valeur.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

  
**Retourne** : liste de paires nom/valeur.