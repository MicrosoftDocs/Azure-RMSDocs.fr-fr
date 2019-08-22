---
title: class mip::ProtectionEngine
description: Documente la classe MIP::p rotectionengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 88cb6565e8e392a83d01ded79186cf7dbb6fb43c
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883492"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
Gère les actions liées à la protection sur une identité spécifique.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres du moteur.
public void GetTemplatesAsync (const std:: shared_ptr\<ProtectionEngine:: observer\>& observateur, const std:: shared_ptr\<void\>& Context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public std:: Vector\<std:: String\> GetTemplates (const std:: shared_ptr\<void\>& Context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public void GetRightsForLabelIdAsync (const std:: String & documentID, const std:: String & ID, const std:: String & ownerEmail, const std:: String & delegatedUserEmail, const std:: shared_ptr\<ProtectionEngine:: O bserver\>& observer, const std:: shared_ptr\<void\>& Context)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.
public std:: Vector\<std:: String\> GetRightsForLabelId (const std:: String & documentID, const std:: String & ID, const std:: String & ownerEmail, const std:: String & delegatedUserEmail, const std:: Shared _PTR\<void\>& Context)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.
public void CreateProtectionHandlerFromDescriptorAsync (const std:: shared_ptr\<ProtectionDescriptor\>descripteur &, const ProtectionHandlerCreationOptions & options, const std:\< : shared_ptr ProtectionHandler:: observer\>& observateur, const std:: shared_ptr\<void\>& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std:: shared_ptr\<ProtectionDescriptor\>& descripteur, const ProtectionHandlerCreationOptions options &, const std:: shared_ptr\<void\>& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public void CreateProtectionHandlerFromPublishingLicenseAsync (const std:: Vector\<uint8_t\>& serializedPublishingLicense, const ProtectionHandlerCreationOptions & options, const std:: shared_ptr\<ProtectionHandler:: observer\>& observateur, const std:: shared_ptr\<void\>& Context)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std:: Vector\<uint8_t\>& serializedPublishingLicense, const ProtectionHandlerCreationOptions & options, const std:: shared_ptr\<void\>& Context)  |  Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.
public void CreateProtectionHandlerForPublishingAsync (const ProtectionHandler::P ublishingsettings & Settings, const std::\<shared_ptr ProtectionHandler::\>observer & observateur, const std:: shared_ptr\<void\>& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler::P ublishingsettings & Settings, const std::\<shared_ptr\>void & Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public void CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings & Settings, const std::\<shared_ptr ProtectionHandler::\>observer & observer, const std:: shared_ptr\<void\>& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler:: ConsumptionSettings & Settings, const std::\<shared_ptr\>void & contexte )  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtient les paramètres du moteur.

  
**Retourne**: Paramètres du moteur
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **Observateur**: Une classe implémentant l’interface [ProtectionEngine:: observer](class_mip_protectionengine_observer.md) 


* **contexte**: Contexte client qui sera retourné de manière opaque aux observateurs et facultatif [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="gettemplates-function"></a>GetTemplates fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **contexte**: Contexte client qui sera transmis de manière opaque à un [HttpDelegate](class_mip_httpdelegate.md) facultatif



  
**Retourne**: Liste des ID de modèle
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync fonction)
Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.

Paramètres :  
* **DocumentID**: ID de document associé aux métadonnées de document 


* **ID**: [Étiquette](class_mip_label.md) ID associé aux métadonnées de document avec lesquelles le document a été créé 


* **ownerEmail** : propriétaire du document 


* **R: un**utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit pour le compte d’un autre utilisateur, vide si aucun 


* **Observateur**: Une classe implémentant l’interface [ProtectionEngine:: observer](class_mip_protectionengine_observer.md) 


* **contexte**: Ce même contexte sera transféré à [ProtectionEngine:: observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) ou [ProtectionEngine:: observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId fonction)
Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.

Paramètres :  
* **DocumentID**: ID de document associé aux métadonnées de document 


* **ID**: [Étiquette](class_mip_label.md) ID associé aux métadonnées de document avec lesquelles le document a été créé 


* **ownerEmail**: Propriétaire du document 


* **R: un**utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit pour le compte d’un autre utilisateur, vide si aucun 


* **contexte**: Ce même contexte sera transféré à un [HttpDelegate](class_mip_httpdelegate.md) facultatif



  
**Retourne**: Liste des droits
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>CreateProtectionHandlerFromDescriptorAsync fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* descripteur: [ProtectionDescriptor](class_mip_protectiondescriptor.md) décrivant la configuration de la protection 


* **options**: Options de création 


* **Observateur**: Une classe implémentant l’interface [ProtectionHandler:: observer](class_mip_protectionhandler_observer.md) 


* **contexte**: Contexte client qui sera retourné de manière opaque aux observateurs et facultatif [HttpDelegate](class_mip_httpdelegate.md)


> Déconseillé Cette méthode sera bientôt dépréciée en faveur de CreateProtectionHandlerForPublishingAsync
  
### <a name="createprotectionhandlerfromdescriptor-function"></a>CreateProtectionHandlerFromDescriptor fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* descripteur: [ProtectionDescriptor](class_mip_protectiondescriptor.md) décrivant la configuration de la protection 


* **options**: Options de création 


* **contexte**: Contexte client qui sera retourné de manière opaque à un [HttpDelegate](class_mip_httpdelegate.md) facultatif



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de CreateProtectionHandlerForPublishingAsync
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>CreateProtectionHandlerFromPublishingLicenseAsync fonction)
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.

Paramètres :  
* **serializedPublishingLicense**: Une licence de publication sérialisée 


* **options**: Options de création 


* **Observateur**: Une classe implémentant l’interface [ProtectionHandler:: observer](class_mip_protectionhandler_observer.md) 


* **contexte**: Contexte client qui sera retourné de manière opaque aux observateurs et facultatif [HttpDelegate](class_mip_httpdelegate.md)


> Déconseillé Cette méthode sera bientôt dépréciée en faveur de CreateProtectionHandlerForConsumptionAsync
  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>CreateProtectionHandlerFromPublishingLicense fonction)
Crée un gestionnaire de protection à partir d’une licence de publication sérialisée.

Paramètres :  
* **serializedPublishingLicense**: Une licence de publication sérialisée 


* **options**: Options de création 


* **Observateur**: Une classe implémentant l’interface [ProtectionHandler:: observer](class_mip_protectionhandler_observer.md) 


* **contexte**: Contexte client qui sera retourné de manière opaque à un [HttpDelegate](class_mip_httpdelegate.md) facultatif



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)
> Déconseillé Cette méthode sera bientôt dépréciée en faveur de CreateProtectionHandlerForConsumption
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: Paramètres de protection 


* **Observateur**: Une classe implémentant l’interface [ProtectionHandler:: observer](class_mip_protectionhandler_observer.md) 


* **contexte**: Contexte client qui sera transmis de manière opaque aux observateurs et facultatif [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerforpublishing-function"></a>CreateProtectionHandlerForPublishing fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: Paramètres de protection 


* **contexte**: Contexte client qui sera transféré opaque au [HttpDelegate](class_mip_httpdelegate.md) facultatif



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: Paramètres de protection 


* **Observateur**: Une classe implémentant l’interface [ProtectionHandler:: observer](class_mip_protectionhandler_observer.md) 


* **contexte**: Contexte client qui sera transmis de manière opaque aux observateurs et facultatif [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: Paramètres de protection 


* **contexte**: Contexte client qui sera transféré opaque au [HttpDelegate](class_mip_httpdelegate.md) facultatif



  
**Retourne**: [ProtectionHandler](class_mip_protectionhandler.md)