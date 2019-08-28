---
title: class mip::ProtectionEngine::Settings
description: Documente la classe MIP::p rotectionengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a083d037fcfb48ae9eee5df67fb78d53fcb5490a
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057595"
---
# <a name="class-mipprotectionenginesettings"></a>class mip::ProtectionEngine::Settings 
[Settings](class_mip_protectionengine_settings.md) utilisé par [ProtectionEngine](class_mip_protectionengine.md) lors de sa création et tout au long de sa durée de vie.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour la création d’un nouveau moteur.
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour le chargement d’un moteur existant.
public const std::string& GetEngineId() const  |  Obtient l’ID du moteur.
public void SetEngineId(const std::string& engineId)  |  Définit l’ID du moteur.
public const Identity& GetIdentity() const  |  Obtient l' [identité](class_mip_identity.md) de l’utilisateur associée au moteur.
public void SetIdentity(const Identity& identity)  |  Définit l' [identité](class_mip_identity.md) de l’utilisateur associée au moteur.
public const std::string& GetClientData() const  |  Obtient les données personnalisées spécifiées par le client.
public void SetClientData(const std::string& clientData)  |  Définit les données personnalisées spécifiées par le client.
public const std::string& GetLocale() const  |  Obtient les paramètres régionaux selon lesquels les données du moteur seront écrites.
public void SetCustomSettings(const std::vector\<std::pair\<std::string, std::string\>\>& value)  |  Définit les paires nom/valeur utilisées pour les tests et l’expérimentation.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient les paires nom/valeur utilisées pour les tests et l’expérimentation.
public void SetSessionId(const std::string& sessionId)  |  Définit l’ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie.
public const std::string& GetSessionId() const  |  Obtient l’ID de session du moteur.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Définit éventuellement l’URL de base du point de terminaison cloud.
public const std::string& GetCloudEndpointBaseUrl() const  |  Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.
  
## <a name="members"></a>Membres
  
### <a name="settings-function"></a>Fonction Settings
Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour la création d’un nouveau moteur.

Paramètres :  
* **identité**: [Identité](class_mip_identity.md) qui sera associée à [ProtectionEngine](class_mip_protectionengine.md)


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **paramètres régionaux**: La sortie du moteur est fournie dans ces paramètres régionaux.


  
### <a name="settings-function"></a>Fonction Settings
Constructeur [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) pour le chargement d’un moteur existant.

Paramètres :  
* **engineId**: Identificateur unique du moteur qui sera chargé 


* **clientData** : données clientes personnalisables qui peuvent être stockées avec le moteur lors du déchargement, et être récupérées à partir d’un moteur chargé. 


* **paramètres régionaux**: La sortie du moteur est fournie dans ces paramètres régionaux.


  
### <a name="getengineid-function"></a>GetEngineId fonction)
Obtient l’ID du moteur.

  
**Retourne**: ID du moteur
  
### <a name="setengineid-function"></a>SetEngineId fonction)
Définit l’ID du moteur.

Paramètres :  
* **engineId** : ID du moteur.


  
### <a name="getidentity-function"></a>GetIdentity fonction)
Obtient l' [identité](class_mip_identity.md) de l’utilisateur associée au moteur.

  
**Retourne**: [Identité](class_mip_identity.md) de l’utilisateur associée au moteur
  
### <a name="setidentity-function"></a>SetIdentity fonction)
Définit l' [identité](class_mip_identity.md) de l’utilisateur associée au moteur.

Paramètres :  
* **identité**: [Identité](class_mip_identity.md) de l’utilisateur associée au moteur


  
### <a name="getclientdata-function"></a>GetClientData fonction)
Obtient les données personnalisées spécifiées par le client.

  
**Retourne**: Données personnalisées spécifiées par le client
  
### <a name="setclientdata-function"></a>SetClientData fonction)
Définit les données personnalisées spécifiées par le client.

Paramètres :  
* **Custom** : données spécifiées par le client


  
### <a name="getlocale-function"></a>GetLocale fonction)
Obtient les paramètres régionaux selon lesquels les données du moteur seront écrites.

  
**Retourne**: Paramètres régionaux dans lesquels les données du moteur seront écrites
  
### <a name="setcustomsettings-function"></a>SetCustomSettings fonction)
Définit les paires nom/valeur utilisées pour les tests et l’expérimentation.

Paramètres :  
* **customSettings**: Paires nom/valeur utilisées pour les tests et l’expérimentation


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient les paires nom/valeur utilisées pour les tests et l’expérimentation.

  
**Retourne**: Paires nom/valeur utilisées pour les tests et l’expérimentation
  
### <a name="setsessionid-function"></a>SetSessionId fonction)
Définit l’ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie.

Paramètres :  
* **SessionID**: ID de session du moteur, utilisé pour la corrélation de la journalisation/télémétrie


  
### <a name="getsessionid-function"></a>GetSessionId fonction)
Obtient l’ID de session du moteur.

  
**Retourne**: ID de session du moteur
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl fonction)
Définit éventuellement l’URL de base du point de terminaison cloud.

Paramètres :  
* **cloudEndpointBaseUrl** : URL de base utilisée par toutes les demandes de service (par exemple, « https://api.aadrm.com  »)


Si l’URL de base n’est pas spécifiée, elle sera déterminée par le biais de la recherche DNS du domaine de l’identité du moteur.
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl function
Obtient l’URL de base du cloud utilisée par toutes les demandes de service, si elle est spécifiée.

  
**Retourne**: URL de base