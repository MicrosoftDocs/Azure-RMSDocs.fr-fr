---
title: class mip::ProtectionDescriptorBuilder
description: Documente la classe MIP::p rotectiondescriptorbuilder du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 7f177685cfb3314f201c56de59f47ea00d154fba
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057669"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
Construit un [ProtectionDescriptor](class_mip_protectiondescriptor.md) qui décrit la protection associée à un élément de contenu.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MIP_API std:: shared_ptr\<ProtectionDescriptor\> Build ()  |  Crée un [ProtectionDescriptor](class_mip_protectiondescriptor.md) dont les autorisations d’accès sont définies par cette instance [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
public void SetName(const std::string& value)  |  Définit un nom pour la stratégie de protection.
public void SetDescription(const std::string& value)  |  Définit la description de la stratégie de protection.
public void SetContentValidUntil (const std:: Chrono:: time_point\<std:: Chrono:: system_clock\>& value)  |  Définit l’heure d’expiration de la stratégie de protection.
public void SetAllowOfflineAccess(bool value)  |  Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.
public void SetReferrer(const std::string& uri)  |  Définit l’adresse du référent de stratégie de protection.
public void SetEncryptedAppData(const std::map\<std::string, std::string\>& value)  |  Définit les données spécifiques de l’application qui doivent être chiffrées.
public void SetSignedAppData(const std::map\<std::string, std::string\>& value)  |  Définit les données spécifiques de l’application qui doivent être signées.
public virtual ~ProtectionDescriptorBuilder()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="build-function"></a>Build, fonction
Crée un [ProtectionDescriptor](class_mip_protectiondescriptor.md) dont les autorisations d’accès sont définies par cette instance [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Retourne**: Nouvelle instance [ProtectionDescriptor](class_mip_protectiondescriptor.md)
  
### <a name="setname-function"></a>SetName fonction)
Définit un nom pour la stratégie de protection.

Paramètres :  
* **valeur**: Nom de la stratégie de protection


  
### <a name="setdescription-function"></a>SetDescription fonction)
Définit la description de la stratégie de protection.

Paramètres :  
* **valeur**: Description de la stratégie


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil function
Définit l’heure d’expiration de la stratégie de protection.

Paramètres :  
* **valeur**: Heure d’expiration de la stratégie


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess fonction)
Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.

Paramètres :  
* **valeur**: Si la stratégie autorise l’accès au contenu hors connexion


  
### <a name="setreferrer-function"></a>SetReferrer fonction)
Définit l’adresse du référent de stratégie de protection.

Paramètres :  
* **URI**: Adresse du référent de la stratégie


Le référent est un URI qui peut être montré à l’utilisateur en cas d’échec de l’acquisition de la stratégie de protection. L’URI contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData fonction)
Définit les données spécifiques de l’application qui doivent être chiffrées.

Paramètres :  
* **valeur**: Données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront chiffrées par le service de protection. Ces données chiffrées ne dépendent pas des données signées définies par SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>SetSignedAppData fonction)
Définit les données spécifiques de l’application qui doivent être signées.

Paramètres :  
* **valeur**: Données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront signées par le service de protection. Ces données signées ne dépendent pas des données chiffrées définies par SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder fonction)
_Pas encore documenté._
