---
title: class mip::PolicyEngine::Settings
description: Décrit la classe mip::policyengine de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3ffd4b3e86192786309739add907a724acdaffa5
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574211"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
Définit les paramètres associés à un [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour le chargement d’un moteur existant.
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour la création d’un moteur.
public const std::string& GetEngineId() const  |  Obtenir l’ID du moteur.
public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
public const Identity& GetIdentity() const  |  Obtenir le [identité](class_mip_identity.md) objet.
public void SetIdentity(const Identity& identity)  |  Définir le [identité](class_mip_identity.md) objet.
public const std::string& GetClientData() const  |  Obtenir la valeur Client Data définie dans les paramètres.
public void SetClientData(const std::string& clientData)  |  Définir la chaîne Client Data.
public const std::string& GetLocale() const  |  Obtenir la valeur Locale définie dans les paramètres.
public void SetCustomSettings(const std::vector\<std::pair\<std::string, std::string\>\>& customSettings)  |  Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.
public void SetSessionId(const std::string& sessionId)  |  Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.
public const std::string& GetSessionId() const  |  Obtenir l’ID de session, qui est un identificateur unique.
public bool IsLoadSensitivityTypesEnabled() const  |  Obtenir l’indicateur spécifiant si les étiquettes de sensibilité de charge est activée.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Définit éventuellement l’URL de base du point de terminaison cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction de paramètres
Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour le chargement d’un moteur existant.

Paramètres :  
* **engineId**: Affectez-lui la valeur de l’ID de moteur unique généré par AddEngineAsync ou un généré automatiquement. Quand vous chargez un moteur existant, réutilisez l’ID ; sinon, un moteur est créé. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **Facultatif**: indicateur indiquant quand le moteur est chargé doit charger également les types de sensibilité personnalisée, si true OnPolicyChange Observateur sur le profil sera appelée sur les mises à jour des types de sensibilité personnalisée, ainsi que des modifications de stratégie. Si vous appelez ListSensitivityTypes false retourne toujours une liste vide.


  
### <a name="settings-function"></a>Fonction de paramètres
Constructeur [PolicyEngine::Settings](class_mip_policyengine_settings.md) pour la création d’un moteur.

Paramètres :  
* **identité**: [Identité](class_mip_identity.md) info de l’utilisateur associé avec le nouveau moteur. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **Facultatif**: indicateur indiquant quand le moteur est chargé doit charger également les types de sensibilité personnalisée, si true OnPolicyChange Observateur sur le profil sera appelée sur les mises à jour des types de sensibilité personnalisée, ainsi que des modifications de stratégie. Si vous appelez ListSensitivityTypes false retourne toujours une liste vide.


  
### <a name="getengineid-function"></a>GetEngineId (fonction)
Obtenir l’ID du moteur.

  
**Retourne**: Une chaîne unique identifiant le moteur.
  
### <a name="setengineid-function"></a>SetEngineId (fonction)
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity (fonction)
Obtenir le [identité](class_mip_identity.md) objet.

  
**Retourne**: Une référence à l’identité dans l’objet de paramètres. 
  
**Voir aussi**: [mip::Identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity (fonction)
Définir le [identité](class_mip_identity.md) objet.

Paramètres :  
* **identity** : identité unique d’un utilisateur. 


  
**Voir aussi**: [mip::Identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData function
Obtenir la valeur Client Data définie dans les paramètres.

  
**Retourne**: Une chaîne de données spécifiées par le client.
  
### <a name="setclientdata-function"></a>SetClientData function
Définir la chaîne Client Data.

Paramètres :  
* **clientData** : données spécifiées par l’utilisateur.


  
### <a name="getlocale-function"></a>GetLocale (fonction)
Obtenir la valeur Locale définie dans les paramètres.

  
**Retourne**: Les paramètres régionaux.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (fonction)
Définir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

Paramètres :  
* **customSettings**: Liste de paires nom/valeur.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (fonction)
Obtenir les paramètres personnalisés, qui sont utilisés pour la régulation et le test de la fonctionnalité.

  
**Retourne**: Liste de paires nom/valeur.
  
### <a name="setsessionid-function"></a>SetSessionId function
Définir l’ID de session, qui est utilisé pour la télémétrie définie par le client.

Paramètres :  
* **sessionId** : chaîne unique qui connecte des événements de télémétrie.


  
### <a name="getsessionid-function"></a>GetSessionId (fonction)
Obtenir l’ID de session, qui est un identificateur unique.

  
**Retourne**: L’ID de session.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled (fonction)
Obtenir l’indicateur spécifiant si les étiquettes de sensibilité de charge est activée.

  
**Retourne**: True si activé ; sinon, false.
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl function
Définit éventuellement l’URL de base du point de terminaison cloud.

Paramètres :  
* **cloudEndpointBaseUrl** : URL de base utilisée par toutes les demandes de service (par exemple, « https://dataservice.protection.outlook.com »)


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl function
Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.

  
**Retourne**: URL de base