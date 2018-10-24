---
title: mip ProtectionDescriptor, classe
description: Informations de référence pour la classe mip ProtectionDescriptor
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e723041af1eec7be7a839bf36f6d3db67b32447f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446547"
---
# <a name="class-mipprotectiondescriptor"></a>class mip::ProtectionDescriptor 
Description de la protection associée à un élément de contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  Obtient le type de protection, issue du modèle de SDK de protection ou non.
 public std::string GetOwner() const  |  Obtient le propriétaire de la protection.
 public std::string GetName() const  |  Obtient le nom de la protection.
 public std::string GetDescription() const  |  Obtient la description de la protection.
 public std::string GetTemplateId() const  |  Obtient l’ID du modèle de protection, le cas échéant.
 public std::string GetLabelId() const  |  Obtient l’ID de l’étiquette, le cas échéant.
public std::vector<UserRights> GetUserRights() const  |  Obtient la collection de mappages utilisateurs-droits.
public std::vector<UserRoles> GetUserRoles() const  |  Obtient la collection de mappages utilisateurs-rôles.
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil() const  |  Obtient l’heure d’expiration de la protection.
 public bool DoesAllowOfflineAccess() const  |  Indique si la protection autorise l’accès au contenu hors connexion ou non.
 public std::string GetReferrer() const  |  Obtient l’adresse du référent de protection.
public std::map<std::string, std::string> GetEncryptedAppData() const  |  Obtient les données propres à l’application qui ont été chiffrées.
public std::map<std::string, std::string> GetSignedAppData() const  |  Obtient les données spécifiques de l’application qui ont été signées.
  
## <a name="members"></a>Membres
  
### <a name="protectiontype"></a>ProtectionType
Obtient le type de protection, issue du modèle de SDK de protection ou non.

  
**Retourne** : le type de protection
  
### <a name="getowner"></a>GetOwner
Obtient le propriétaire de la protection.

  
**Retourne** : propriétaire de la protection
  
### <a name="getname"></a>GetName
Obtient le nom de la protection.

  
**Retourne** : nom de la protection
  
### <a name="getdescription"></a>GetDescription
Obtient la description de la protection.

  
**Retourne** : description de la protection
  
### <a name="gettemplateid"></a>GetTemplateId
Obtient l’ID du modèle de protection, le cas échéant.

  
**Retourne** : ID du modèle
  
### <a name="getlabelid"></a>GetLabelId
Obtient l’ID de l’étiquette, le cas échéant.

  
**Retourne** : ID de [l’étiquette](class_mip_label.md). Cette propriété sera uniquement remplie dans ProtectionDescriptors pour le contenu protégé préexistant. Il s’agit d’un champ rempli par le serveur au moment où le contenu protégé est utilisé.
  
### <a name="userrights"></a>UserRights
Obtient la collection de mappages utilisateurs-droits.

  
**Retourne** : collection de mappages utilisateurs-droits. La valeur de la propriété [UserRights](class_mip_userrights.md) est vide si l’utilisateur actif n’a pas accès à ces informations (c’est-à-dire s’il n’est pas le propriétaire et qu’il ne dispose pas du droit VIEWRIGHTSDATA).
  
### <a name="userroles"></a>UserRoles
Obtient la collection de mappages utilisateurs-rôles.

  
**Retourne** : la collection de mappages utilisateurs-rôles
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtient l’heure d’expiration de la protection.

  
**Retourne** : heure d’expiration de la protection
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Indique si la protection autorise l’accès au contenu hors connexion ou non.

  
**Retourne** : valeur indiquant si la protection autorise l’accès au contenu hors connexion ou non (valeur par défaut = True)
  
### <a name="getreferrer"></a>GetReferrer
Obtient l’adresse du référent de protection.

  
**Retourne** : adresse du référent de protection. Le référent est un URI qui peut être affiché pour l’utilisateur s’il ne peut pas ôter la protection du contenu. Il contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
Obtient les données propres à l’application qui ont été chiffrées.

  
**Retourne** : données spécifiques à l’application. Un [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire des données spécifiques à l’application qui ont été chiffrées par le service de protection. Ces données chiffrées ne dépendent pas des données signées accessibles par [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata)
  
### <a name="getsignedappdata"></a>GetSignedAppData
Obtient les données spécifiques de l’application qui ont été signées.

  
**Retourne** : données spécifiques à l’application. Un [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire des données spécifiques à l’application qui ont été signées par le service de protection. Ces données signées ne dépendent pas des données chiffrées accessibles par [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata)