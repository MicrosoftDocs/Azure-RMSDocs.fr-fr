---
title: 'classe ProtectionHandler :: ConsumptionSettings'
description: 'Documente la classe protectionhandler :: consumptionsettings du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 627845405fc0d4fc2523e958e2226d343d0013cc
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565544"
---
# <a name="class-protectionhandlerconsumptionsettings"></a>classe ProtectionHandler :: ConsumptionSettings 
Paramètres utilisés pour créer un ProtectionHandler pour utiliser le contenu existant.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std :: Vector \<uint8_t\>& serializedPublishingLicense)  |  ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.
public ConsumptionSettings (const std :: Vector \<uint8_t\>& serializedPreLicense, const std :: vector \<uint8_t\>& serializedPublishingLicense)  |  ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.
public ConsumptionSettings (const std :: shared_ptr \<PublishingLicenseInfo\>& licenseInfo)  |  ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.
public std :: shared_ptr \<PublishingLicenseInfo\> GetPublishingLicenseInfo () const  |  Procurez-vous la licence de publication associée au contenu protégé.
public bool GetIsOfflineOnly () const  |  Obtient une valeur indiquant si la création de ProtectionHandler autorise ou non les opérations HTTP en ligne.
public void SetIsOfflineOnly (bool isOfflineOnly)  |  Définit si la création de ProtectionHandler autorise ou non les opérations HTTP en ligne.
public void SetDelegatedUserEmail (const std :: String& delegatedUserEmail)  |  Définit l’utilisateur délégué.
public void SetContentName (const std :: String& contentName)  | _Pas encore documenté._
public const std :: String& GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
public const std :: String& GetContentName () const  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings fonction)
ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.

Paramètres :  
* **serializedPublishingLicense**: licence de publication sérialisée à partir du contenu protégé


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings fonction)
ProtectionHandler :: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.

Paramètres :  
* **serializedPreLicense**: pré-licence sérialisée de attaché au contenu. 


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
  
### <a name="setcontentname-function"></a>SetContentName fonction)
Pas encore documenté.

  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getcontentname-function"></a>GetContentName fonction)
Pas encore documenté.
