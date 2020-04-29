---
title: ProtectionEngine de classe
description: 'Documente la classe protectionengine :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 61311ec2ac7c622099e9e7f56f22191e0287278c
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763905"
---
# <a name="class-protectionengine"></a>ProtectionEngine de classe 
Gère les actions liées à la protection sur une identité spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres du moteur.
public std :: shared_ptr\<AsyncControl\> GetTemplatesAsync (const std :: Shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& Context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public std :: Vector\<std :: shared_ptr\<TemplateDescriptor\> \> GetTemplates (const std :: shared_ptr\<void\>& Context)  |  Obtient la collection de modèles disponibles pour un utilisateur.
public bool IsFeatureSupported (FeatureId featureId)  |  Vérifiez que la fonctionnalité est prise en charge.
public std :: shared_ptr\<AsyncControl\> GetRightsForLabelIdAsync (const std :: String& DocumentID, const std :: String& ID, const std :: String& ownerEmail, const std :: String& delegatedUserEmail, const std :: Shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& Context)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un ID d’étiquette.
public std :: Vector\<std :: String\> GetRightsForLabelId (const std :: String& DocumentID, const std :: String& ID, const std :: String& ownerEmail, const std :: String& delegatedUserEmail, const std :: shared_ptr\<void\>& Context)  |  Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.
public std :: shared_ptr\<AsyncControl\> CreateProtectionHandlerForPublishingAsync (const ProtectionHandler ::P ublishingsettings& Settings, const std ::\<shared_ptr ProtectionHandler ::\> observer& observateur, const std ::\<shared_ptr\> void& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std :: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler ::P ublishingsettings& Settings, const std ::\<shared_ptr\> void& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std :: shared_ptr\<AsyncControl\> CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler :: ConsumptionSettings& Settings, const std ::\<shared_ptr ProtectionHandler ::\> observer& observateur, const std ::\<shared_ptr\> void& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public std :: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler :: ConsumptionSettings& Settings, const std ::\<shared_ptr\> void& Context)  |  Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.
public bool LoadUserCert (const std :: shared_ptr\<void\>& Context)  |  Chargez de manière préventive le certificat de licence utilisateur, utile lorsque le chargement en arrière-plan à l’aide de la prélicence peut entraîner un appel réseau supplémentaire.
public std :: shared_ptr\<AsyncControl\> LoadUserCertAsync (const std :: Shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& Context)  |  Chargez de manière préventive le certificat de licence utilisateur, utile lorsque le chargement en arrière-plan à l’aide de la prélicence peut entraîner un appel réseau supplémentaire.
public void RegisterContentForTrackingAndRevocation (const std :: Vector\<Uint8_t\>& serializedPublishingLicense, const std :: String& ContentName, bool isOwnerNotificationEnabled, const std :: shared_ptr\<void\>& Context)  |  Enregistrez la licence de publication (PL) pour le suivi des documents & la révocation.
public std :: shared_ptr\<AsyncControl\> RegisterContentForTrackingAndRevocationAsync (const std :: Vector\<uint8_t\>& serializedPublishingLicense, const std :: String& ContentName, bool isOwnerNotificationEnabled, const std :: shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& Context)  |  Enregistrez la licence de publication (PL) pour le suivi des documents & la révocation.
public void RevokeContent (const std :: Vector\<Uint8_t\>& serializedPublishingLicense, const std :: shared_ptr\<void\>& Context)  |  Procédez à la révocation du contenu.
public std :: shared_ptr\<AsyncControl\> RevokeContentAsync (const std :: Vector\<uint8_t\>& serializedPublishingLicense, const std :: shared_ptr\<ProtectionEngine :: observer\>& observateur, const std :: shared_ptr\<void\>& Context)  |  Procédez à la révocation du contenu.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtient les paramètres du moteur.

  
**Retourne ** : les paramètres du moteur
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **observer** : classe qui implémente l’interface [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context** : contexte client qui est repassé de façon opaque aux observateurs et à l’interface HttpDelegate facultative



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="gettemplates-function"></a>GetTemplates fonction)
Obtient la collection de modèles disponibles pour un utilisateur.

Paramètres :  
* **context** : contexte client qui est passé de façon opaque à l’interface HttpDelegate facultative



  
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


* **ownerEmail**: propriétaire du document 


* **R : un**utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit pour le compte d’un autre utilisateur, vide si aucun 


* **observer** : classe qui implémente l’interface ProtectionEngine::Observer 


* **context** : ce même contexte sera transféré à ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess ou ProtectionEngine::Observer::OnGetRightsForLabelIdFailure



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId fonction)
Obtenir la collection des droits disponibles pour un utilisateur pour un labelId.

Paramètres :  
* **documentId** : ID de document associé aux métadonnées de document 


* **ID**: ID d’étiquette associé aux métadonnées de document avec lesquelles le document a été créé 


* **ownerEmail** : propriétaire du document 


* **R : un**utilisateur délégué est spécifié quand l’utilisateur/l’application d’authentification agit pour le compte d’un autre utilisateur, vide si aucun 


* **context** : ce même contexte sera transféré à l’interface HttpDelegate facultative



  
**Retourne** : liste des droits
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync fonction)
Crée un gestionnaire de protection où les droits/rôles sont attribués à des utilisateurs spécifiques.

Paramètres :  
* **paramètres**: paramètres de protection 


* **observer** : classe qui implémente l’interface [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 


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


* **observer** : classe qui implémente l’interface ProtectionHandler::Observer 


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
* **observer** : classe qui implémente l’interface ProtectionHandler::Observer 


* **Context**: contexte client qui sera transféré opaque aux observateurs et facultatif HttpDelegate



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="registercontentfortrackingandrevocation-function"></a>RegisterContentForTrackingAndRevocation fonction)
Enregistrez la licence de publication (PL) pour le suivi des documents & la révocation.

Paramètres :  
* **ContentName**: nom à associer au contenu spécifié par serializedPublishingLicense. Si le serializedPublishingLicense spécifie un nom de contenu, cette valeur est prioritaire. 


* **isOwnerNotificationEnabled**: affectez la valeur true pour informer le propriétaire par courrier électronique chaque fois que le document est déchiffré, ou false pour ne pas envoyer la notification. 


* **Context**: contexte client qui sera transféré opaque au HttpDelegate facultatif


  
### <a name="registercontentfortrackingandrevocationasync-function"></a>RegisterContentForTrackingAndRevocationAsync fonction)
Enregistrez la licence de publication (PL) pour le suivi des documents & la révocation.

Paramètres :  
* **serializedPublishingLicense**: licence de publication sérialisée à partir du contenu protégé 


* **ContentName**: nom à associer au contenu spécifié par serializedPublishingLicense. Si le serializedPublishingLicense spécifie un nom de contenu, cette valeur est prioritaire 


* **isOwnerNotificationEnabled**: affectez la valeur true pour informer le propriétaire par courrier électronique chaque fois que le document est déchiffré, ou false pour ne pas envoyer la notification. 


* **observer** : classe qui implémente l’interface ProtectionHandler::Observer 


* **Context**: contexte client qui sera transféré opaque aux observateurs et facultatif HttpDelegate



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="revokecontent-function"></a>RevokeContent fonction)
Procédez à la révocation du contenu.

Paramètres :  
* **serializedPublishingLicense**: licence de publication sérialisée à partir du contenu protégé 


* **Context**: contexte client qui sera transféré opaque au HttpDelegate facultatif


  
### <a name="revokecontentasync-function"></a>RevokeContentAsync fonction)
Procédez à la révocation du contenu.

Paramètres :  
* **serializedPublishingLicense**: licence de publication sérialisée à partir du contenu protégé 


* **observer** : classe qui implémente l’interface ProtectionHandler::Observer 


* **Context**: contexte client qui sera transféré opaque aux observateurs et facultatif HttpDelegate



  
**Retourne**: objet de contrôle asynchrone.