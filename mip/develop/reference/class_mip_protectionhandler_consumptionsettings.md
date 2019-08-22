---
title: 'MIP::P rotectionHandler:: ConsumptionSettings'
description: Documente la classe MIP::p rotectionhandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 259c29cb0da2635bc1aa8973b5e975e526fb81b3
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893138"
---
# <a name="class-mipprotectionhandlerconsumptionsettings"></a>MIP::P rotectionHandler:: ConsumptionSettings 
Paramètres utilisés pour créer un [ProtectionHandler](class_mip_protectionhandler.md) pour utiliser le contenu existant.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std:: Vector\<uint8_t\>& serializedPublishingLicense)  | ProtectionHandler:: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.
public ConsumptionSettings (const std:: shared_ptr\<PublishingLicenseInfo\>& licenseInfo)  |  ProtectionHandler:: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.
public std:: shared_ptr\<PublishingLicenseInfo\> GetPublishingLicenseInfo () const  |  Procurez-vous la licence de publication associée au contenu protégé.
public bool GetIsOfflineOnly () const  |  Obtient une valeur indiquant si la création de [ProtectionHandler](class_mip_protectionhandler.md) autorise ou non les opérations http en ligne.
public void SetIsOfflineOnly (bool isOfflineOnly)  |  Définit si la création de [ProtectionHandler](class_mip_protectionhandler.md) autorise ou non les opérations http en ligne.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std:: String & GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
  
## <a name="members"></a>Membres
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings fonction)
ProtectionHandler:: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.

Paramètres :  
* **serializedPublishingLicense**: Licence de publication sérialisée à partir du contenu protégé


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings fonction)
ProtectionHandler:: ConsumptionSettings constructeur pour la création d’un nouveau gestionnaire.

Paramètres :  
* **licenseInfo**: Publication des informations de licence à partir du contenu protégé


Le fait de fournir un PublishingLicenseInfo (par opposition à une seule licence de publication sérialisée brute) supprime la nécessité pour le SDK MIP d’analyser la licence de publication.
  
### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo fonction)
Procurez-vous la licence de publication associée au contenu protégé.

  
**Retourne**: Publication des informations de licence
  
### <a name="getisofflineonly-function"></a>GetIsOfflineOnly fonction)
Obtient une valeur indiquant si la création de [ProtectionHandler](class_mip_protectionhandler.md) autorise ou non les opérations http en ligne.

  
**Retourne**: True si les opérations HTTP ne sont pas autorisées. sinon, false si la valeur est true, la création de [ProtectionHandler](class_mip_protectionhandler.md) réussit uniquement si le contenu a déjà été déchiffré précédemment et que sa licence non expirée est mise en cache. Un MIP:: NetworkError = est levé si le contenu mis en cache est introuvable.
  
### <a name="setisofflineonly-function"></a>SetIsOfflineOnly fonction)
Définit si la création de [ProtectionHandler](class_mip_protectionhandler.md) autorise ou non les opérations http en ligne.

Paramètres :  
* **isOfflineOnly**: True si les opérations HTTP ne sont pas autorisées, sinon false.


Si la valeur est true, la création de [ProtectionHandler](class_mip_protectionhandler.md) réussit uniquement si le contenu a déjà été déchiffré précédemment et que sa licence non expirée est mise en cache. Une exception MIP:: NetworkError est levée si le contenu mis en cache est introuvable.
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail fonction)
Définit l’utilisateur délégué.

Paramètres :  
* **delegatedUserEmail**: e-mail de délégation.


Un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: Utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur