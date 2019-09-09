---
title: class mip::PolicyEngine::Settings
description: Documente la classe MIP ::p olicyengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: db96d00d268158b072d2052a5e98f39bf0efa425
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054312"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
Définit les paramètres associés à un [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std :: String & engineId, const std :: String & ClientData :, const std :: String & paramètres régionaux, bool loadSensitivityTypes)  |  Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour le chargement d’un moteur existant.
Paramètres publics (const Identity & Identity, const std :: String & ClientData :, const std :: String & locale, bool loadSensitivityTypes)  |  Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour la création d’un moteur.
public const std::string& GetEngineId() const  |  Obtenir l’ID du moteur.
public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
public const Identity& GetIdentity() const  |  Obtient l’objet [Identity](class_mip_identity.md) .
public void SetIdentity(const Identity& identity)  |  Définissez l’objet [Identity](class_mip_identity.md) .
public const std::string& GetClientData() const  |  Obtenir la valeur Client Data définie dans les paramètres.
public void SetClientData(const std::string& clientData)  |  Définir la chaîne Client Data.
public const std::string& GetLocale() const  |  Obtenir la valeur Locale définie dans les paramètres.
public void SetCustomSettings (const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public void SetSessionId(const std::string& sessionId)  |  Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.
public const std::string& GetSessionId() const  |  Obtenir l’ID de session, qui est un identificateur unique.
public bool IsLoadSensitivityTypesEnabled () const  |  Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Définit éventuellement l’URL de base du point de terminaison cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.
public void SetDelegatedUserEmail (const std :: String & delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std :: String & GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour le chargement d’un moteur existant.

Paramètres :  
* **engineId**: Affectez-lui l’ID de moteur unique généré par AddEngineAsync ou un ID généré automatiquement. Quand vous chargez un moteur existant, réutilisez l’ID ; sinon, un moteur est créé. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **Facultatif**: l’indicateur spécifiant le moment où le moteur est chargé doit également charger des types de sensibilité personnalisés, si la valeur true OnPolicyChange observer sur le profil sera appelée sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="settings-function"></a>Fonction Settings
Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour la création d’un moteur.

Paramètres :  
* **identité**: Informations d' [identité](class_mip_identity.md) de l’utilisateur associé au nouveau moteur. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **Facultatif**: l’indicateur spécifiant le moment où le moteur est chargé doit également charger des types de sensibilité personnalisés, si la valeur true OnPolicyChange observer sur le profil sera appelée sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="getengineid-function"></a>GetEngineId fonction)
Obtenir l’ID du moteur.

  
**Retourne**: Chaîne unique identifiant le moteur.
  
### <a name="setengineid-function"></a>SetEngineId fonction)
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity fonction)
Obtient l’objet [Identity](class_mip_identity.md) .

  
**Retourne**: Référence à l’identité dans l’objet de paramètres. 
  
**Voir aussi**: [MIP :: Identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity fonction)
Définissez l’objet [Identity](class_mip_identity.md) .

Paramètres :  
* **identity** : identité unique d’un utilisateur. 


  
**Voir aussi**: [MIP :: Identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData fonction)
Obtenir la valeur Client Data définie dans les paramètres.

  
**Retourne**: Chaîne de données spécifiée par le client.
  
### <a name="setclientdata-function"></a>SetClientData fonction)
Définir la chaîne Client Data.

Paramètres :  
* **clientData** : données spécifiées par l’utilisateur.


  
### <a name="getlocale-function"></a>GetLocale fonction)
Obtenir la valeur Locale définie dans les paramètres.

  
**Retourne**: Paramètres régionaux.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings**: Liste de paires nom/valeur.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

  
**Retourne**: Liste de paires nom/valeur.
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.

Paramètres :  
* **sessionId** : chaîne unique qui connecte des événements de télémétrie.


  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Obtenir l’ID de session, qui est un identificateur unique.

  
**Retourne**: ID de session.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled fonction)
Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.

  
**Retourne**: True si l’option est activée. sinon, false.
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl fonction)
Définit éventuellement l’URL de base du point de terminaison cloud.

Paramètres :  
* **cloudEndpointBaseUrl** : URL de base utilisée par toutes les demandes de service (par exemple, « https://dataservice.protection.outlook.com  »)


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl function
Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.

  
**Retourne**: URL de base
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail fonction)
Définit l’utilisateur délégué.

Paramètres :  
* **delegatedUserEmail**: e-mail de délégation.


Un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: Utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur