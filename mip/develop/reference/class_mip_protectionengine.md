---
title: mip ProtectionEngine, classe
description: Informations de référence pour la classe mip ProtectionEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ddc8cfd58acb2a80d024978084b625f3d3728c87
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446734"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
Gère les actions liées à la protection sur une identité spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtient les paramètres du moteur.
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public std::vector<std::string> GetTemplates(const std::shared_ptr<void>& context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public void GetRightsForLabelIdAsync(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.
public std::vector<std::string> GetRightsForLabelId(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<void>& context)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.
public void GetGrantingLabelIdsAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtenir la collection des ID d’étiquettes disponibles pour un utilisateur.
public std::vector<std::string> GetGrantingLabelIds(const std::shared_ptr<void>& context)  |  Obtenir la collection des ID d’étiquettes disponibles pour un utilisateur.
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromDescriptor(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicense(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.
public void CreateProtectionHandlerFromPublishingLicenseContextAsync(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection à partir d’un contexte de licence de publication.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicenseContext(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crée un gestionnaire de protection à partir d’un contexte de licence de publication.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtient les paramètres du moteur.

  
**Retourne**  : les paramètres du moteur
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **observer** : classe qui implémente l’interface [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context** : contexte client qui est repassé de façon opaque aux observateurs et à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative


  
### <a name="gettemplates"></a>GetTemplates
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **context** : contexte client qui est passé de façon opaque à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative



  
**Retourne** : liste des ID de modèles
  
### <a name="getrightsforlabelidasync"></a>GetRightsForLabelIdAsync
Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.

Paramètres :  
* **documentId** : ID de document associé aux métadonnées de document 


* **labelId** : ID [d’étiquette](class_mip_label.md) associé aux métadonnées de document avec lesquelles le document est créé 


* **ownerEmail** : propriétaire du document 


* **observer** : classe qui implémente l’interface [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context** : ce même contexte sera transféré à [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) ou [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)


  
### <a name="getrightsforlabelid"></a>GetRightsForLabelId
Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.

Paramètres :  
* **documentId** : ID de document associé aux métadonnées de document 


* **labelId** : ID [d’étiquette](class_mip_label.md) associé aux métadonnées de document avec lesquelles le document est créé 


* **ownerEmail** : propriétaire du document 


* **context** : ce même contexte sera transféré à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative



  
**Retourne** : liste des droits
  
### <a name="getgrantinglabelidsasync"></a>GetGrantingLabelIdsAsync
Obtenir la collection des ID d’étiquettes disponibles pour un utilisateur.

Paramètres :  
* **observer** : classe qui implémente l’interface [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context** : ce même contexte sera transféré à [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) ou ProtectionEngine::Observer::OnGrantingLabelIdsFailure


  
### <a name="getgrantinglabelids"></a>GetGrantingLabelIds
Obtenir la collection des ID d’étiquettes disponibles pour un utilisateur.

Paramètres :  
* **context** : ce même contexte sera transféré à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative



  
**Retourne** : liste des ID d’étiquettes
  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **descriptor** : un [ProtectionDescriptor](class_mip_protectiondescriptor.md) décrivant la configuration de la protection 


* **options** : options de création 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context** : contexte client qui est repassé de façon opaque aux observateurs et à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative


  
### <a name="protectionhandler"></a>ProtectionHandler
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **descriptor** : un [ProtectionDescriptor](class_mip_protectiondescriptor.md) décrivant la configuration de la protection 


* **options** : options de création 


* **context** : contexte client qui est repassé de façon opaque à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative



  
**Retourne** : [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.

Paramètres :  
* **serializedPublishingLicense** : licence de publication sérialisée 


* **options** : options de création 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context** : contexte client qui est repassé de façon opaque aux observateurs et à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative


  
### <a name="protectionhandler"></a>ProtectionHandler
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.

Paramètres :  
* **serializedPublishingLicense** : licence de publication sérialisée 


* **options** : options de création 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context** : contexte client qui est repassé de façon opaque à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative



  
**Retourne** : [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync
Crée un gestionnaire de protection à partir d’un contexte de licence de publication.

Paramètres :  
* **publishingLicenseContext** : forme prétraitée de la licence de publication sérialisée 


* **options** : options de création 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context** : contexte client qui est repassé de façon opaque aux observateurs et à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative


  
### <a name="protectionhandler"></a>ProtectionHandler
Crée un gestionnaire de protection à partir d’un contexte de licence de publication.

Paramètres :  
* **publishingLicenseContext** : forme prétraitée de la licence de publication sérialisée 


* **options** : options de création 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


* **context** : contexte client qui est repassé de façon opaque à l’interface [HttpDelegate](class_mip_httpdelegate.md) facultative



  
**Retourne** : [ProtectionHandler](class_mip_protectionhandler.md)