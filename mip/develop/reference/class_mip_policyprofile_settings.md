---
title: mip::PolicyProfile::Settings, classe
description: Documente la classe MIP::p olicyprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2edec96a34b6885aa6c38477d36e401ebc49242a
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055661"
---
# <a name="class-mippolicyprofilesettings"></a>mip::PolicyProfile::Settings, classe 
[Paramètres](class_mip_policyprofile_settings.md) utilisés par [PolicyProfile](class_mip_policyprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
paramètres publics (const std:: String & chemin, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\<PolicyProfile:: observer\> & observateur, const ApplicationInfo & applicationInfo)  |  Interface pour la configuration du profil.
paramètres publics (const std:: shared_ptr\<MipContext\>& MipContext, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\< PolicyProfile:: observer\>& observer)  |  Interface pour la configuration du profil.
public const std::string& GetPath() const  |  Obtenir le chemin de l’état stocké.
public CacheStorageType GetCacheStorageType () const  |  Déterminez si les caches sont stockés dans la mémoire ou sur le disque.
public const std:: shared_ptr\<AuthDelegate\>& GetAuthDelegate () const  |  Obtenir le délégué d’authentification.
public const std:: shared_ptr\<PolicyProfile:: observer\>& GetObserver () const  |  Obtenir l’observateur d’événements.
public const ApplicationInfo& GetApplicationInfo() const  |  Obtenir les informations sur l’application.
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  Obtient le contexte MIP qui représente l’état partagé sur tous les profils.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& LoggerDelegate)  |  Remplacer l’enregistreur d’événements par défaut.
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& HttpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& TaskDispatcherDelegate)  |  Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.
public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
public bool IsTelemetryOptedOut() const  |  Indique si la collecte des données de télémétrie doit être désactivée ou non.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.
public LogLevel GetMinimumLogLevel() const  |  Obtenir l’objet de niveau de journalisation minimum.
public void SetSessionId(const std::string& sessionId)  | _Pas encore documenté._
public const std::string& GetSessionId() const  | _Pas encore documenté._
public ~Settings()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Interface pour la configuration du profil.

Paramètres :  
* **chemin d’accès**: Chemin d’accès à un répertoire dans lequel le kit de développement logiciel (SDK) stocke l’état du profil. 


* **cacheStorageType**: Stocker un État mis en cache dans la mémoire ou sur le disque 


* **authDelegate**: Délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification. 


* **Observateur**: Classe implémentant l’interface [PolicyProfile:: observer](class_mip_policyprofile_observer.md) . Peut être nullptr. 


* **applicationInfo**: Identificateurs d’application utilisés pour l’accès au service.


> Déconseillé Ce constructeur sera bientôt déconseillé au profit d’un paramètre MIP:: MipContext
  
### <a name="settings-function"></a>Fonction Settings
Interface pour la configuration du profil.

Paramètres :  
* **mipContext**: Paramètres de contexte globaux 


* **cacheStorageType**: Stocker un État mis en cache dans la mémoire ou sur le disque 


* **authDelegate**: Délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification. 


* **Observateur**: Classe implémentant l’interface [PolicyProfile:: observer](class_mip_policyprofile_observer.md) . Peut être nullptr.


  
### <a name="getpath-function"></a>GetPath fonction)
Obtenir le chemin de l’état stocké.

  
**Retourne**: Chemin d’accès à l’État stocké.
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType fonction)
Déterminez si les caches sont stockés dans la mémoire ou sur le disque.

  
**Retourne**: Type de stockage utilisé
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate fonction)
Obtenir le délégué d’authentification.

  
**Retourne**: Délégué d’authentification.
  
### <a name="getobserver-function"></a>GetObserver fonction)
Obtenir l’observateur d’événements.

  
**Retourne**: Observateur d’événements.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo fonction)
Obtenir les informations sur l’application.

  
**Retourne**: Informations sur l’application.
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="getmipcontext-function"></a>GetMipContext fonction)
Obtient le contexte MIP qui représente l’état partagé sur tous les profils.

  
**Retourne**: Contexte MIP
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate fonction)
Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.

  
**Retourne**: Enregistreur
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate fonction)
Remplacer l’enregistreur d’événements par défaut.

Paramètres :  
* **loggerDelegate**: Interface de rappel d’enregistrement implémentée par les applications clientes


Cette méthode doit être appelée par les applications clientes qui utilisent leur propre implémentation de l’enregistreur d’événements 
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate fonction)
Obtenir le délégué HTTP (le cas échéant) fourni par l’application.

  
**Retourne**: Délégué http à utiliser pour les opérations HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate fonction)
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate**: Interface de rappel http implémentée par l’application cliente


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate fonction)
Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.

  
**Retourne**: Délégué TaskDispatcher à utiliser pour l’exécution de tâches asynchrones
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate fonction)
Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.

Paramètres :  
* **taskDispatcherDelegate**: Interface de rappel de répartition des tâches implémentée par l’application cliente


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry fonction)
Refuse la collecte des données de télémétrie.
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut fonction)
Indique si la collecte des données de télémétrie doit être désactivée ou non.

  
**Retourne**: True si la collecte de données de télémétrie doit être désactivée, sinon false
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel fonction)
Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.

Paramètres :  
* **logLevel** : niveau de journalisation minimum qui va déclencher un événement de journalisation.


> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel fonction)
Obtenir l’objet de niveau de journalisation minimum.

  
**Retourne**: Niveau de journalisation minimal qui déclenchera un événement de journalisation.
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
_Pas encore documenté._

  
### <a name="getsessionid-function"></a>GetSessionId fonction)
_Pas encore documenté._

  
### <a name="settings-function"></a>~ Settings, fonction
_Pas encore documenté._
