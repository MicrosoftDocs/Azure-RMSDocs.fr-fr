---
title: 'MIP ::P rotectionHandler :: ConsumptionSettings'
description: Documente la classe MIP ::p rotectionhandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 63a7f3c377a40a5faf82afe332a12efed0d646c4
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560725"
---
# <a name="class-mipprotectionhandlerconsumptionsettings"></a>MIP ::P rotectionHandler :: ConsumptionSettings 
Paramètres utilisés pour créer un ProtectionHandler pour utiliser le contenu existant.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std :: Vector\<uint8_t\>& serializedPublishingLicense)  |  ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.
public ConsumptionSettings (const std :: shared_ptr\<PublishingLicenseInfo\>& licenseInfo)  |  ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.
public std :: shared_ptr\<PublishingLicenseInfo\> GetPublishingLicenseInfo () const  |  Procurez-vous la licence de publication associée au contenu protégé.
public bool GetIsOfflineOnly () const  |  Obtient une valeur indiquant si la création de ProtectionHandler autorise ou non les opérations HTTP en ligne.
public void SetIsOfflineOnly (bool isOfflineOnly)  |  Définit si la création de ProtectionHandler autorise ou non les opérations HTTP en ligne.
public void SetDelegatedUserEmail (const std :: String & delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std :: String & GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
  
## <a name="members"></a>Membres
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings fonction)
ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.

Paramètres :  
* **serializedPublishingLicense**: licence de publication sérialisée à partir du contenu protégé


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings fonction)
ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.

Paramètres :  
* **licenseInfo**: publication des informations de licence à partir du contenu protégé


Le fait de fournir un PublishingLicenseInfo (par opposition à une seule licence de publication sérialisée brute) supprime la nécessité pour le SDK MIP d’analyser la licence de publication.
  
### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo fonction)
Procurez-vous la licence de publication associée au contenu protégé.

  
**Retourne**: publication des informations de licence
  
### <a name="getisofflineonly-function"></a>GetIsOfflineOnly fonction)
Obtient une valeur indiquant si la création de ProtectionHandler autorise ou non les opérations HTTP en ligne.

  
**Retourne**: true si les opérations http ne sont pas autorisées. sinon, false si la valeur est true, la création de ProtectionHandler réussit uniquement si le contenu a déjà été déchiffré précédemment et que sa licence non expirée est mise en cache. Une exception MIP :: NetworkError est levée si le contenu mis en cache est introuvable.
  
### <a name="setisofflineonly-function"></a>SetIsOfflineOnly fonction)
Définit si la création de ProtectionHandler autorise ou non les opérations HTTP en ligne.

Paramètres :  
* **isOfflineOnly**: true si les opérations http ne sont pas autorisées, sinon false.


Si la valeur est true, la création de ProtectionHandler réussit uniquement si le contenu a déjà été déchiffré précédemment et que sa licence non expirée est mise en cache. Une exception MIP :: NetworkError est levée si le contenu mis en cache est introuvable.
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail fonction)
Définit l’utilisateur délégué.

Paramètres :  
* **delegatedUserEmail**: e-mail de délégation.


Un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit au nom d’un autre utilisateur