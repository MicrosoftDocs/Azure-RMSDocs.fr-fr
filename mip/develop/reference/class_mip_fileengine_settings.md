---
title: 'classe FileEngine :: Settings'
description: 'Documente la classe fileengine :: Settings du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 05fb06ec06943b39209c980236643e50d873d451
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566974"
---
# <a name="class-fileenginesettings"></a>classe FileEngine :: Settings 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const std :: String& engineId, const std :: shared_ptr \<AuthDelegate\>& authDelegate, const std :: string& ClientData :, const std :: string& paramètres régionaux, bool loadSensitivityTypes)  |  Constructeur FileEngine::Settings pour le chargement d’un moteur existant.
Paramètres publics (const Identity& Identity, const std :: shared_ptr \<AuthDelegate\>& authDelegate, const std :: string& ClientData :, const std :: string& locale, bool loadSensitivityTypes)  |  Constructeur FileProfile::Settings pour la création d’un moteur.
public const std::string& GetEngineId() const  |  Retourne l’ID du moteur.
public void SetEngineId(const std::string& id)  |  Définir l’ID du moteur.
public const Identity& GetIdentity() const  |  Retourne l’identité du moteur.
public void SetIdentity(const Identity& identity)  |  Définit l’identité du moteur.
public const std::string& GetClientData() const  |  Retourne les données clientes du moteur.
public const std::string& GetLocale() const  |  Retourne les paramètres régionaux du moteur.
public void SetCustomSettings (const std :: Vector \<std::pair\<std::string, std::string\> \>& valeur)  |  Définit une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std :: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Obtient une liste de paires nom/valeur utilisées pour les tests et l’expérimentation.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur.
public const std::string& GetSessionId() const  |  Retourne l’ID de session du moteur.
public void SetCloud (Cloud Cloud)  |  Définit éventuellement le Cloud cible.
const GetCloud () du cloud public  |  Obtient le Cloud cible utilisé par toutes les demandes de service.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison Cloud de protection pour le Cloud personnalisé.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Obtient l’URL de base du point de terminaison Cloud de protection.
public void SetPolicyCloudEndpointBaseUrl (const std :: String& policyCloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison Cloud de la stratégie pour le Cloud personnalisé.
public const std :: String& GetPolicyCloudEndpointBaseUrl () const  |  Obtient l’URL de base du point de terminaison Cloud de la stratégie.
public void SetProtectionOnlyEngine (bool protectionOnly)  |  Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public const bool IsProtectionOnlyEngine() const  |  Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
public bool IsLoadSensitivityTypesEnabled () const  |  Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.
public void EnablePFile (valeur bool)  |  Définit l’indicateur qui spécifie si produit fichiers pfile.
public const bool IsPFileEnabled ()  |  Obtient l’indicateur qui spécifie si produit fichiers pfile.
public void SetDelegatedUserEmail (const std :: String& delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std :: String& GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
public void SetLabelFilter (const std :: Vector \<LabelFilterType\>& deprecatedLabelFilters)  |  Définit le filtre d’étiquette.
public const std :: Vector \<LabelFilterType\>& GetLabelFilter () const  |  Obtient les filtres d’étiquette définis via la fonction déconseillée SetLabelFilter.
public void ConfigureFunctionality (LabelFilterType labelFilterType, bool Enabled)  |  Active ou désactive la fonctionnalité.
public const std :: map \<LabelFilterType, bool\>& GetConfiguredFunctionality () const  |  Obtient les fonctionnalités configurées.
public void SetClassifierEnabled (classifieur classifierType, bool Enabled)  |  Active ou désactive la prise en charge des types de classification.
public const std :: map \<Classifier, bool\>& GetConfiguredClassifierSupport () const  |  Obtient les substitutions de classifieur prises en charge.
public void SetAuthDelegate (const std :: shared_ptr \<AuthDelegate\>& authDelegate)  |  Définissez le délégué d’authentification du moteur.
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  Obtient le délégué d’authentification du moteur.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Constructeur FileEngine::Settings pour le chargement d’un moteur existant.

Paramètres :  
* **engineId**: affectez-lui l’ID de moteur unique généré par AddEngineAsync. 


* **authDelegate**: le délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification remplace PolicyProfile :: Settings :: authDelegate si les deux sont fournis 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie localisable du moteur est fournie dans ces paramètres régionaux. 


* **loadSensitivityTypes**: un indicateur facultatif indiquant le moment où le moteur est chargé doit également charger des types de sensibilité personnalisés, si la valeur true OnPolicyChange observer sur le profil sera appelée sur des mises à jour de types de sensibilité personnalisés, ainsi que des modifications de stratégie. Si la valeur false, l’appel ListSensitivityTypes retourne toujours une liste vide.


  
### <a name="settings-function"></a>Fonction Settings
Constructeur FileProfile::Settings pour la création d’un moteur.

Paramètres :  
* **identity** : informations d’identité de l’utilisateur associé au nouveau moteur. 


* **authDelegate**: le délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification remplace PolicyProfile :: Settings :: authDelegate si les deux sont fournis 


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
  
### <a name="setcloud-function"></a>SetCloud fonction)
Définit éventuellement le Cloud cible.

Paramètres :  
* **Cloud**: Cloud


Si le Cloud n’est pas spécifié, le Cloud global est utilisé par défaut.
  
### <a name="getcloud-function"></a>GetCloud fonction)
Obtient le Cloud cible utilisé par toutes les demandes de service.

  
**Retourne**: Cloud
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl fonction)
Définit l’URL de base du point de terminaison Cloud de protection pour le Cloud personnalisé.

Paramètres :  
* **protectionCloudEndpointBaseUrl** : URL de base associée aux points de terminaison de protection


Cette valeur est lue uniquement et doit être définie pour Cloud = Custom
  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl fonction)
Obtient l’URL de base du point de terminaison Cloud de protection.

  
**Retourne**: URL de base associée aux points de terminaison de protection. cette valeur sera uniquement lue et doit être définie pour Cloud = Custom
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl fonction)
Définit l’URL de base du point de terminaison Cloud de la stratégie pour le Cloud personnalisé.

Paramètres :  
* **policyCloudEndpointBaseUrl**: URL de base associée aux points de terminaison de stratégie


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl fonction)
Obtient l’URL de base du point de terminaison Cloud de la stratégie.

  
**Retourne**: URL de base associée aux points de terminaison de stratégie
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine fonction)
Définit l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine fonction)
Retourne l’indicateur du moteur de protection uniquement - sans étiquette/stratégie.
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled fonction)
Obtient l’indicateur qui spécifie si les étiquettes de sensibilité de la charge sont activées.

  
**Retourne** la valeur true si l’option est activée. sinon, false.
  
### <a name="enablepfile-function"></a>EnablePFile fonction)
Définit l’indicateur qui spécifie si produit fichiers pfile.
  
### <a name="ispfileenabled-function"></a>IsPFileEnabled fonction)
Obtient l’indicateur qui spécifie si produit fichiers pfile.

  
**Retourne** la valeur true si l’option est activée. sinon, false.
  
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


Par défaut, les étiquettes sont filtrées par défaut, cette API permet de filtrer par actions possibles. Si la valeur n’est pas définie, HyokProtection et DoubleKeyProtection sont filtrés.
  
### <a name="getlabelfilter-function"></a>GetLabelFilter fonction)
Obtient les filtres d’étiquette définis via la fonction déconseillée SetLabelFilter.

  
**Retourne**: filtre d’étiquette.
Par défaut, les étiquettes sont filtrées par défaut, cette API permet de filtrer par actions possibles.
  
### <a name="configurefunctionality-function"></a>ConfigureFunctionality fonction)
Active ou désactive la fonctionnalité.

Paramètres :  
* **labelFilterType**: type de fonctionnalité. 


* **activé**: true pour activer, false pour désactiver


HyokProtection, DoubleKeyProtection, DoubleKeyUserDefinedProtection sont désactivés par défaut et doivent être activés
  
### <a name="getconfiguredfunctionality-function"></a>GetConfiguredFunctionality fonction)
Obtient les fonctionnalités configurées.

  
**Retourne**: un mappage des types à une valeur booléenne indiquant si elle est activée ou non.
  
### <a name="setclassifierenabled-function"></a>SetClassifierEnabled fonction)
Active ou désactive la prise en charge des types de classification.

Paramètres :  
* **classifierType**: type de classifieur 


* **activé**: true pour activer, false pour désactiver


Seuls les classifers SensitiveInformation sont activés par défaut
  
### <a name="getconfiguredclassifiersupport-function"></a>GetConfiguredClassifierSupport fonction)
Obtient les substitutions de classifieur prises en charge.

  
**Retourne**: un mappage des types à une valeur booléenne indiquant s’ils ont été remplacés par la prise en charge
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate fonction)
Définissez le délégué d’authentification du moteur.

Paramètres :  
* **authDelegate**: délégué d’authentification


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate fonction)
Obtient le délégué d’authentification du moteur.

  
**Retourne**: le délégué d’authentification du moteur.