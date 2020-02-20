---
title: class mip::ProtectionEngine
description: Documente la classe MIP ::p rotectionengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 23f9f54a3f9701d0c9321b7ba643ed7dd3f47be1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486832"
---
# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
Gère les actions liées à la protection sur une identité spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres du moteur.
public std :: shared_ptr\<AsyncControl\> GetTemplatesAsync (const std :: shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& contexte)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public std :: Vector\<std :: shared_ptr\<TemplateDescriptor\>\> GetTemplates (const std :: shared_ptr\<void\>& contexte)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public bool IsFeatureSupported (FeatureId featureId)  |  Vérifiez que la fonctionnalité est prise en charge.
public std :: shared_ptr\<AsyncControl\> GetRightsForLabelIdAsync (const std :: String & documentId, const std :: String & ID, const std :: String & ownerEmail, const std :: String & delegatedUserEmail, const std :: shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& contexte)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.
public std :: Vector\<std :: String\> GetRightsForLabelId (const std :: String & documentId, const std :: String & ID, const std :: String & ownerEmail, const std :: String & delegatedUserEmail, const std :: shared_ptr\<void\>contexte &)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.
public std :: shared_ptr\<AsyncControl\> CreateProtectionHandlerForPublishingAsync (const ProtectionHandler ::P ublishingSettings & Settings, const std :: shared_ptr\<ProtectionHandler :: observer\>& observateur, const std :: shared_ptr\<void\>contexte &)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std :: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler ::P ublishingSettings & Settings, const std :: shared_ptr\<void\>con& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std :: shared_ptr\<AsyncControl\> CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler :: ConsumptionSettings & Settings, const std :: shared_ptr\<ProtectionHandler :: observer\>& observateur, const std :: shared_ptr\<void\>contexte &)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std :: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler :: ConsumptionSettings & Settings, const std :: shared_ptr\<void\>con& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public bool LoadUserCert (const std :: shared_ptr\<void\>& Context)  |  Chargez de manière préventive le certificat de licence utilisateur, utile lorsque le chargement en arrière-plan à l’aide de la prélicence peut entraîner un appel réseau supplémentaire.
public std :: shared_ptr\<AsyncControl\> LoadUserCertAsync (const std :: shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& contexte)  |  Chargez de manière préventive le certificat de licence utilisateur, utile lorsque le chargement en arrière-plan à l’aide de la prélicence peut entraîner un appel réseau supplémentaire.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtient les paramètres du moteur.

  
**Retourne**  : les paramètres du moteur
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **observer**: classe implémentant l’interface ProtectionEngine :: observer 


* **Context**: contexte client qui sera retourné de manière opaque aux observateurs et facultatif HttpDelegate



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="gettemplates-function"></a>GetTemplates fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **Context**: contexte client qui sera transmis de manière opaque à un HttpDelegate facultatif



  
**Retourne** : liste des ID de modèles
  
### <a name="isfeaturesupported-function"></a>IsFeatureSupported fonction)
Vérifiez que la fonctionnalité est prise en charge.

Paramètres :  
* **FeatureId**: ID de la fonctionnalité à vérifier



  
**Retourne**: résultat booléen
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync fonction)
Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.

Paramètres :  
* **documentId** : ID de document associé aux métadonnées de document 


* **ID**: ID d’étiquette associé aux métadonnées de document avec lesquelles le document a été créé 


* **ownerEmail** : propriétaire du document 


* **R : un**utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit pour le compte d’un autre utilisateur, vide si aucun 


* **observer**: classe implémentant l’interface ProtectionEngine :: observer 


* **contexte**: ce même contexte sera transféré à ProtectionEngine :: observer :: OnGetRightsForLabelIdSuccess ou ProtectionEngine :: observer :: OnGetRightsForLabelIdFailure



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId fonction)
Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.

Paramètres :  
* **documentId** : ID de document associé aux métadonnées de document 


* **ID**: ID d’étiquette associé aux métadonnées de document avec lesquelles le document a été créé 


* **ownerEmail** : propriétaire du document 


* **R : un**utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit pour le compte d’un autre utilisateur, vide si aucun 


* **contexte**: ce même contexte sera transféré à un HttpDelegate facultatif



  
**Retourne** : liste des droits
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: paramètres de protection 


* **observer**: classe implémentant l’interface ProtectionHandler :: observer 


* **Context**: contexte client qui sera transféré opaque aux observateurs et facultatif HttpDelegate



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="createprotectionhandlerforpublishing-function"></a>CreateProtectionHandlerForPublishing fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: paramètres de protection 


* **Context**: contexte client qui sera transféré opaque au HttpDelegate facultatif



  
**Retourne**: ProtectionHandler
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: paramètres de protection 


* **observer**: classe implémentant l’interface ProtectionHandler :: observer 


* **Context**: contexte client qui sera transféré opaque aux observateurs et facultatif HttpDelegate



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: paramètres de protection 


* **Context**: contexte client qui sera transféré opaque au HttpDelegate facultatif



  
**Retourne**: ProtectionHandler
  
### <a name="loadusercert-function"></a>LoadUserCert fonction)
Chargez de manière préventive le certificat de licence utilisateur, utile lorsque le chargement en arrière-plan à l’aide de la prélicence peut entraîner un appel réseau supplémentaire.

Paramètres :  
* **Context**: contexte client qui sera transféré opaque au HttpDelegate facultatif



  
**Retourne**: true si le chargement a réussi, sinon false.
  
### <a name="loadusercertasync-function"></a>LoadUserCertAsync fonction)
Chargez de manière préventive le certificat de licence utilisateur, utile lorsque le chargement en arrière-plan à l’aide de la prélicence peut entraîner un appel réseau supplémentaire.

Paramètres :  
* **observer**: classe implémentant l’interface ProtectionHandler :: observer 


* **Context**: contexte client qui sera transféré opaque aux observateurs et facultatif HttpDelegate



  
**Retourne**: objet de contrôle asynchrone.