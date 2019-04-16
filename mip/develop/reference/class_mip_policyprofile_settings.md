---
title: mip::PolicyProfile::Settings, classe
description: Décrit la classe mip::policyprofile de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d3105bd9c13e91108c44e847c3eae74f166c5e04
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573647"
---
# <a name="class-mippolicyprofilesettings"></a>mip::PolicyProfile::Settings, classe 
[Paramètres](class_mip_policyprofile_settings.md) utilisés par [PolicyProfile](class_mip_policyprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std::shared_ptr const std::string & chemin d’accès, useinmemorystorage : bool,\<authdelegate :\>& authdelegate :, const std::shared_ptr\<PolicyProfile::Observer\>& observer, const ApplicationInfo & applicationInfo)  |  Interface pour la configuration du profil.
public const std::string& GetPath() const  |  Obtenir le chemin de l’état stocké.
public bool GetUseInMemoryStorage() const  |  Obtenir l’indicateur d’utilisation de la mémoire de stockage.
public const std::shared_ptr\<AuthDelegate\>& GetAuthDelegate() const  |  Obtenir le délégué d’authentification.
public const std::shared_ptr\<PolicyProfile::Observer\>& GetObserver() const  |  Obtenir l’observateur d’événements.
public const ApplicationInfo GetApplicationInfo() const  |  Obtenir les informations sur l’application.
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public SetLoggerDelegate void (const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  Remplacer l’enregistreur d’événements par défaut.
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public SetHttpDelegate void (const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
public std::shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate() const  |  Obtenir le délégué TaskDispatcher (le cas échéant) fourni par l’application.
public SetTaskDispatcherDelegate void (const std::shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Remplacer la tâche d’asynchrone avec par défaut la distribution de gestion avec du client.
public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
public bool IsTelemetryOptedOut() const  |  Indique si la collecte des données de télémétrie doit être désactivée ou non.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.
public LogLevel GetMinimumLogLevel() const  |  Obtenir l’objet de niveau de journalisation minimum.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction de paramètres
Interface pour la configuration du profil.

Paramètres :  
* **Chemin d’accès**: Le chemin d’accès à un répertoire dans lequel le SDK stocke l’état de profil. 


* **useinmemorystorage :**: Store n’importe quel état mis en cache en mémoire plutôt que sur le disque. 


* **authDelegate**: Le délégué d’authentification utilisé par le SDK pour acquérir des jetons d’authentification. 


* **Observateur**: Une classe qui implémente le [PolicyProfile::Observer](class_mip_policyprofile_observer.md) interface. Peut être nullptr. 


* **applicationInfo**: Les identificateurs d’application utilisés pour l’accès au service.


  
### <a name="getpath-function"></a>GetPath (fonction)
Obtenir le chemin de l’état stocké.

  
**Retourne**: Chemin d’accès à l’état stocké.
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage (fonction)
Obtenir l’indicateur d’utilisation de la mémoire de stockage.

  
**Retourne**: True si l’utilisation dans la mémoire est définie ; sinon false.
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (fonction)
Obtenir le délégué d’authentification.

  
**Retourne**: Le délégué d’authentification.
  
### <a name="getobserver-function"></a>GetObserver (fonction)
Obtenir l’observateur d’événements.

  
**Retourne**: L’Observateur d’événements.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo (fonction)
Obtenir les informations sur l’application.

  
**Retourne**: Les informations sur l’application.
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate (fonction)
Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.

  
**Retourne**: Enregistreur d’événements
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate (fonction)
Remplacer l’enregistreur d’événements par défaut.

Paramètres :  
* **loggerDelegate**: Interface de rappel de journalisation implémentée par les applications clientes


Cette méthode doit être appelée par les applications clientes qui utilisent leur propre implémentation de l’enregistreur d’événements
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate function
Obtenir le délégué HTTP (le cas échéant) fourni par l’application.

  
**Retourne**: Délégué de HTTP à utiliser pour les opérations HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (fonction)
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate**: Interface de rappel HTTP implémentée par l’application cliente


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate (fonction)
Obtenir le délégué TaskDispatcher (le cas échéant) fourni par l’application.

  
**Retourne**: Délégué TaskDispatcher à utiliser pour l’exécution de tâches asynchrones
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate (fonction)
Remplacer la tâche d’asynchrone avec par défaut la distribution de gestion avec du client.

Paramètres :  
* **taskDispatcherDelegate**: Tâche de la distribution d’interface de rappel implémentée par l’application cliente


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry (fonction)
Refuse la collecte des données de télémétrie.
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut function
Indique si la collecte des données de télémétrie doit être désactivée ou non.

  
**Retourne**: True si la collecte des données de télémétrie doivent être désactivée ; sinon, false
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel (fonction)
Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.

Paramètres :  
* **logLevel** : niveau de journalisation minimum qui va déclencher un événement de journalisation. 



  
**Retourne**: True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel (fonction)
Obtenir l’objet de niveau de journalisation minimum.

  
**Retourne**: Niveau de journalisation minimum qui va déclencher un événement de journalisation.