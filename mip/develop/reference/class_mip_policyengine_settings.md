---
title: mip PolicyEngine Settings, classe
description: Informations de référence pour la classe mip PolicyEngine Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6ac94d1e34615a0248dac85f28c55154b127574f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446343"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
Définit les paramètres associés à un [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour le chargement d’un moteur existant.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour la création d’un moteur.
 public const std::string& GetEngineId() const  |  Obtenir l’ID du moteur.
 public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
 public const Identity& GetIdentity() const  |  Obtenir l’objet Identity.
 public void SetIdentity(const Identity& identity)  |  Définir l’objet Identity.
 public const std::string& GetClientData() const  |  Obtenir la valeur Client Data définie dans les paramètres.
 public void SetClientData(const std::string& clientData)  |  Définir la chaîne Client Data.
 public const std::string& GetLocale() const  |  Obtenir la valeur Locale définie dans les paramètres.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
 public void SetSessionId(const std::string& sessionId)  |  Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.
 public const std::string& GetSessionId() const  |  Obtenir l’ID de session, qui est un identificateur unique.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour le chargement d’un moteur existant.

Paramètres :  
* **engineId** : affectez à ce paramètre l’ID unique du moteur généré par AddEngineAsync ou un ID généré automatiquement. Quand vous chargez un moteur existant, réutilisez l’ID ; sinon, un moteur est créé. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux.


  
### <a name="settings"></a>Paramètres
Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour la création d’un moteur.

Paramètres :  
* **identity** : informations d’identité de l’utilisateur associé au nouveau moteur. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux.


  
### <a name="getengineid"></a>GetEngineId
Obtenir l’ID du moteur.

  
**Retourne** : une chaîne unique identifiant le moteur.
  
### <a name="setengineid"></a>SetEngineId
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity"></a>GetIdentity
Obtenir l’objet Identity.

  
**Retourne** : une référence à l’identité définie dans l’objet settings. 
  
**Voir aussi** : mip::Identity
  
### <a name="setidentity"></a>SetIdentity
Définir l’objet Identity.

Paramètres :  
* **identity** : identité unique d’un utilisateur. 


  
**Voir aussi** : mip::Identity
  
### <a name="getclientdata"></a>GetClientData
Obtenir la valeur Client Data définie dans les paramètres.

  
**Retourne** : une chaîne de données spécifiées par le client.
  
### <a name="setclientdata"></a>SetClientData
Définir la chaîne Client Data.

Paramètres :  
* **clientData** : données spécifiées par l’utilisateur.


  
### <a name="getlocale"></a>GetLocale
Obtenir la valeur Locale définie dans les paramètres.

  
**Retourne** : les paramètres régionaux.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings** : liste de paires nom/valeur.


  
### <a name="getcustomsettings"></a>SetCustomSettings
Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

  
**Retourne** : liste de paires nom/valeur.
  
### <a name="setsessionid"></a>SetSessionId
Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.

Paramètres :  
* **sessionId** : chaîne unique qui connecte des événements de télémétrie.


  
### <a name="getsessionid"></a>GetSessionId
Obtenir l’ID de session, qui est un identificateur unique.

  
**Retourne** : ID de session.