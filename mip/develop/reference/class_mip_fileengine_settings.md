---
title: mip::FileEngine::Settings, classe
description: 'Documente la classe MIP :: fileengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 6105a542c3c01b31598796912211f97562b25f08
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488787"
---
# <a name="class-mipfileenginesettings"></a>mip::FileEngine::Settings, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std :: String & engineId, const std :: String & ClientData :, const std :: String & paramètres régionaux, bool loadSensitivityTypes)  |  FileEngine :: Settings, constructeur pour le chargement d’un moteur existant.
Paramètres publics (const Identity & Identity, const std :: String & ClientData :, const std :: String & locale, bool loadSensitivityTypes)  |  FileProfile :: Settings, constructeur pour la création d’un nouveau moteur.
public const std::string& GetEngineId() const  |  Retourne l’ID du moteur.
public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
public const Identity& GetIdentity() const  |  Retourne l’identité du moteur.
public void SetIdentity(const Identity& identity)  |  Définit l’identité du moteur.
public const std::string& GetClientData() const  |  Retourne les données clientes du moteur.
public const std::string& GetLocale() const  |  Retourne les paramètres régionaux du moteur.
public void SetCustomSettings (const std :: Vector\<std ::p air\<std :: String, std :: String\>\>valeur &)  |  Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetCustomSettings () const  |  Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur.
public const std::string& GetSessionId() const  |  Retourne l’ID de session du moteur.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison du cloud de protection, utilisée pour spécifier la limite du cloud.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Obtient l’URL de base du point de terminaison Cloud de protection.
public void SetPolicyCloudEndpointBaseUrl (const std :: String & policyCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison Cloud de la stratégie, utilisée pour spécifier la limite du Cloud.
public const std::string& GetPolicyCloudEndpointBaseUrl() const  |  Obtient l’URL de base du point de terminaison Cloud de la stratégie.
public void SetProtectionOnlyEngine (bool protectionOnly)  |  Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public const bool IsProtectionOnlyEngine() const  |  Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public bool IsLoadSensitivityTypesEnabled () const  |  Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.
public void EnablePFile (valeur bool)  |  Définit l’indicateur qui spécifie si produit fichiers pfile.
public const bool IsPFileEnabled ()  |  Obtient l’indicateur qui spécifie si produit fichiers pfile.
public void SetDelegatedUserEmail (const std :: String & delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std :: String & GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
public void SetLabelFilter (const std :: Vector\<LabelFilterType\>& labelFilter)  |  Définit le filtre d’étiquette.
public const std :: Vector\<LabelFilterType\>& GetLabelFilter () const  |  Obtient le filtre d’étiquette.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
FileEngine :: Settings, constructeur pour le chargement d’un moteur existant.

Paramètres :  
* **engineId** : affectez à ce paramètre l’ID de moteur unique généré par AddEngineAsync. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **loadSensitivityTypes**: un indicateur facultatif indiquant le moment où le moteur est chargé doit également charger des types de sensibilité personnalisés, si la valeur true OnPolicyChange observer sur le profil sera appelée sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="settings-function"></a>Fonction Settings
FileProfile :: Settings, constructeur pour la création d’un nouveau moteur.

Paramètres :  
* **identity** : informations d’identité de l’utilisateur associé au nouveau moteur. 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **loadSensitivityTypes**: un indicateur facultatif indiquant le moment où le moteur est chargé doit également charger des types de sensibilité personnalisés, si la valeur true OnPolicyChange observer sur le profil sera appelée sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="getengineid-function"></a>GetEngineId fonction)
Retourne l’ID du moteur.
  
### <a name="setengineid-function"></a>SetEngineId fonction)
Définir l’ID du moteur.

Paramètres :  
* **id** : ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity fonction)
Retourne l’identité du moteur.
  
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
* **protectionCloudEndpointBaseUrl** : URL de base associée aux points de terminaison de protection


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl function
Obtient l’URL de base du point de terminaison Cloud de protection.

  
**Retourne** : URL de base associée aux points de terminaison de protection
  
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

  
**Retourne**la valeur true si l’option est activée. sinon, false.
  
### <a name="enablepfile-function"></a>EnablePFile fonction)
Définit l’indicateur qui spécifie si produit fichiers pfile.
  
### <a name="ispfileenabled-function"></a>IsPFileEnabled fonction)
Obtient l’indicateur qui spécifie si produit fichiers pfile.

  
**Retourne**la valeur true si l’option est activée. sinon, false.
  
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