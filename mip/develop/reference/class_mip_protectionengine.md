---
title: class mip::ProtectionEngine
description: Décrit la classe mip::protectionengine de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 60a61f5e06b5e76cbf0c557e7d489a8d618a8261
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574146"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
Gère les actions liées à la protection sur une identité spécifique.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres du moteur.
public GetTemplatesAsync void (const std::shared_ptr\<ProtectionEngine::Observer\>& observer, const std::shared_ptr\<void\>& contexte)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public std::vector\<std::string\> GetTemplates(const std::shared_ptr\<void\>& context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public GetRightsForLabelIdAsync void (const std::string & documentId, const std::string & ID d’étiquette, const std::string & ownerEmail, const std::shared_ptr\<ProtectionEngine::Observer\>& observer, const std : : shared_ptr\<void\>& contexte)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.
public std::vector\<std::string\> GetRightsForLabelId(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr\<void\>& context)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.
public CreateProtectionHandlerFromDescriptorAsync void (const std::shared_ptr\<ProtectionDescriptor\>& descripteur, ProtectionHandlerCreationOptions constantes & options, const std::shared_ptr\< ProtectionHandler::Observer\>& observer, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std::shared_ptr\<ProtectionDescriptor\>& descripteur, ProtectionHandlerCreationOptions constantes & options, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public CreateProtectionHandlerFromPublishingLicenseAsync void (const std::vector\<uint8_t\>& serializedPublishingLicense, ProtectionHandlerCreationOptions constantes & options, const std::shared_ptr\<ProtectionHandler::Observer\>& observer, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std::vector\<uint8_t\>& serializedPublishingLicense, const ProtectionHandlerCreationOptions & options, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.
public CreateProtectionHandlerFromProtectionInfoAsync void (const std::vector\<uint8_t\>& serializedPublishingLicense, const std::vector\<uint8_t\>& serializedProtectionInfo, const std::shared_ptr\<ProtectionHandler::Observer\>& observer, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée et une information protection sérialisée.
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromProtectionInfo (const std::vector\<uint8_t\>& serializedPublishingLicense, const std::vector\< uint8_t\>& serializedProtectionInfo, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée et une information protection sérialisée.
public CreateProtectionHandlerFromPublishingLicenseContextAsync void (const std::shared_ptr const PublishingLicenseContext & publishingLicenseContext, ProtectionHandlerCreationOptions constantes & options,\< ProtectionHandler::Observer\>& observer, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection à partir d’un contexte de licence de publication.
public std::shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicenseContext (PublishingLicenseContext const & publishingLicenseContext, ProtectionHandlerCreationOptions constantes & Options, const std::shared_ptr\<void\>& contexte)  |  Crée un gestionnaire de protection à partir d’un contexte de licence de publication.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings (fonction)
Obtient les paramètres du moteur.

  
**Retourne**: Paramètres du moteur
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync (fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **Observateur**: Une classe qui implémente le [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) interface 


* **contexte**: Contexte du client qui sera opaque passé au observateurs et facultatifs [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="gettemplates-function"></a>GetTemplates (fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **contexte**: Contexte du client qui sera transmis de manière opaque à facultatif [HttpDelegate](class_mip_httpdelegate.md)



  
**Retourne**: Liste des ID de modèle.
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync function
Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.

Paramètres :  
* **documentId**: ID de document associé avec les métadonnées de document 


* **ID d’étiquette**: [Étiquette](class_mip_label.md) ID associé aux métadonnées de document avec lequel le document créé 


* **ownerEmail** : propriétaire du document 


* **Observateur**: Une classe qui implémente le [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) interface 


* **contexte**: Ce même contexte sera transféré vers [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) ou [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId function
Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.

Paramètres :  
* **documentId**: ID de document associé avec les métadonnées de document 


* **ID d’étiquette**: [Étiquette](class_mip_label.md) ID associé aux métadonnées de document avec lequel le document créé 


* **ownerEmail**: Propriétaire du document 


* **contexte**: Ce même contexte transmis comme facultatif [HttpDelegate](class_mip_httpdelegate.md)



  
**Retourne**: Liste des droits
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>CreateProtectionHandlerFromDescriptorAsync (fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **descriptor**: Un [ProtectionDescriptor](class_mip_protectiondescriptor.md) décrivant la configuration de protection 


* **options**: Options de création 


* **Observateur**: Une classe qui implémente le [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interface 


* **contexte**: Contexte du client qui sera opaque passé au observateurs et facultatifs [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfromdescriptor-function"></a>CreateProtectionHandlerFromDescriptor (fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **descriptor**: Un [ProtectionDescriptor](class_mip_protectiondescriptor.md) décrivant la configuration de protection 


* **options**: Options de création 


* **contexte**: Contexte du client qui sera transmis de manière opaque à l’option [HttpDelegate](class_mip_httpdelegate.md)



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>CreateProtectionHandlerFromPublishingLicenseAsync (fonction)
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.

Paramètres :  
* **serializedPublishingLicense**: Une licence de publication sérialisée 


* **options**: Options de création 


* **Observateur**: Une classe qui implémente le [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interface 


* **contexte**: Contexte du client qui sera opaque passé au observateurs et facultatifs [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>CreateProtectionHandlerFromPublishingLicense (fonction)
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.

Paramètres :  
* **serializedPublishingLicense**: Une licence de publication sérialisée 


* **options**: Options de création 


* **Observateur**: Une classe qui implémente le [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interface 


* **contexte**: Contexte du client qui sera transmis de manière opaque à l’option [HttpDelegate](class_mip_httpdelegate.md)



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfromprotectioninfoasync-function"></a>CreateProtectionHandlerFromProtectionInfoAsync (fonction)
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée et une information protection sérialisée.

Paramètres :  
* **serializedPublishingLicense**: Une licence de publication sérialisée 


* **serializedProtectionInfo**: Une information protection sérialisée 


* **Observateur**: Une classe qui implémente le [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interface 


* **contexte**: Contexte du client qui sera transmis de manière opaque à observateurs


  
### <a name="createprotectionhandlerfromprotectioninfo-function"></a>CreateProtectionHandlerFromProtectionInfo function
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée et une information protection sérialisée.

Paramètres :  
* **serializedPublishingLicense**: Une licence de publication sérialisée 


* **serializedProtectionInfo**: Une information protection sérialisée 


* **contexte**: Contexte du client qui sera transmis de manière opaque à observateurs



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync-function"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync function
Crée un gestionnaire de protection à partir d’un contexte de licence de publication.

Paramètres :  
* **publishingLicenseContext**: Une forme prétraitée de la licence de publication sérialisée 


* **options**: Options de création 


* **Observateur**: Une classe qui implémente le [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interface 


* **contexte**: Contexte du client qui sera opaque passé au observateurs et facultatifs [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicensecontext-function"></a>CreateProtectionHandlerFromPublishingLicenseContext function
Crée un gestionnaire de protection à partir d’un contexte de licence de publication.

Paramètres :  
* **publishingLicenseContext**: Une forme prétraitée de la licence de publication sérialisée 


* **options**: Options de création 


* **Observateur**: Une classe qui implémente le [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interface 


* **contexte**: Contexte du client qui sera transmis de manière opaque à l’option [HttpDelegate](class_mip_httpdelegate.md)



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)