---
title: ProtectionDescriptor de classe
description: 'Documente la classe protectiondescriptor :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: b4257be5475b1225f79efe00c11df4b79ee67ee9
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763947"
---
# <a name="class-protectiondescriptor"></a>ProtectionDescriptor de classe 
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
public std :: String GetContentId () const  |  Obtient l’ID de contenu, le cas échéant.
public std :: Vector\<UserRights\> GetUserRights () const  |  Obtient la collection de mappages utilisateurs-droits.
public std :: Vector\<UserRoles\> GetUserRoles () const  |  Obtient la collection de mappages utilisateurs-rôles.
public bool DoesContentExpire () const  |  Vérifie si le contenu a une heure d’expiration ou non.
public std :: Chrono :: time_point\<std :: Chrono :: system_clock\> GetContentValidUntil () const  |  Obtient l’heure d’expiration de la protection.
public bool DoesAllowOfflineAccess() const  |  Indique si la protection autorise l’accès au contenu hors connexion ou non.
public std::string GetReferrer() const  |  Obtient l’adresse du référent de protection.
public std :: map\<std :: String, std :: String\> GetEncryptedAppData () const  |  Obtient les données propres à l’application qui ont été chiffrées.
public std :: map\<std :: String, std :: String\> GetSignedAppData () const  |  Obtient les données spécifiques de l’application qui ont été signées.
public std :: String GetDoubleKeyUrl () const  |  Obtient l’URL de clé double à utiliser pour la protection personnalisée.
  
## <a name="members"></a>Membres
  
### <a name="getprotectiontype-function"></a>GetProtectionType fonction)
Obtient le type de protection, issue du modèle de SDK de protection ou non.

  
**Retourne** : le type de protection
  
### <a name="getowner-function"></a>GetOwner fonction)
Obtient le propriétaire de la protection.

  
**Retourne** : propriétaire de la protection
  
### <a name="getname-function"></a>Fonction GetName
Obtient le nom de la protection.

  
**Retourne** : nom de la protection
  
### <a name="getdescription-function"></a>GetDescription, fonction
Obtient la description de la protection.

  
**Retourne** : description de la protection
  
### <a name="gettemplateid-function"></a>GetTemplateId fonction)
Obtient l’ID du modèle de protection, le cas échéant.

  
**Retourne**: ID de modèle
  
### <a name="getlabelid-function"></a>GetLabelId fonction)
Obtient l’ID de l’étiquette, le cas échéant.

  
**Retourne**: ID d’étiquette cette propriété sera remplie uniquement dans ProtectionDescriptors pour le contenu protégé préexistant. Il s’agit d’un champ rempli par le serveur au moment où le contenu protégé est utilisé.
  
### <a name="getcontentid-function"></a>GetContentId fonction)
Obtient l’ID de contenu, le cas échéant.

  
**Retourne**: ID de contenu
  
### <a name="getuserrights-function"></a>GetUserRights fonction)
Obtient la collection de mappages utilisateurs-droits.

  
**Retourne** : collection de mappages utilisateurs-droits. La valeur de la propriété [UserRights](class_mip_userrights.md) est vide si l’utilisateur actif n’a pas accès à ces informations (c’est-à-dire s’il n’est pas le propriétaire et qu’il ne dispose pas du droit VIEWRIGHTSDATA).
  
### <a name="getuserroles-function"></a>GetUserRoles fonction)
Obtient la collection de mappages utilisateurs-rôles.

  
**Retourne** : la collection de mappages utilisateurs-rôles
  
### <a name="doescontentexpire-function"></a>DoesContentExpire fonction)
Vérifie si le contenu a une heure d’expiration ou non.

  
**Retourne**la valeur true si le contenu peut expirer, sinon false.
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil fonction)
Obtient l’heure d’expiration de la protection.

  
**Retourne** : heure d’expiration de la protection
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess fonction)
Indique si la protection autorise l’accès au contenu hors connexion ou non.

  
**Retourne** : valeur indiquant si la protection autorise l’accès au contenu hors connexion ou non (valeur par défaut = True)
  
### <a name="getreferrer-function"></a>GetReferrer fonction)
Obtient l’adresse du référent de protection.

  
**Retourne** : adresse du référent de protection. Le référent est un URI qui peut être affiché pour l’utilisateur s’il ne peut pas ôter la protection du contenu. Il contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData fonction)
Obtient les données propres à l’application qui ont été chiffrées.

  
**Retourne** : données spécifiques à l’application. Un ProtectionHandler peut contenir un dictionnaire des données spécifiques à l’application qui ont été chiffrées par le service de protection. Ces données chiffrées sont indépendantes des données signées accessibles via ProtectionDescriptor :: GetSignedAppData.
  
### <a name="getsignedappdata-function"></a>GetSignedAppData fonction)
Obtient les données spécifiques de l’application qui ont été signées.

  
**Retourne** : données spécifiques à l’application. Un ProtectionHandler peut contenir un dictionnaire des données spécifiques à l’application qui ont été signées par le service de protection. Ces données signées sont indépendantes des données chiffrées accessibles via ProtectionDescriptor :: GetEncryptedAppData.
  
### <a name="getdoublekeyurl-function"></a>GetDoubleKeyUrl fonction)
Obtient l’URL de clé double à utiliser pour la protection personnalisée.

  
**Retourne**: URL de clé double URL de clé double utilisée dans les demandes personnalisées pour protéger les informations avec une deuxième clé