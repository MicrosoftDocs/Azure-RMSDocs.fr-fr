---
title: class mip::ProtectionDescriptorBuilder
description: Documente la classe MIP ::p rotectiondescriptorbuilder du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: cdc72fd45a4b82611aa02d0a9182cd829b6d8a9e
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560773"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
Construit un ProtectionDescriptor qui décrit la protection associée à un élément de contenu.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MIP_API std :: shared_ptr\<ProtectionDescriptor\> Build ()  |  Crée un ProtectionDescriptor dont les autorisations d’accès sont définies par cette instance ProtectionDescriptorBuilder.
public void SetName(const std::string& value)  |  Définit un nom pour la stratégie de protection.
public void SetDescription(const std::string& value)  |  Définit la description de la stratégie de protection.
public void SetContentValidUntil (const std :: Chrono :: time_point\<std :: Chrono :: system_clock\>& valeur)  |  Définit l’heure d’expiration de la stratégie de protection.
public void SetAllowOfflineAccess(bool value)  |  Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.
public void SetReferrer(const std::string& uri)  |  Définit l’adresse du référent de stratégie de protection.
public void SetEncryptedAppData (const std :: Map\<std :: String, std :: String\>& valeur)  |  Définit les données spécifiques de l’application qui doivent être chiffrées.
public void SetSignedAppData (const std :: Map\<std :: String, std :: String\>& valeur)  |  Définit les données spécifiques de l’application qui doivent être signées.
public virtual ~ProtectionDescriptorBuilder()  | Pas encore documenté.
public static MIP_API std :: shared_ptr&lt;ProtectionDescriptorBuilder&gt; MIP ::P rotectionDescriptorBuilder :: CreateFromUserRights | Crée un ProtectionDescriptorBuilder dont les autorisations d’accès sont définies par les utilisateurs et les droits.
public static MIP_API std :: shared_ptr&lt;ProtectionDescriptorBuilder&gt; MIP ::P rotectionDescriptorBuilder :: CreateFromUserRoles | Crée un ProtectionDescriptorBuilder dont les autorisations d’accès sont définies par les utilisateurs et les rôles.
public static MIP_API std :: shared_ptr&lt;ProtectionDescriptorBuilder&gt; MIP ::P rotectionDescriptorBuilder :: CreateFromTemplate | Crée un ProtectionDescriptorBuilder dont les autorisations d’accès sont définies par le modèle de protection. 

## <a name="members"></a>Membres
  
### <a name="build-function"></a>Build, fonction
Crée un ProtectionDescriptor dont les autorisations d’accès sont définies par cette instance ProtectionDescriptorBuilder.

  
**Retourne**: nouvelle instance ProtectionDescriptor
  
### <a name="setname-function"></a>SetName fonction)
Définit un nom pour la stratégie de protection.

Paramètres :  
* **value** : nom de la stratégie de protection


  
### <a name="setdescription-function"></a>SetDescription fonction)
Définit la description de la stratégie de protection.

Paramètres :  
* **value** : description de la stratégie


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil fonction)
Définit l’heure d’expiration de la stratégie de protection.

Paramètres :  
* **value** : heure d’expiration de la stratégie


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess fonction)
Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.

Paramètres :  
* **value** : valeur indiquant si la stratégie autorise l’accès au contenu hors connexion ou non


  
### <a name="setreferrer-function"></a>SetReferrer fonction)
Définit l’adresse du référent de stratégie de protection.

Paramètres :  
* **uri** : adresse du référent de la stratégie


Le référent est un URI qui peut être montré à l’utilisateur en cas d’échec de l’acquisition de la stratégie de protection. L’URI contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData fonction)
Définit les données spécifiques de l’application qui doivent être chiffrées.

Paramètres :  
* **value** : données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront chiffrées par le service de protection. Ces données chiffrées ne dépendent pas des données signées définies par SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>SetSignedAppData fonction)
Définit les données spécifiques de l’application qui doivent être signées.

Paramètres :  
* **value** : données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront signées par le service de protection. Ces données signées ne dépendent pas des données chiffrées définies par SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder fonction)
_Pas encore documenté._

### <a name="createfromuserrights-function"></a>CreateFromUserRights fonction)
Crée un ProtectionDescriptorBuilder dont les autorisations d’accès sont définies par les utilisateurs et les droits.

Paramètres :
* **usersAndRights**: collection de mappages utilisateurs-droits.

**Retourne** : nouvelle instance [ProtectionDescriptor](class_mip_protectiondescriptor.md) 

### <a name="createfromuserroles-function"></a>CreateFromUserRoles fonction)
Crée un ProtectionDescriptorBuilder dont les autorisations d’accès sont définies par les utilisateurs et les rôles.

Paramètres :
* **usersAndRoles**: collection de mappages utilisateurs-rôles.

**Retourne**: crée un [ProtectionDescriptor](class_mip_protectiondescriptor.md) dont les autorisations d’accès sont définies par les utilisateurs et les rôles.

### <a name="createfromtemplate-function"></a>CreateFromTemplate fonction)
Crée un ProtectionDescriptorBuilder dont les autorisations d’accès sont définies par le modèle de protection. 

Paramètres :
* **TemplateID**: ID de modèle de protection.

**Retourne**: une nouvelle instance [ProtectionDescriptor](class_mip_protectiondescriptor.md) .