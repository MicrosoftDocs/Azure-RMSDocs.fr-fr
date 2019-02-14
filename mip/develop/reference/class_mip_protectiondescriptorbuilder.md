---
title: class mip::ProtectionDescriptorBuilder
description: Décrit la classe mip::protectiondescriptorbuilder de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: e704dde11ab210638c4e1fd273bc0b1407817813
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252212"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
Construit un [ProtectionDescriptor](class_mip_protectiondescriptor.md) qui décrit la protection associée à un élément de contenu.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr MIP_API\<ProtectionDescriptor\> Build()  |  Crée un [ProtectionDescriptor](class_mip_protectiondescriptor.md) dont les autorisations d’accès sont définies par cette instance [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
public void SetName(const std::string& value)  |  Définit un nom pour la stratégie de protection.
public void SetDescription(const std::string& value)  |  Définit la description de la stratégie de protection.
public void SetContentValidUntil(const std::chrono::time_point\<std::chrono::system_clock\>& value)  |  Définit l’heure d’expiration de la stratégie de protection.
public void SetAllowOfflineAccess(bool value)  |  Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.
public void SetReferrer(const std::string& uri)  |  Définit l’adresse du référent de stratégie de protection.
public void SetEncryptedAppData(const std::map\<std::string, std::string\>& value)  |  Définit les données spécifiques de l’application qui doivent être chiffrées.
public void SetSignedAppData(const std::map\<std::string, std::string\>& value)  |  Définit les données spécifiques de l’application qui doivent être signées.
public virtual ~ProtectionDescriptorBuilder()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="build-function"></a>Build (fonction)
Crée un [ProtectionDescriptor](class_mip_protectiondescriptor.md) dont les autorisations d’accès sont définies par cette instance [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Retourne**: Nouvelle [ProtectionDescriptor](class_mip_protectiondescriptor.md) instance
  
### <a name="setname-function"></a>SetName (fonction)
Définit un nom pour la stratégie de protection.

Paramètres :  
* **Valeur**: Nom de stratégie de protection


  
### <a name="setdescription-function"></a>SetDescription (fonction)
Définit la description de la stratégie de protection.

Paramètres :  
* **Valeur**: Description de la stratégie


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil function
Définit l’heure d’expiration de la stratégie de protection.

Paramètres :  
* **Valeur**: Heure d’expiration de la stratégie


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess (fonction)
Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.

Paramètres :  
* **Valeur**: Si la stratégie autorise l’accès au contenu hors connexion ou non


  
### <a name="setreferrer-function"></a>SetReferrer (fonction)
Définit l’adresse du référent de stratégie de protection.

Paramètres :  
* **URI**: Adresse du référent de stratégie


Le référent est un URI qui peut être montré à l’utilisateur en cas d’échec de l’acquisition de la stratégie de protection. L’URI contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData (fonction)
Définit les données spécifiques de l’application qui doivent être chiffrées.

Paramètres :  
* **Valeur**: Données spécifiques de l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront chiffrées par le service de protection. Ces données chiffrées ne dépendent pas des données signées définies par SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>SetSignedAppData function
Définit les données spécifiques de l’application qui doivent être signées.

Paramètres :  
* **Valeur**: Données spécifiques de l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront signées par le service de protection. Ces données signées ne dépendent pas des données chiffrées définies par SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder (fonction)
_Pas encore documenté._
