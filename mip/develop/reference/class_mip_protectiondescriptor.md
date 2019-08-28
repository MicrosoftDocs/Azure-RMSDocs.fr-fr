---
title: class mip::ProtectionDescriptor
description: Documente la classe MIP::p rotectiondescriptor du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 9ea47c36df8077c711960d0dfadf84c2c055e1a5
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057699"
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
public std:: String GetContentId () const  |  Obtient l’ID de contenu, le cas échéant.
public std:: Vector\<UserRights\> GetUserRights () const  |  Obtient la collection de mappages utilisateurs-droits.
public std:: Vector\<UserRoles\> GetUserRoles () const  |  Obtient la collection de mappages utilisateurs-rôles.
public bool DoesContentExpire () const  |  Vérifie si le contenu a une heure d’expiration ou non.
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetContentValidUntil () const  |  Obtient l’heure d’expiration de la protection.
public bool DoesAllowOfflineAccess() const  |  Indique si la protection autorise l’accès au contenu hors connexion ou non.
public std::string GetReferrer() const  |  Obtient l’adresse du référent de protection.
public std::map\<std::string, std::string\> GetEncryptedAppData() const  |  Obtient les données propres à l’application qui ont été chiffrées.
public std::map\<std::string, std::string\> GetSignedAppData() const  |  Obtient les données spécifiques de l’application qui ont été signées.
  
## <a name="members"></a>Membres
  
### <a name="getprotectiontype-function"></a>GetProtectionType fonction)
Obtient le type de protection, issue du modèle de SDK de protection ou non.

  
**Retourne**: Type de protection
  
### <a name="getowner-function"></a>GetOwner fonction)
Obtient le propriétaire de la protection.

  
**Retourne**: Propriétaire de la protection
  
### <a name="getname-function"></a>Fonction GetName
Obtient le nom de la protection.

  
**Retourne**: Nom de la protection
  
### <a name="getdescription-function"></a>GetDescription, fonction
Obtient la description de la protection.

  
**Retourne**: Description de la protection
  
### <a name="gettemplateid-function"></a>GetTemplateId fonction)
Obtient l’ID du modèle de protection, le cas échéant.

  
**Retourne**: ID de modèle
  
### <a name="getlabelid-function"></a>GetLabelId fonction)
Obtient l’ID de l’étiquette, le cas échéant.

  
**Retourne**: [Étiquette](class_mip_label.md) ID cette propriété sera remplie uniquement dans ProtectionDescriptors pour le contenu protégé préexistant. Il s’agit d’un champ rempli par le serveur au moment où le contenu protégé est utilisé.
  
### <a name="getcontentid-function"></a>GetContentId fonction)
Obtient l’ID de contenu, le cas échéant.

  
**Retourne**: ID de contenu
  
### <a name="getuserrights-function"></a>GetUserRights fonction)
Obtient la collection de mappages utilisateurs-droits.

  
**Retourne**: Collection de mappages utilisateurs-droits la valeur de la propriété [UserRights](class_mip_userrights.md) est vide si l’utilisateur actuel n’a pas accès à ces informations (autrement dit, si l’utilisateur n’est pas le propriétaire et qu’il n’a pas le droit VIEWRIGHTSDATA).
  
### <a name="getuserroles-function"></a>GetUserRoles fonction)
Obtient la collection de mappages utilisateurs-rôles.

  
**Retourne**: Collection de mappages utilisateurs-rôles
  
### <a name="doescontentexpire-function"></a>DoesContentExpire fonction)
Vérifie si le contenu a une heure d’expiration ou non.

  
**Retourne**: True si le contenu peut expirer, sinon false
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil function
Obtient l’heure d’expiration de la protection.

  
**Retourne**: Heure d’expiration de la protection
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess fonction)
Indique si la protection autorise l’accès au contenu hors connexion ou non.

  
**Retourne**: Si la protection autorise l’accès au contenu hors connexion (valeur par défaut = true)
  
### <a name="getreferrer-function"></a>GetReferrer fonction)
Obtient l’adresse du référent de protection.

  
**Retourne**: Adresse du point de vue de la protection le référent est un URI affichable par l’utilisateur s’il ne peut pas ôter la protection du contenu. Il contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData fonction)
Obtient les données propres à l’application qui ont été chiffrées.

  
**Retourne**: Données spécifiques à l’application un [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire de données spécifiques à l’application qui ont été chiffrées par le service de protection. Ces données chiffrées ne dépendent pas des données signées accessibles par [ProtectionDescriptor::GetSignedAppData](#getsignedappdata-function)
  
### <a name="getsignedappdata-function"></a>GetSignedAppData fonction)
Obtient les données spécifiques de l’application qui ont été signées.

  
**Retourne**: Données spécifiques à l’application un [ProtectionHandler](class_mip_protectionhandler.md) peut contenir un dictionnaire des données spécifiques à l’application qui ont été signées par le service de protection. Ces données signées ne dépendent pas des données chiffrées accessibles par [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata-function)