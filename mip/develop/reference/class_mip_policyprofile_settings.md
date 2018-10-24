---
title: mip PolicyProfile Settings, classe
description: Informations de référence pour la classe mip PolicyProfile Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 07cbcbc022c02a43f751e1cf55b5b0efdfb816d1
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446879"
---
# <a name="class-mippolicyprofilesettings"></a>mip::PolicyProfile::Settings, classe 
[Paramètres](class_mip_policyprofile_settings.md) utilisés par [PolicyProfile](class_mip_policyprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<PolicyProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interface pour la configuration du profil.
 public const std::string& GetPath() const  |  Obtenir le chemin de l’état stocké.
 public bool GetUseInMemoryStorage() const  |  Obtenir l’indicateur d’utilisation de la mémoire de stockage.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Obtenir le délégué d’authentification.
public const std::shared_ptr<PolicyProfile::Observer>& GetObserver() const  |  Obtenir l’observateur d’événements.
 public const ApplicationInfo GetApplicationInfo() const  |  Obtenir les informations sur l’application.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Remplacer l’enregistreur d’événements par défaut.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
 public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
 public bool IsTelemetryOptedOut() const  |  Indique si la collecte des données de télémétrie doit être désactivée ou non.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.
 public LogLevel GetMinimumLogLevel() const  |  Obtenir l’objet de niveau de journalisation minimum.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Interface pour la configuration du profil.

Paramètres :  
* **path** : chemin d’un répertoire dans lequel le SDK stocke l’état du profil. 


* **useInMemoryStorage** : stocker tout état mis en cache dans la mémoire plutôt que sur le disque. 


* **authDelegate** : délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification. 


* **observer** : classe qui implémente l’interface [PolicyProfile::Observer](class_mip_policyprofile_observer.md). Peut être nullptr. 


* **applicationInfo** : identificateurs d’application utilisés pour l’accès au service.


  
### <a name="getpath"></a>GetPath
Obtenir le chemin de l’état stocké.

  
**Retourne** : le chemin de l’état stocké.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtenir l’indicateur d’utilisation de la mémoire de stockage.

  
**Retourne** : true si l’utilisation en mémoire est définie ; sinon, false.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtenir le délégué d’authentification.

  
**Retourne** : le délégué d’authentification.
  
### <a name="policyprofileobserver"></a>PolicyProfile::Observer
Obtenir l’observateur d’événements.

  
**Retourne** : l’observateur d’événements.
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtenir les informations sur l’application.

  
**Retourne** : les informations sur l’application.
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.

  
**Retourne** : enregistreur d’événements
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Remplacer l’enregistreur d’événements par défaut.

Paramètres :  
* **loggerDelegate** : interface de rappel de journalisation implémentée par les applications clientes


Cette méthode doit être appelée par les applications clientes qui utilisent leur propre implémentation de l’enregistreur d’événements
  
### <a name="httpdelegate"></a>HttpDelegate
Obtenir le délégué HTTP (le cas échéant) fourni par l’application.

  
**Retourne** : délégué HTTP à utiliser pour les opérations HTTP
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate** : interface de rappel http implémentée par l’application cliente


  
### <a name="optouttelemetry"></a>OptOutTelemetry
Refuse la collecte des données de télémétrie.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Indique si la collecte des données de télémétrie doit être désactivée ou non.

  
**Retourne** : valeur indiquant si la collecte des données de télémétrie doit être désactivée ou non
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.

Paramètres :  
* **logLevel** : niveau de journalisation minimum qui va déclencher un événement de journalisation. 



  
**Retourne** : True
  
### <a name="loglevel"></a>LogLevel
Obtenir l’objet de niveau de journalisation minimum.

  
**Retourne** : niveau de journalisation minimum qui va déclencher un événement de journalisation.