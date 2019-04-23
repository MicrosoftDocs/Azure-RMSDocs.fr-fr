---
title: class mip::ProtectionDescriptor
description: Décrit la classe mip::protectiondescriptor de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6f4bb83950a4745739a1663950a52d05c51f7f4d
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173290"
---
# <a name="class-mipprotectiondescriptor"></a>class mip::ProtectionDescriptor 
Description de la protection associée à un élément de contenu.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  Obtient le type de protection, issue du modèle de SDK de protection ou non.
public std::string GetOwner() const  |  Obtient le propriétaire de la protection.
public std::string GetName() const  |  Obtient le nom de la protection.
public std::string GetDescription() const  |  Obtient la description de la protection.
public std::string GetTemplateId() const  |  Obtient l’ID du modèle de protection, le cas échéant.
public std::string GetLabelId() const  |  Obtient l’ID de l’étiquette, le cas échéant.
public std::string GetContentId() const  |  Obtient l’ID de contenu, le cas échéant.
public std::vector\<UserRights\> GetUserRights() const  |  Obtient la collection de mappages utilisateurs-droits.
public std::vector\<UserRoles\> GetUserRoles() const  |  Obtient la collection de mappages utilisateurs-rôles.
public bool DoesContentExpire() const  |  Vérifie si contenu a un délai d’expiration ou non.
public std::chrono::time_point\<std::chrono::system_clock\> GetContentValidUntil() const  |  Obtient l’heure d’expiration de la protection.
public bool DoesAllowOfflineAccess() const  |  Indique si la protection autorise l’accès au contenu hors connexion ou non.
public std::string GetReferrer() const  |  Obtient l’adresse du référent de protection.
public std::map\<std::string, std::string\> GetEncryptedAppData() const  |  Obtient les données propres à l’application qui ont été chiffrées.
public std::map\<std::string, std::string\> GetSignedAppData() const  |  Obtient les données spécifiques de l’application qui ont été signées.
  
## <a name="members"></a>Membres
  
### <a name="getprotectiontype-function"></a>GetProtectionType function
Obtient le type de protection, issue du modèle de SDK de protection ou non.

  
**Retourne**: Type de protection
  
### <a name="getowner-function"></a>GetOwner (fonction)
Obtient le propriétaire de la protection.

  
**Retourne**: Propriétaire de la protection
  
### <a name="getname-function"></a>GetName (fonction)
Obtient le nom de la protection.

  
**Retourne**: Nom de la protection
  
### <a name="getdescription-function"></a>GetDescription (fonction)
Obtient la description de la protection.

  
**Retourne**: Description de la protection
  
### <a name="gettemplateid-function"></a>GetTemplateId (fonction)
Obtient l’ID du modèle de protection, le cas échéant.

  
**Retourne**: ID de modèle
  
### <a name="getlabelid-function"></a>GetLabelId (fonction)
Obtient l’ID de l’étiquette, le cas échéant.

  
**Retourne**: [Étiquette](class_mip_label.md) ID de cette propriété sera uniquement remplie dans ProtectionDescriptors pour préexistant du contenu protégé. Il s’agit d’un champ rempli par le serveur au moment où le contenu protégé est utilisé.
  
### <a name="getcontentid-function"></a>GetContentId (fonction)
Obtient l’ID de contenu, le cas échéant.

  
**Retourne**: ID de contenu
  
### <a name="getuserrights-function"></a>GetUserRights (fonction)
Obtient la collection de mappages utilisateurs-droits.

  
**Retourne**: Collection de mappages utilisateurs-droits la valeur de la [UserRights](class_mip_userrights.md) propriété sera vide si l’utilisateur actuel n’a pas accès à ces informations (autrement dit, si l’utilisateur n’est pas le propriétaire et ne dispose pas du droit VIEWRIGHTSDATA).
  
### <a name="getuserroles-function"></a>GetUserRoles (fonction)
Obtient la collection de mappages utilisateurs-rôles.

  
**Retourne**: Collection de mappages utilisateurs-rôles
  
### <a name="doescontentexpire-function"></a>DoesContentExpire (fonction)
Vérifie si contenu a un délai d’expiration ou non.

  
**Retourne**: True si le contenu peut expirer ; sinon, false
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil function
Obtient l’heure d’expiration de la protection.

  
**Retourne**: Délai d’expiration de protection
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess (fonction)
Indique si la protection autorise l’accès au contenu hors connexion ou non.

  
**Retourne**: Si la protection permet l’accès au contenu hors connexion ou non (valeur par défaut = true)
  
### <a name="getreferrer-function"></a>GetReferrer (fonction)
Obtient l’adresse du référent de protection.

  
**Retourne**: Adresse du référent de protection. le référent est un URI qui est affichable à l’utilisateur si elles ne peuvent pas ôter la protection du contenu. Il contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData (fonction)
Obtient les données propres à l’application qui ont été chiffrées.

  
**Retourne**: Données spécifiques de l’application A [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire des données spécifiques de l’application qui a été chiffrés par le service de protection. Ces données chiffrées sont indépendantes des données signées accessibles par le biais de ProtectionDescriptor::GetSignedAppData.
  
### <a name="getsignedappdata-function"></a>GetSignedAppData function
Obtient les données spécifiques de l’application qui ont été signées.

  
**Retourne**: Données spécifiques de l’application A [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire des données spécifiques de l’application qui a été signés par le service de protection. Ces données signées ne dépendent pas des données chiffrées accessibles par [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata-function)