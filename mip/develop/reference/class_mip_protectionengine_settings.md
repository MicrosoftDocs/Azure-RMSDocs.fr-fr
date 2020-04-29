---
title: 'classe ProtectionEngine :: Settings'
description: 'Documente la classe protectionengine :: Settings du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 7c6b96a1ec78712cb256ab63efe869213fc71f8e
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764597"
---
# <a name="class-protectionenginesettings"></a>classe ProtectionEngine :: Settings 
Settings utilisé par ProtectionEngine lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
Paramètres publics (const Identity& Identity, const std :\<:\> shared_ptr AuthDelegate& AuthDelegate, const std :: String& ClientData :, const std :: String& paramètres régionaux)  |  Constructeur ProtectionEngine::Settings pour la création d’un nouveau moteur.
Paramètres publics (const std :: String& engineId, const std :: shared_ptr\<AuthDelegate\>& AuthDelegate, const std :: String& ClientData :, const std :: String& paramètres régionaux)  |  Constructeur ProtectionEngine::Settings pour le chargement d’un moteur existant.
public const std::string& GetEngineId() const  |  Obtient l’ID du moteur.
public void SetEngineId(const std::string& engineId)  |  Définit l’ID du moteur.
public const Identity& GetIdentity() const  |  Obtient l’identité de l’utilisateur associé au moteur.
public void SetIdentity(const Identity& identity)  |  Définit l’identité de l’utilisateur associé au moteur.
public const std::string& GetClientData() const  |  Obtient les données personnalisées spécifiées par le client.
public void SetClientData(const std::string& clientData)  |  Définit les données personnalisées spécifiées par le client.
public const std::string& GetLocale() const  |  Obtient les paramètres régionaux selon lesquels les données du moteur seront écrites.
public void SetCustomSettings (const std :: Vector\<std ::p air\<std :: String, std :: String\> \>& value)  |  Définit les paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std :: Vector\<std ::p air\<std :: String, std :: String\> \>& GetCustomSettings () const  |  Obtient les paires nom/valeur utilisées pour les tests et l’expérimentation.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie.
public const std::string& GetSessionId() const  |  Obtient l’ID de session du moteur.
public void SetCloud (Cloud Cloud)  |  Définit éventuellement le Cloud cible.
const GetCloud () du cloud public  |  Obtient le Cloud cible utilisé par toutes les demandes de service.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Définit l’URL de base du point de terminaison Cloud pour le Cloud personnalisé.
public const std::string& GetCloudEndpointBaseUrl() const  |  Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.
public void SetAuthDelegate (const std :: shared_ptr\<authDelegate\>& AuthDelegate)  |  Définissez le délégué d’authentification du moteur.
public std :: shared_ptr\<AuthDelegate\> GetAuthDelegate () const  |  Obtient le délégué d’authentification du moteur.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Constructeur ProtectionEngine::Settings pour la création d’un nouveau moteur.

Paramètres :  
* **identity** : identité qui sera associée à ProtectionEngine


* **authDelegate**: le délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification remplace PolicyProfile :: Settings :: authDelegate si les deux sont fournis 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie du moteur est fournie dans ces paramètres régionaux.


  
### <a name="settings-function"></a>Fonction Settings
Constructeur ProtectionEngine::Settings pour le chargement d’un moteur existant.

Paramètres :  
* **engineId** : identificateur unique du moteur qui sera chargé 


* **authDelegate**: le délégué d’authentification utilisé par le kit de développement logiciel (SDK) pour acquérir des jetons d’authentification remplace PolicyProfile :: Settings :: authDelegate si les deux sont fournis 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **locale** : la sortie du moteur est fournie dans ces paramètres régionaux.


  
### <a name="getengineid-function"></a>GetEngineId fonction)
Obtient l’ID du moteur.

  
**Retourne**: ID du moteur
  
### <a name="setengineid-function"></a>SetEngineId fonction)
Définit l’ID du moteur.

Paramètres :  
* **engineId**: ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity fonction)
Obtient l’identité de l’utilisateur associé au moteur.

  
**Retourne** : l’identité de l’utilisateur associé au moteur
  
### <a name="setidentity-function"></a>SetIdentity fonction)
Définit l’identité de l’utilisateur associé au moteur.

Paramètres :  
* **identity** : l’identité de l’utilisateur associé au moteur


  
### <a name="getclientdata-function"></a>GetClientData fonction)
Obtient les données personnalisées spécifiées par le client.

  
**Retourne** : les données personnalisées spécifiées par le client
  
### <a name="setclientdata-function"></a>SetClientData fonction)
Définit les données personnalisées spécifiées par le client.

Paramètres :  
* **Custom** : données spécifiées par le client


  
### <a name="getlocale-function"></a>GetLocale fonction)
Obtient les paramètres régionaux selon lesquels les données du moteur seront écrites.

  
**Retourne** : les paramètres régionaux selon lesquels les données du moteur seront écrites
  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définit les paires nom/valeur utilisées pour les tests et l’expérimentation.

Paramètres :  
* **customSettings** : une liste de paires nom/valeur utilisées pour les tests et l’expérimentation


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient les paires nom/valeur utilisées pour les tests et l’expérimentation.

  
**Retourne** : les paires nom/valeur utilisées pour les tests et l’expérimentation
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Définit l’ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie.

Paramètres :  
* **SessionID**: ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie


  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Obtient l’ID de session du moteur.

  
**Retourne**: ID de session du moteur
  
### <a name="setcloud-function"></a>SetCloud fonction)
Définit éventuellement le Cloud cible.

Paramètres :  
* **Cloud**: Cloud


Si le Cloud n’est pas spécifié, il est déterminé par la recherche DNS du domaine d’identité du moteur, si possible, sinon revient au Cloud global.
  
### <a name="getcloud-function"></a>GetCloud fonction)
Obtient le Cloud cible utilisé par toutes les demandes de service.

  
**Retourne**: Cloud
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl fonction)
Définit l’URL de base du point de terminaison Cloud pour le Cloud personnalisé.

Paramètres :  
* **cloudEndpointBaseUrl** : URL de base utilisée par toutes les demandes de service (par exemple, « https://api.aadrm.com »)


Cette valeur est lue uniquement et doit être définie pour Cloud = Custom
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl fonction)
Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.

  
**Retourne** : URL de base
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate fonction)
Définissez le délégué d’authentification du moteur.

Paramètres :  
* **authDelegate**: délégué d’authentification


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate fonction)
Obtient le délégué d’authentification du moteur.

  
**Retourne**: le délégué d’authentification du moteur.