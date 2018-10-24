---
title: mip FileProfile Settings, classe
description: Informations de référence pour la classe mip FileProfile Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 4b79d8eb75a54a56f1b3e48645bdd5eec0afaa19
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446377"
---
# <a name="class-mipfileprofilesettings"></a>mip::FileProfile::Settings, classe 
[Settings](class_mip_fileprofile_settings.md) utilisé par [FileProfile](class_mip_fileprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md).
 public const std::string& GetPath() const  |  Obtient le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant.
 public bool GetUseInMemoryStorage() const  |  Détermine si tous les états doivent être stockés dans la mémoire (plutôt que sur le disque)
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Obtient le délégué de consentement utilisé pour demander le consentement de l’utilisateur pour la connexion aux services.
public std::shared_ptr<Observer> GetObserver() const  |  Obtient l’observateur qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md).
 public const ApplicationInfo GetApplicationInfo() const  |  Obtient des informations sur l’application qui utilise le SDK.
 public bool GetSkipTelemetryInit() const  |  Indique si l’initialisation de la télémétrie doit être ignorée ou non.
 public void SetSkipTelemetryInit()  |  Désactive l’initialisation de la télémétrie.
 public void SetNewFeaturesDisabled()  |  Désactive les nouvelles fonctionnalités.
 public bool AreNewFeaturesDisabled() const  |  Indique si les nouvelles fonctionnalités sont désactivées ou non.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Remplacer l’enregistreur d’événements par défaut.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
 public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
 public bool IsTelemetryOptedOut() const  |  Indique si la collecte des données de télémétrie doit être désactivée ou non.
 public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de la session.
 public const std::string& GetSessionId() const  |  Obtient l’ID de la session.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Définir le niveau de journalisation le plus bas qui va déclencher un événement de journalisation.
 public LogLevel GetMinimumLogLevel() const  |  Obtenir le niveau de journalisation le plus bas qui va déclencher un événement de journalisation.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md).

Paramètres :  
* **path** : le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant 


* **useInMemoryStorage** : True si tous les états doivent être stockés dans la mémoire, False si l’état peut être mis en cache sur le disque 


* **authDelegate** : le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification 


* **observer** : instance de [l’observateur](class_mip_fileprofile_observer.md) qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md)


* **applicationInfo** : informations sur l’application qui utilise le SDK


  
### <a name="getpath"></a>GetPath
Obtient le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant.

  
**Retourne** : le chemin où sont stockés les informations de journalisation, les données de télémétrie et l’état persistant
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Détermine si tous les états doivent être stockés dans la mémoire (plutôt que sur le disque)

  
**Retourne** : valeur indiquant si tous les états doivent être stockés dans la mémoire (plutôt que sur le disque)
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.

  
**Retourne** : le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification
  
### <a name="consentdelegate"></a>ConsentDelegate
Obtient le délégué de consentement utilisé pour demander le consentement de l’utilisateur pour la connexion aux services.

  
**Retourne** : le délégué consentement utilisé pour demander le consentement de l’utilisateur
  
### <a name="observer"></a>Observateur
Obtient l’observateur qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md).

  
**Retourne** : [observateur](class_mip_fileprofile_observer.md) qui reçoit les notifications des événements liés à [FileProfile](class_mip_fileprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtient des informations sur l’application qui utilise le SDK.

  
**Retourne** : informations sur l’application qui utilise le SDK
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Indique si l’initialisation de la télémétrie doit être ignorée ou non.

  
**Retourne** : valeur indiquant si l’initialisation de la télémétrie doit être ignorée ou non
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Désactive l’initialisation de la télémétrie.
Cette méthode n’est généralement pas appelée par les applications clientes, mais plutôt utilisée par le SDK de fichier pour empêcher l’initialisation en double
  
### <a name="setnewfeaturesdisabled"></a>SetNewFeaturesDisabled
Désactive les nouvelles fonctionnalités.
Pour les applications qui ne veulent pas essayer de nouvelles fonctionnalités
  
### <a name="arenewfeaturesdisabled"></a>AreNewFeaturesDisabled
Indique si les nouvelles fonctionnalités sont désactivées ou non.

  
**Retourne** : valeur indiquant si les nouvelles fonctionnalités sont désactivées ou non
  
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
* **httpDelegate** : interface de rappel HTTP implémentée par l’application cliente


  
### <a name="optouttelemetry"></a>OptOutTelemetry
Refuse la collecte des données de télémétrie.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Indique si la collecte des données de télémétrie doit être désactivée ou non.

  
**Retourne** : valeur indiquant si la collecte des données de télémétrie doit être désactivée ou non
  
### <a name="setsessionid"></a>SetSessionId
Définit l’ID de la session.

Paramètres :  
* **sessionId** : ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie


  
### <a name="getsessionid"></a>GetSessionId
Obtient l’ID de la session.

  
**Retourne** : ID de session à utiliser pour mettre en corrélation des journaux et la télémétrie
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
Définir le niveau de journalisation le plus bas qui va déclencher un événement de journalisation.

Paramètres :  
* **logLevel** : niveau de journalisation le plus bas qui va déclencher un événement de journalisation. 



  
**Retourne** : True
  
### <a name="loglevel"></a>LogLevel
Obtenir le niveau de journalisation le plus bas qui va déclencher un événement de journalisation.

  
**Retourne** : niveau de journalisation le plus bas qui va déclencher un événement de journalisation.