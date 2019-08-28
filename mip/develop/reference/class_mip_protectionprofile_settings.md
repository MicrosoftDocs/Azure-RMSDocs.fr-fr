---
title: mip::ProtectionProfile::Settings, classe
description: Documente la classe MIP::p rotectionprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f5c9d9fcd72f65b029c0a1af582b0f0cd498186e
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057482"
---
# <a name="class-mipprotectionprofilesettings"></a>mip::ProtectionProfile::Settings, classe 
[Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
paramètres publics (const std:: String & chemin, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\<ConsentDelegate\>& consentDelegate, const std:: shared_ptr\<ProtectionProfile:: observer\>& observateur, const ApplicationInfo & ApplicationInfo)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) qui spécifie un observateur à utiliser pour les opérations asynchrones.
paramètres publics (const std:: shared_ptr\<MipContext\>& MipContext, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\< ConsentDelegate\>& ConsentDelegate, const std:: shared_ptr\<ProtectionProfile:: observer\>& observer)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) qui spécifie un observateur à utiliser pour les opérations asynchrones.
paramètres publics (const std:: String & chemin, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\<ConsentDelegate\>& consentDelegate, const ApplicationInfo & applicationInfo)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) utilisé pour les opérations synchrones.
paramètres publics (const std:: shared_ptr\<MipContext\>& MipContext, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\< ConsentDelegate\>& ConsentDelegate)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) utilisé pour les opérations synchrones.
public const std::string& GetPath() const  |  Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.
public CacheStorageType GetCacheStorageType () const  |  Déterminez si les caches sont stockés dans la mémoire ou sur le disque.
public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate () const  |  Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.
public std:: shared_ptr\<ConsentDelegate\> GetConsentDelegate () const  |  Obtient le délégué de consentement utilisé pour la connexion aux services.
public std:: shared_ptr\<ProtectionProfile:: observer\> GetObserver () const  |  Obtient l’observateur qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).
public const ApplicationInfo& GetApplicationInfo() const  |  Obtient des informations sur l’application qui utilise le SDK de protection.
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  Obtient le contexte MIP qui représente l’état partagé sur tous les profils.
public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
public bool IsTelemetryOptedOut() const  |  Indique si la collecte des données de télémétrie doit être désactivée ou non.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& LoggerDelegate)  |  Remplacer l’enregistreur d’événements par défaut.
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& HttpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& TaskDispatcherDelegate)  |  Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de la session.
public const std::string& GetSessionId() const  |  Obtient l’ID de la session.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.
public LogLevel GetMinimumLogLevel() const  |  Obtenir l’objet de niveau de journalisation minimum.
public void SetCanCacheLicenses (bool canCacheLicenses)  |  Configure si les licences utilisateur final (LUF) sont mises en cache localement.
public bool CanCacheLicenses () const  |  Obtient une valeur indiquant si les licences d’utilisateur final (LUF) sont mises en cache localement.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) qui spécifie un observateur à utiliser pour les opérations asynchrones.

Paramètres :  
* **chemin d’accès**: Chemin de fichier sous lequel sont stockées les données de journalisation, de télémétrie et autres supports de protection 


* **cacheStorageType**: Stocker un État mis en cache dans la mémoire ou sur le disque 


* **authDelegate**: Objet de rappel à utiliser pour l’authentification, implémenté par l’application cliente 


* **consentDelegate**: Délégué utilisé pour obtenir l’autorisation de l’utilisateur pour accéder aux ressources externes 


* **Observateur**: Instance [Observateur](class_mip_protectionprofile_observer.md) qui recevra les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: Informations sur l’application qui consomme le kit de développement logiciel (SDK) de protection


> Déconseillé Ce constructeur sera bientôt déconseillé au profit d’un paramètre MIP:: MipContext
  
### <a name="settings-function"></a>Fonction Settings
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) qui spécifie un observateur à utiliser pour les opérations asynchrones.

Paramètres :  
* **mipContext**: Paramètres de contexte globaux 


* **cacheStorageType**: Stocker un État mis en cache dans la mémoire ou sur le disque 


* **authDelegate**: Objet de rappel à utiliser pour l’authentification, implémenté par l’application cliente 


* **consentDelegate**: Délégué utilisé pour obtenir l’autorisation de l’utilisateur pour accéder aux ressources externes 


* **Observateur**: Instance [Observateur](class_mip_protectionprofile_observer.md) qui recevra les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: Informations sur l’application qui consomme le kit de développement logiciel (SDK) de protection


  
### <a name="settings-function"></a>Fonction Settings
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) utilisé pour les opérations synchrones.

Paramètres :  
* **chemin d’accès**: Chemin de fichier sous lequel sont stockées les données de journalisation, de télémétrie et autres supports de protection 


* **cacheStorageType**: Stocker un État mis en cache dans la mémoire ou sur le disque 


* **authDelegate**: Objet de rappel à utiliser pour l’authentification, implémenté par l’application cliente 


* **consentDelegate**: Délégué utilisé pour obtenir l’autorisation de l’utilisateur pour accéder aux ressources externes 


* **applicationInfo**: Informations sur l’application qui consomme le kit de développement logiciel (SDK) de protection


Ce constructeur sera bientôt déconseillé au profit d’un paramètre MIP:: MipContext
  
### <a name="settings-function"></a>Fonction Settings
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) utilisé pour les opérations synchrones.

Paramètres :  
* **mipContext**: Paramètres de contexte globaux 


* **cacheStorageType**: Stocker un État mis en cache dans la mémoire ou sur le disque 


* **authDelegate**: Objet de rappel à utiliser pour l’authentification, implémenté par l’application cliente 


* **consentDelegate**: Délégué utilisé pour obtenir l’autorisation de l’utilisateur pour accéder aux ressources externes 


* **applicationInfo**: Informations sur l’application qui consomme le kit de développement logiciel (SDK) de protection


  
### <a name="getpath-function"></a>GetPath fonction)
Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.

  
**Retourne**: le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType fonction)
Déterminez si les caches sont stockés dans la mémoire ou sur le disque.

  
**Retourne**: Type de stockage utilisé
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate fonction)
Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.

  
**Retourne**: Délégué d’authentification utilisé pour acquérir des jetons d’authentification
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate fonction)
Obtient le délégué de consentement utilisé pour la connexion aux services.

  
**Retourne**: Délégué de consentement utilisé pour la connexion aux services
  
### <a name="getobserver-function"></a>GetObserver fonction)
Obtient l’observateur qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).

  
**Retourne**: [Observateur](class_mip_protectionprofile_observer.md) qui reçoit des notifications d’événements liés à [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo fonction)
Obtient des informations sur l’application qui utilise le SDK de protection.

  
**Retourne**: Informations sur l’application qui consomme le kit de développement logiciel (SDK) de protection
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="getmipcontext-function"></a>GetMipContext fonction)
Obtient le contexte MIP qui représente l’état partagé sur tous les profils.

  
**Retourne**: Contexte MIP
  
### <a name="optouttelemetry-function"></a>OptOutTelemetry fonction)
Refuse la collecte des données de télémétrie.
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut fonction)
Indique si la collecte des données de télémétrie doit être désactivée ou non.

  
**Retourne**: Si la collecte de données de télémétrie doit être désactivée ou non
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
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

  
**Retourne**: Délégué HTTP à utiliser pour les opérations HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate fonction)
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate**: Interface de rappel HTTP implémentée par l’application cliente


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate fonction)
Obtient le délégué TaskDispatcher (le cas échéant) fourni par l’application.

  
**Retourne**: Délégué TaskDispatcher à utiliser pour l’exécution de tâches asynchrones
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate fonction)
Remplacez la tâche asynchonous par défaut en rétribuant la gestion avec le propriétaire du client.

Paramètres :  
* **taskDispatcherDelegate**: Interface de rappel de répartition des tâches implémentée par l’application cliente


  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Définit l’ID de la session.

Paramètres :  
* **SessionID**: ID de session qui sera utilisé pour mettre en corrélation les journaux/la télémétrie


  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Obtient l’ID de la session.

  
**Retourne**: ID de session qui sera utilisé pour mettre en corrélation les journaux/la télémétrie
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel fonction)
Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.

Paramètres :  
* **logLevel** : niveau de journalisation minimum qui va déclencher un événement de journalisation.


> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel fonction)
Obtenir l’objet de niveau de journalisation minimum.

  
**Retourne**: Niveau de journalisation minimal qui déclenchera un événement de journalisation.
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de l’obtention ou de la définition des données de contexte communes via MIP:: MipContext.
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses fonction)
Configure si les licences utilisateur final (LUF) sont mises en cache localement.

Paramètres :  
* **canCacheLicenses**: Indique si le moteur doit mettre en cache une licence lors de l’ouverture du contenu protégé


Si la valeur est true, l’ouverture du contenu protégé met en cache la licence associée localement. Si la valeur est false, l’ouverture du contenu protégé effectue toujours l’opération HTTP pour acquérir la licence du service RMS.
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses fonction)
Obtient une valeur indiquant si les licences d’utilisateur final (LUF) sont mises en cache localement.

  
**Retourne**: Configuration de la mise en cache des licences