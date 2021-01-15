---
title: PublishingLicenseInfo de classe
description: 'Documente la classe publishinglicenseinfo :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: b16c58d7faeea7b91ced99f0a1fc786701ad12a2
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213281"
---
# <a name="class-publishinglicenseinfo"></a>PublishingLicenseInfo de classe 
Contient les détails d’une licence de publication utilisée pour créer un gestionnaire de protection.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public PublishingLicenseInfo (const std :: Vector \<uint8_t\>& serializedPublishingLicense)  | _Pas encore documenté._
public PublishingLicenseInfo (const std :: Vector \<uint8_t\>& serializedPreLicense, const std :: vector \<uint8_t\>& serializedPublishingLicense)  | _Pas encore documenté._
public void SetParsedData (const std :: Vector \<std::string\>& domaines, const std :: string& serverPublicCert, const std :: string& ContentId, const std :: string& issuerId)  | _Pas encore documenté._
public void SetDoubleKeyData (const std :: String& algorithme, const std :: map \<std::string, std::string\>& doubleKeyApplicationData)  | _Pas encore documenté._
public const std :: Vector \<uint8_t\>& GetSerializedPublishingLicense () const  | _Pas encore documenté._
public const std :: Vector \<uint8_t\>& GetPreLicense () const  | _Pas encore documenté._
public const std :: Vector \<std::string\>& GetDomains () const  | _Pas encore documenté._
public const std :: String& GetServerPublicCertificate () const  | _Pas encore documenté._
public const std :: String& GetIssuerId () const  | _Pas encore documenté._
public const std :: String& GetContentId () const  | _Pas encore documenté._
public bool IsLicenseParsed () const  | _Pas encore documenté._
public bool HasPreLicense () const  | _Pas encore documenté._
public bool GetIsDoubleKeyLicense () const  | _Pas encore documenté._
public const std :: String& GetDoubleKeyAlgorithm () const  | _Pas encore documenté._
public const std :: map \<std::string, std::string\>& GetDoubleKeyApplicationData () const  | _Pas encore documenté._
  
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
