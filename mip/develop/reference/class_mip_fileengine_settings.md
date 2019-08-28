---
title: mip::FileEngine::Settings, classe
description: 'Documente la classe MIP:: fileengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 7d0845c2bf7516a4fc0a85b690fa94059253cde8
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055032"
---
# <a name="class-mipfileenginesettings"></a>mip::FileEngine::Settings, classe 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std:: String & engineId, const std:: String & ClientData:, const std:: String & paramètres régionaux, bool loadSensitivityTypes)  |  Constructeur [FileEngine::Settings](class_mip_fileengine_settings.md) pour le chargement d’un moteur existant.
Paramètres publics (const Identity & Identity, const std:: String & ClientData:, const std:: String & locale, bool loadSensitivityTypes)  |  Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md) pour la création d’un moteur.
public const std::string& GetEngineId() const  |  Retourne l’ID du moteur.
public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
public const Identity& GetIdentity() const  |  Retourne l' [identité](class_mip_identity.md)du moteur.
public void SetIdentity(const Identity& identity)  |  Définit l’identité du moteur.
public const std::string& GetClientData() const  |  Retourne les données clientes du moteur.
public const std::string& GetLocale() const  |  Retourne les paramètres régionaux du moteur.
public void SetCustomSettings(const std::vector\<std::pair\<std::string, std::string\>\>& value)  |  Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur.
public const std::string& GetSessionId() const  |  Retourne l’ID de session du moteur.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison du cloud de protection, utilisée pour spécifier la limite du cloud.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Obtient l’URL de base du point de terminaison Cloud de protection.
public void SetPolicyCloudEndpointBaseUrl (const std:: String & policyCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison Cloud de la stratégie, utilisée pour spécifier la limite du Cloud.
public const std::string& GetPolicyCloudEndpointBaseUrl() const  |  Obtient l’URL de base du point de terminaison Cloud de la stratégie.
public void SetProtectionOnlyEngine (bool protectionOnly)  |  Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public const bool IsProtectionOnlyEngine() const  |  Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public bool IsLoadSensitivityTypesEnabled () const  |  Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.
public void EnablePFile (valeur bool)  |  Définit l’indicateur qui spécifie si produit fichiers pfile.
public const bool IsPFileEnabled ()  |  Obtient l’indicateur qui spécifie si produit fichiers pfile.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std:: String & GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Constructeur [FileEngine::Settings](class_mip_fileengine_settings.md) pour le chargement d’un moteur existant.

Paramètres :  
* **engineId**: Affectez-lui l’ID de moteur unique généré par AddEngineAsync. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **loadSensitivityTypes**: Un indicateur facultatif qui spécifie quand le moteur est chargé doit également charger des types de sensibilité personnalisés, si true OnPolicyChange observer sur le profil sera appelé sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="settings-function"></a>Fonction Settings
Constructeur [FileProfile::Settings](class_mip_fileprofile_settings.md) pour la création d’un moteur.

Paramètres :  
* **identité**: Informations d' [identité](class_mip_identity.md) de l’utilisateur associé au nouveau moteur. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **loadSensitivityTypes**: Un indicateur facultatif qui spécifie quand le moteur est chargé doit également charger des types de sensibilité personnalisés, si true OnPolicyChange observer sur le profil sera appelé sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="getengineid-function"></a>GetEngineId fonction)
Retourne l’ID du moteur.
  
### <a name="setengineid-function"></a>SetEngineId fonction)
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity fonction)
Retourne l' [identité](class_mip_identity.md)du moteur.
  
### <a name="setidentity-function"></a>SetIdentity fonction)
Définit l’identité du moteur.
  
### <a name="getclientdata-function"></a>GetClientData fonction)
Retourne les données clientes du moteur.
  
### <a name="getlocale-function"></a>GetLocale fonction)
Retourne les paramètres régionaux du moteur.
  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Définit l’ID de session du moteur.
  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Retourne l’ID de session du moteur.
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl function
Définit l’URL de base du point de terminaison du cloud de protection, utilisée pour spécifier la limite du cloud.

Paramètres :  
* **protectionCloudEndpointBaseUrl**: URL de base associée aux points de terminaison de protection


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl function
Obtient l’URL de base du point de terminaison Cloud de protection.

  
**Retourne**: URL de base associée aux points de terminaison de protection
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl function
Définit l’URL de base du point de terminaison Cloud de la stratégie, utilisée pour spécifier la limite du Cloud.

Paramètres :  
* **policyCloudEndpointBaseUrl**: URL de base associée aux points de terminaison de stratégie


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl function
Obtient l’URL de base du point de terminaison Cloud de la stratégie.

  
**Retourne**: URL de base associée aux points de terminaison de stratégie
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine fonction)
Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine fonction)
Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled fonction)
Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.

  
**Retourne**: True si l’option est activée. sinon, false.
  
### <a name="enablepfile-function"></a>EnablePFile fonction)
Définit l’indicateur qui spécifie si produit fichiers pfile.
  
### <a name="ispfileenabled-function"></a>IsPFileEnabled fonction)
Obtient l’indicateur qui spécifie si produit fichiers pfile.

  
**Retourne**: True si l’option est activée. sinon, false.
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail fonction)
Définit l’utilisateur délégué.

Paramètres :  
* **delegatedUserEmail**: e-mail de délégation.


Un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: Utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur