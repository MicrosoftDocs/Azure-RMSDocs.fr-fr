---
title: PublishingLicenseInfo de classe
description: 'Documente la classe publishinglicenseinfo :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 362a5fe810a5244feef723563dfed910d0c88e62
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567077"
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
Pas encore documenté.

  
### <a name="publishinglicenseinfo-function"></a>PublishingLicenseInfo fonction)
Pas encore documenté.

  
### <a name="setparseddata-function"></a>SetParsedData fonction)
Pas encore documenté.

  
### <a name="setdoublekeydata-function"></a>SetDoubleKeyData fonction)
Pas encore documenté.

  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense fonction)
Pas encore documenté.

  
### <a name="getprelicense-function"></a>GetPreLicense fonction)
Pas encore documenté.

  
### <a name="getdomains-function"></a>GetDomains fonction)
Pas encore documenté.

  
### <a name="getserverpubliccertificate-function"></a>GetServerPublicCertificate fonction)
Pas encore documenté.

  
### <a name="getissuerid-function"></a>GetIssuerId fonction)
Pas encore documenté.

  
### <a name="getcontentid-function"></a>GetContentId fonction)
Pas encore documenté.

  
### <a name="islicenseparsed-function"></a>IsLicenseParsed fonction)
Pas encore documenté.

  
### <a name="hasprelicense-function"></a>HasPreLicense fonction)
Pas encore documenté.

  
### <a name="getisdoublekeylicense-function"></a>GetIsDoubleKeyLicense fonction)
Pas encore documenté.

  
### <a name="getdoublekeyalgorithm-function"></a>GetDoubleKeyAlgorithm fonction)
Pas encore documenté.

  
### <a name="getdoublekeyapplicationdata-function"></a>GetDoubleKeyApplicationData fonction)
Pas encore documenté.
