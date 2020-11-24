---
title: ProtectionHandler de classe ::P ublishingSettings
description: Documente la classe protectionhandler ::p ublishingsettings du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c5edcb9eca5e14d0f0f611f32e2f91d9ed2fcb25
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567117"
---
# <a name="class-protectionhandlerpublishingsettings"></a>ProtectionHandler de classe ::P ublishingSettings 
Paramètres utilisés pour créer un ProtectionHandler pour protéger un nouveau contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public PublishingSettings (const std :: shared_ptr \<ProtectionDescriptor\>& protectionDescriptor)  |  ProtectionHandler :: Settings, constructeur pour la création d’un nouveau moteur.
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  | _Pas encore documenté._
public bool GetIsAuditedExtractionAllowed () const  |  Obtient une valeur indiquant si des applications prenant en charge les non-MIP sont autorisées ou non pour ouvrir du contenu protégé.
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)  |  Définit si les applications prenant en charge non MIP sont autorisées ou non pour ouvrir du contenu protégé.
public bool GetIsDeprecatedAlgorithmPreferred () const  |  Obtient une valeur indiquant si l’algorithme de chiffrement (ECB) déconseillé est préféré pour la compatibilité descendante.
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)  |  Définit si l’algorithme de chiffrement déconseillé (ECB) est préféré pour la compatibilité descendante.
public void SetDelegatedUserEmail (const std :: String& delegatedUserEmail)  |  Définit l’utilisateur délégué.
public const std :: String& GetDelegatedUserEmail () const  |  Obtient l’utilisateur délégué.
public bool IsPublishingFormatJson () const  |  Obtient une valeur indiquant si le pl retourné est au format JSON (le format XML est plus largement accepté et est la valeur par défaut).
public void SetPublishingFormatJson (bool isPublishingFormatJson)  |  indique si le pl renvoyé est au format JSON (le format XML est plus largement accepté et est la valeur par défaut).
public void SetPreLicenseUserEmail (const std :: String& preLicenseUserEmail)  |  Définit l’utilisateur de pré-licence.
public const std :: String& GetPreLicenseUserEmail () const  |  Obtient l’utilisateur de pré-licence.
  
## <a name="members"></a>Membres
  
### <a name="publishingsettings-function"></a>PublishingSettings fonction)
ProtectionHandler :: Settings, constructeur pour la création d’un nouveau moteur.

Paramètres :  
* **protectionDescriptor**: détails de la protection


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor fonction)
Pas encore documenté.

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed fonction)
Obtient une valeur indiquant si des applications prenant en charge les non-MIP sont autorisées ou non pour ouvrir du contenu protégé.

  
**Retourne**: si des applications prenant en charge non MIP sont autorisées à ouvrir du contenu protégé
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed fonction)
Définit si les applications prenant en charge non MIP sont autorisées ou non pour ouvrir du contenu protégé.

Paramètres :  
* **isAuditedExtractionAllowed**: si les applications prenant en charge non MIP sont autorisées à ouvrir du contenu protégé


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred fonction)
Obtient une valeur indiquant si l’algorithme de chiffrement (ECB) déconseillé est préféré pour la compatibilité descendante.

  
**Retourne**: si l’algorithme de chiffrement deprectated est préféré
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred fonction)
Définit si l’algorithme de chiffrement déconseillé (ECB) est préféré pour la compatibilité descendante.

Paramètres :  
* **Si**: l’algorithme de chiffrement deprectated est préféré


  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail fonction)
Définit l’utilisateur délégué.

Paramètres :  
* **delegatedUserEmail**: e-mail de délégation.


Un utilisateur délégué est spécifié quand l’utilisateur ou l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail fonction)
Obtient l’utilisateur délégué.

  
**Retourne**: utilisateur délégué un utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit au nom d’un autre utilisateur
  
### <a name="ispublishingformatjson-function"></a>IsPublishingFormatJson fonction)
Obtient une valeur indiquant si le pl retourné est au format JSON (le format XML est plus largement accepté et est la valeur par défaut).

  
**Retourne** la valeur true si a la valeur de la sortie au format JSON.
  
### <a name="setpublishingformatjson-function"></a>SetPublishingFormatJson fonction)
indique si le pl renvoyé est au format JSON (le format XML est plus largement accepté et est la valeur par défaut).

Paramètres :  
* **isPublishingFormatJson**: si le format JSON est activé.


  
### <a name="setprelicenseuseremail-function"></a>SetPreLicenseUserEmail fonction)
Définit l’utilisateur de pré-licence.

Paramètres :  
* **preLicenseUserEmail**: utilisateur de pré-licence


Si aucun utilisateur de pré-licence n’est spécifié, une pré-licence ne sera pas obtenue
  
### <a name="getprelicenseuseremail-function"></a>GetPreLicenseUserEmail fonction)
Obtient l’utilisateur de pré-licence.

  
**Retourne**: utilisateur de pré-licence