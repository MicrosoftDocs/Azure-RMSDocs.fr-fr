---
title: mip::ProtectionProfile::Settings, classe
description: Décrit la classe mip::protectionprofile de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 5e609cfbc7cbb705dafbee239726c0cfd15cc38a
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331866"
---
# <a name="class-mipprotectionprofilesettings"></a>mip::ProtectionProfile::Settings, classe 
[Settings](class_mip_protectionprofile_settings.md) utilisé par [ProtectionProfile](class_mip_protectionprofile.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std::shared_ptr const std::string & chemin d’accès, useinmemorystorage : bool,\<authdelegate :\>& authdelegate :, const std::shared_ptr\<ConsentDelegate\>& consentDelegate const std::shared_ptr\<ProtectionProfile::Observer\>& observer, const ApplicationInfo & applicationInfo)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) qui spécifie un observateur à utiliser pour les opérations asynchrones.
Paramètres publics (const std::shared_ptr const std::string & chemin d’accès, useinmemorystorage : bool,\<authdelegate :\>& authdelegate :, const std::shared_ptr\<ConsentDelegate\>& consentDelegate const ApplicationInfo & applicationInfo)  |  Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) utilisé pour les opérations synchrones.
public const std::string& GetPath() const  |  Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.
public bool GetUseInMemoryStorage() const  |  Savoir si les caches sont stockés en mémoire uniquement (plutôt que sur le disque)
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  Obtient le délégué de consentement utilisé pour la connexion aux services.
public std::shared_ptr\<ProtectionProfile::Observer\> GetObserver() const  |  Obtient l’observateur qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).
public const ApplicationInfo& GetApplicationInfo() const  |  Obtient des informations sur l’application qui utilise le SDK de protection.
public void OptOutTelemetry()  |  Refuse la collecte des données de télémétrie.
public bool IsTelemetryOptedOut() const  |  Indique si la collecte des données de télémétrie doit être désactivée ou non.
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  Obtenir le délégué d’enregistreur d’événements (le cas échéant) fourni par l’application.
public SetLoggerDelegate void (const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  Remplacer l’enregistreur d’événements par défaut.
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Obtenir le délégué HTTP (le cas échéant) fourni par l’application.
public SetHttpDelegate void (const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  Remplacer la pile HTTP par défaut par celle du client.
public bool GetSkipTelemetryInit() const  |  Indique si l’initialisation de la télémétrie doit être ignorée ou non.
public void SetSkipTelemetryInit()  |  Désactive l’initialisation de la télémétrie.
public void SetNewFeaturesDisabled()  |  Désactive les nouvelles fonctionnalités.
public bool AreNewFeaturesDisabled() const  |  Indique si les nouvelles fonctionnalités sont désactivées ou non.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de la session.
public const std::string& GetSessionId() const  |  Obtient l’ID de la session.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.
public LogLevel GetMinimumLogLevel() const  |  Obtenir l’objet de niveau de journalisation minimum.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction de paramètres
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) qui spécifie un observateur à utiliser pour les opérations asynchrones.

Paramètres :  
* **Chemin d’accès**: Chemin d’accès de fichier sous l’enregistrement, données de télémétrie et les autres informations relatives à la protection est stockée. 


* **useinmemorystorage :**: Store n’importe quel état mis en cache en mémoire plutôt que sur le disque 


* **authDelegate**: Objet de rappel à utiliser pour l’authentification, implémentée par l’application cliente 


* **Observateur**: [Observateur](class_mip_protectionprofile_observer.md) instance qui recevra les notifications d’événements liés à [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: Plus d’informations sur l’application qui utilise le Kit de développement logiciel de protection


  
### <a name="settings-function"></a>Fonction de paramètres
Constructeur [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) utilisé pour les opérations synchrones.

Paramètres :  
* **Chemin d’accès**: Chemin d’accès de fichier sous l’enregistrement, données de télémétrie et les autres informations relatives à la protection est stockée. 


* **useinmemorystorage :**: Store n’importe quel état mis en cache en mémoire plutôt que sur le disque 


* **authDelegate**: Objet de rappel à utiliser pour l’authentification, implémentée par l’application cliente 


* **applicationInfo**: Plus d’informations sur l’application qui utilise le SDK de protection


  
### <a name="getpath-function"></a>GetPath (fonction)
Obtient le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection.

  
**Retourne**: le chemin où sont stockées les informations de journalisation, les données de télémétrie et autres informations relatives à la protection
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage (fonction)
Savoir si les caches sont stockés en mémoire uniquement (plutôt que sur le disque)

  
**Retourne**: True si les caches sont stockés en mémoire uniquement
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (fonction)
Obtient le délégué d’authentification utilisé pour l’acquisition des jetons d’authentification.

  
**Retourne**: Délégué d’authentification utilisé pour l’acquisition des jetons d’authentification
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate (fonction)
Obtient le délégué de consentement utilisé pour la connexion aux services.

  
**Retourne**: Délégué utilisé pour la connexion aux services de consentement
  
### <a name="getobserver-function"></a>GetObserver (fonction)
Obtient l’observateur qui reçoit les notifications des événements liés à [ProtectionProfile](class_mip_protectionprofile.md).

  
**Retourne**: [Observateur](class_mip_protectionprofile_observer.md) qui reçoit des notifications d’événements liés à [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo (fonction)
Obtient des informations sur l’application qui utilise le SDK de protection.

  
**Retourne**: Plus d’informations sur l’application qui utilise le Kit de développement logiciel de protection
  
### <a name="optouttelemetry-function"></a>OptOutTelemetry (fonction)
Refuse la collecte des données de télémétrie.
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut function
Indique si la collecte des données de télémétrie doit être désactivée ou non.

  
**Retourne**: Si la collecte des données de télémétrie doivent être désactivée ou non
  
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

  
**Retourne**: Délégué HTTP à utiliser pour les opérations HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (fonction)
Remplacer la pile HTTP par défaut par celle du client.

Paramètres :  
* **httpDelegate**: Interface de rappel HTTP implémentée par l’application cliente


  
### <a name="getskiptelemetryinit-function"></a>GetSkipTelemetryInit (fonction)
Indique si l’initialisation de la télémétrie doit être ignorée ou non.

  
**Retourne**: Si l’initialisation de télémétrie doit être ignorée ou non
  
### <a name="setskiptelemetryinit-function"></a>SetSkipTelemetryInit (fonction)
Désactive l’initialisation de la télémétrie.
Cette méthode n’est généralement pas appelée par les applications clientes, mais plutôt utilisée par le SDK de fichier pour empêcher l’initialisation en double
  
### <a name="setnewfeaturesdisabled-function"></a>SetNewFeaturesDisabled (fonction)
Désactive les nouvelles fonctionnalités.
Pour les applications qui ne veulent pas essayer de nouvelles fonctionnalités
  
### <a name="arenewfeaturesdisabled-function"></a>AreNewFeaturesDisabled (fonction)
Indique si les nouvelles fonctionnalités sont désactivées ou non.

  
**Retourne**: Si les nouvelles fonctionnalités sont désactivées ou non
  
### <a name="setsessionid-function"></a>SetSessionId function
Définit l’ID de la session.

Paramètres :  
* **sessionId**: ID de session qui sera utilisé pour mettre en corrélation des journaux et la télémétrie


  
### <a name="getsessionid-function"></a>GetSessionId (fonction)
Obtient l’ID de la session.

  
**Retourne**: ID de session qui sera utilisé pour mettre en corrélation des journaux et la télémétrie
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel (fonction)
Définir le niveau de journalisation minimum qui va déclencher un événement de journalisation.

Paramètres :  
* **logLevel** : niveau de journalisation minimum qui va déclencher un événement de journalisation. 



  
**Retourne**: True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel (fonction)
Obtenir l’objet de niveau de journalisation minimum.

  
**Retourne**: Niveau de journalisation minimum qui va déclencher un événement de journalisation.
