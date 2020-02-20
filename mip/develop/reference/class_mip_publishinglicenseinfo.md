---
title: MIP de classe ::P ublishingLicenseInfo
description: Documente la classe MIP ::p ublishinglicenseinfo du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f9283a9cc52ef803e35a6d714e43bfce9b137771
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489637"
---
# <a name="class-mippublishinglicenseinfo"></a>MIP de classe ::P ublishingLicenseInfo 
Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public PublishingLicenseInfo (const std :: Vector\<uint8_t\>& serializedPublishingLicense)  | _Pas encore documenté._
public PublishingLicenseInfo (const std :: Vector\<uint8_t\>& serializedPreLicense, const std :: Vector\<uint8_t\>& serializedPublishingLicense)  | _Pas encore documenté._
public void SetParsedData (const std :: Vector\<std :: String\>& domaines, const std :: String & serverPublicCert, const std :: String & contentId, const std :: String & issuerId)  | _Pas encore documenté._
public void SetDoubleKeyData (const std :: String & algorithme, const std :: Map\<std :: String, std :: String\>& doubleKeyApplicationData)  | _Pas encore documenté._
public const std :: Vector\<uint8_t\>& GetSerializedPublishingLicense () const  | _Pas encore documenté._
public const std :: Vector\<uint8_t\>& GetPreLicense () const  | _Pas encore documenté._
public const std :: Vector\<std :: String\>& GetDomains () const  | _Pas encore documenté._
public const std :: String & GetServerPublicCertificate () const  | _Pas encore documenté._
public const std :: String & GetIssuerId () const  | _Pas encore documenté._
public const std :: String & GetContentId () const  | _Pas encore documenté._
public bool IsLicenseParsed () const  | _Pas encore documenté._
public bool HasPreLicense () const  | _Pas encore documenté._
public bool GetIsDoubleKeyLicense () const  | _Pas encore documenté._
public const std :: String & GetDoubleKeyAlgorithm () const  | _Pas encore documenté._
public const std :: Map\<std :: String, std :: String\>& GetDoubleKeyApplicationData () const  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="publishinglicenseinfo-function"></a>PublishingLicenseInfo fonction)
_Pas encore documenté._

  
### <a name="publishinglicenseinfo-function"></a>PublishingLicenseInfo fonction)
_Pas encore documenté._

  
### <a name="setparseddata-function"></a>SetParsedData fonction)
_Pas encore documenté._

  
### <a name="setdoublekeydata-function"></a>SetDoubleKeyData fonction)
_Pas encore documenté._

  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense fonction)
_Pas encore documenté._

  
### <a name="getprelicense-function"></a>GetPreLicense fonction)
_Pas encore documenté._

  
### <a name="getdomains-function"></a>GetDomains fonction)
_Pas encore documenté._

  
### <a name="getserverpubliccertificate-function"></a>GetServerPublicCertificate fonction)
_Pas encore documenté._

  
### <a name="getissuerid-function"></a>GetIssuerId fonction)
_Pas encore documenté._

  
### <a name="getcontentid-function"></a>GetContentId fonction)
_Pas encore documenté._

  
### <a name="islicenseparsed-function"></a>IsLicenseParsed fonction)
_Pas encore documenté._

  
### <a name="hasprelicense-function"></a>HasPreLicense fonction)
_Pas encore documenté._

  
### <a name="getisdoublekeylicense-function"></a>GetIsDoubleKeyLicense fonction)
_Pas encore documenté._

  
### <a name="getdoublekeyalgorithm-function"></a>GetDoubleKeyAlgorithm fonction)
_Pas encore documenté._

  
### <a name="getdoublekeyapplicationdata-function"></a>GetDoubleKeyApplicationData fonction)
_Pas encore documenté._
