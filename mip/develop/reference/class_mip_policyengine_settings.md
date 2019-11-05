---
title: class mip::PolicyEngine::Settings
description: Documente la classe MIP ::p olicyengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: c215b7e25908cc3f7984f68b63e3ea1be4d4a718
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560982"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
Définit les paramètres associés à un PolicyEngine.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std :: String & engineId, const std :: String & ClientData :, const std :: String & paramètres régionaux, bool loadSensitivityTypes)  |  PolicyEngine :: Settings, constructeur pour le chargement d’un moteur existant.
Paramètres publics (const Identity & Identity, const std :: String & ClientData :, const std :: String & locale, bool loadSensitivityTypes)  |  PolicyEngine :: Settings, constructeur pour la création d’un nouveau moteur.
public const std::string& GetEngineId() const  |  Obtenir l’ID du moteur.
public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
public const Identity& GetIdentity() const  |  Obtenir l’objet Identity.
public void SetIdentity(const Identity& identity)  |  Définir l’objet Identity.
public const std::string& GetClientData() const  |  Obtenir la valeur Client Data définie dans les paramètres.
public void SetClientData(const std::string& clientData)  |  Définir la chaîne Client Data.
public const std::string& GetLocale() const  |  Obtenir la valeur Locale définie dans les paramètres.
public void SetCustomSettings (const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetCustomSettings () const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public void SetSessionId(const std::string& sessionId)  |  Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.
public const std::string& GetSessionId() const  |  Obtenir l’ID de session, qui est un identificateur unique.
public bool IsLoadSensitivityTypesEnabled () const  |  Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Définit éventuellement l’URL de base du point de terminaison cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.
public void SetDelegatedUserEmail (const std :: String & delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std :: String & GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
public void SetLabelFilter (const std :: Vector\<LabelFilterType\>& labelFilter)  |  Définit le filtre d’étiquette.
public const std :: Vector\<LabelFilterType\>& GetLabelFilter () const  |  Obtient le filtre d’étiquette.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
PolicyEngine :: Settings, constructeur pour le chargement d’un moteur existant.

Paramètres :  
* **engineId** : affectez à ce paramètre l’ID unique du moteur généré par AddEngineAsync ou un ID généré automatiquement. Quand vous chargez un moteur existant, réutilisez l’ID ; sinon, un moteur est créé. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **Facultatif**: l’indicateur spécifiant le moment où le moteur est chargé doit également charger des types de sensibilité personnalisés, si la valeur true OnPolicyChange observer sur le profil sera appelée sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="settings-function"></a>Fonction Settings
PolicyEngine :: Settings, constructeur pour la création d’un nouveau moteur.

Paramètres :  
* **identity** : informations d’identité de l’utilisateur associé au nouveau moteur. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **Facultatif**: l’indicateur spécifiant le moment où le moteur est chargé doit également charger des types de sensibilité personnalisés, si la valeur true OnPolicyChange observer sur le profil sera appelée sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="getengineid-function"></a>GetEngineId fonction)
Obtenir l’ID du moteur.

  
**Retourne** : une chaîne unique identifiant le moteur.
  
### <a name="setengineid-function"></a>SetEngineId fonction)
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity fonction)
Obtenir l’objet Identity.

  
**Retourne** : une référence à l’identité définie dans l’objet settings. 
  
**Voir aussi** : mip::Identity
  
### <a name="setidentity-function"></a>SetIdentity fonction)
Définir l’objet Identity.

Paramètres :  
* **identity** : identité unique d’un utilisateur. 


  
**Voir aussi** : mip::Identity
  
### <a name="getclientdata-function"></a>GetClientData fonction)
Obtenir la valeur Client Data définie dans les paramètres.

  
**Retourne** : une chaîne de données spécifiées par le client.
  
### <a name="setclientdata-function"></a>SetClientData fonction)
Définir la chaîne Client Data.

Paramètres :  
* **clientData** : données spécifiées par l’utilisateur.


  
### <a name="getlocale-function"></a>GetLocale fonction)
Obtenir la valeur Locale définie dans les paramètres.

  
**Retourne** : les paramètres régionaux.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings** : liste de paires nom/valeur.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

  
**Retourne** : liste de paires nom/valeur.
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.

Paramètres :  
* **sessionId** : chaîne unique qui connecte des événements de télémétrie.


  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Obtenir l’ID de session, qui est un identificateur unique.

  
**Retourne** : ID de session.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled fonction)
Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.

  
**Retourne**la valeur true si l’option est activée. sinon, false.
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl fonction)
Définit éventuellement l’URL de base du point de terminaison cloud.

Paramètres :  
* **cloudEndpointBaseUrl** : URL de base utilisée par toutes les demandes de service (par exemple, « https://dataservice.protection.outlook.com  »)


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl fonction)
Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.

  
**Retourne** : URL de base
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail fonction)
Définit l’utilisateur délégué.

Paramètres :  
* **delegatedUserEmail**: e-mail de délégation.


Un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="setlabelfilter-function"></a>SetLabelFilter fonction)
Définit le filtre d’étiquette.

Paramètres :  
* **labelFilter**: filtre d’étiquette.


Par défaut, les étiquettes sont filtrées par défaut, cette API permet de filtrer par actions possibles.
  
### <a name="getlabelfilter-function"></a>GetLabelFilter fonction)
Obtient le filtre d’étiquette.

  
**Retourne**: filtre d’étiquette.
Par défaut, les étiquettes sont filtrées par défaut, cette API permet de filtrer par actions possibles.