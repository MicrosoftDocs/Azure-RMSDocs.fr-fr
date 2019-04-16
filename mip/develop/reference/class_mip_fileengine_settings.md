---
title: mip::FileEngine::Settings, classe
description: Décrit la classe mip::fileengine de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2481ee7d42f00ce5b33529b15e17b22ba6556b0e
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574038"
---
# <a name="class-mipfileenginesettings"></a>mip::FileEngine::Settings, classe 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  Constructeur [FileEngine::Settings](class_mip_fileengine_settings.md) pour le chargement d’un moteur existant.
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md) pour la création d’un moteur.
public const std::string& GetEngineId() const  |  Retourne l’ID du moteur.
public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
public const Identity& GetIdentity() const  |  Retourne le moteur [identité](class_mip_identity.md).
public void SetIdentity(const Identity& identity)  |  Définit l’identité du moteur.
public const std::string& GetClientData() const  |  Retourne les données clientes du moteur.
public const std::string& GetLocale() const  |  Retourne les paramètres régionaux du moteur.
public void SetCustomSettings(const std::vector\<std::pair\<std::string, std::string\>\>& value)  |  Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur.
public const std::string& GetSessionId() const  |  Retourne l’ID de session du moteur.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison du cloud de protection, utilisée pour spécifier la limite du cloud.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Obtient l’url de base de protection cloud point de terminaison.
public void SetPolicyCloudEndpointBaseUrl(const std::string& policyCloudEndpointBaseUrl)  |  Définit la stratégie cloud point de terminaison url de base, permet de spécifier la limite du cloud.
public const std::string& GetPolicyCloudEndpointBaseUrl() const  |  Obtient l’url de base de stratégie cloud point de terminaison.
public void SetProtectionOnlyEngine(const bool protectionOnly)  |  Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public const bool IsProtectionOnlyEngine() const  |  Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public bool IsLoadSensitivityTypesEnabled() const  |  Obtenir l’indicateur spécifiant si les étiquettes de sensibilité de charge est activée.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction de paramètres
Constructeur [FileEngine::Settings](class_mip_fileengine_settings.md) pour le chargement d’un moteur existant.

Paramètres :  
* **engineId**: Affectez-lui la valeur de l’ID de moteur unique généré par AddEngineAsync. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **loadSensitivityTypes**: Indicateur facultatif indiquant quand le moteur est chargé doit charger également les types de sensibilité personnalisée, si true OnPolicyChange Observateur sur le profil sera appelée sur les mises à jour des types de sensibilité personnalisée, ainsi que des modifications de stratégie. Si vous appelez ListSensitivityTypes false retourne toujours une liste vide.


  
### <a name="settings-function"></a>Fonction de paramètres
Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md) pour la création d’un moteur.

Paramètres :  
* **identité**: [Identité](class_mip_identity.md) info de l’utilisateur associé avec le nouveau moteur. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **loadSensitivityTypes**: Indicateur facultatif indiquant quand le moteur est chargé doit charger également les types de sensibilité personnalisée, si true OnPolicyChange Observateur sur le profil sera appelée sur les mises à jour des types de sensibilité personnalisée, ainsi que des modifications de stratégie. Si vous appelez ListSensitivityTypes false retourne toujours une liste vide.


  
### <a name="getengineid-function"></a>GetEngineId (fonction)
Retourne l’ID du moteur.
  
### <a name="setengineid-function"></a>SetEngineId (fonction)
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity (fonction)
Retourne le moteur [identité](class_mip_identity.md).
  
### <a name="setidentity-function"></a>SetIdentity (fonction)
Définit l’identité du moteur.
  
### <a name="getclientdata-function"></a>GetClientData function
Retourne les données clientes du moteur.
  
### <a name="getlocale-function"></a>GetLocale (fonction)
Retourne les paramètres régionaux du moteur.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (fonction)
Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (fonction)
Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
  
### <a name="setsessionid-function"></a>SetSessionId function
Définit l’ID de session du moteur.
  
### <a name="getsessionid-function"></a>GetSessionId (fonction)
Retourne l’ID de session du moteur.
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl function
Définit l’URL de base du point de terminaison du cloud de protection, utilisée pour spécifier la limite du cloud.

Paramètres :  
* **protectionCloudEndpointBaseUrl**: Url de base associés aux points de terminaison de protection


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl function
Obtient l’url de base de protection cloud point de terminaison.

  
**Retourne**: Url de base associés aux points de terminaison de protection
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl function
Définit la stratégie cloud point de terminaison url de base, permet de spécifier la limite du cloud.

Paramètres :  
* **policyCloudEndpointBaseUrl**: Url de base associés aux points de terminaison de stratégie


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl function
Obtient l’url de base de stratégie cloud point de terminaison.

  
**Retourne**: Url de base associés aux points de terminaison de stratégie
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine (fonction)
Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine (fonction)
Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled (fonction)
Obtenir l’indicateur spécifiant si les étiquettes de sensibilité de charge est activée.

  
**Retourne**: True si activé ; sinon, false.