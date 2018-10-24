---
title: mip ProtectionDescriptorBuilder, classe
description: Informations de référence pour la classe mip ProtectionDescriptorBuilder
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 42e44cfaf269a43d0210c0c040ea70ccc1fb192e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446632"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
Construit un [ProtectionDescriptor](class_mip_protectiondescriptor.md) qui décrit la protection associée à un élément de contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr<ProtectionDescriptor> Build()  |  Crée un [ProtectionDescriptor](class_mip_protectiondescriptor.md) dont les autorisations d’accès sont définies par cette instance [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
 public void SetName(const std::string& value)  |  Définit un nom pour la stratégie de protection.
 public void SetDescription(const std::string& value)  |  Définit la description de la stratégie de protection.
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  Définit l’heure d’expiration de la stratégie de protection.
 public void SetAllowOfflineAccess(bool value)  |  Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.
 public void SetReferrer(const std::string& uri)  |  Définit l’adresse du référent de stratégie de protection.
public void SetEncryptedAppData(const std::map<std::string, std::string>& value)  |  Définit les données spécifiques de l’application qui doivent être chiffrées.
public void SetSignedAppData(const std::map<std::string, std::string>& value)  |  Définit les données spécifiques de l’application qui doivent être signées.
 public virtual ~ProtectionDescriptorBuilder()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Crée un [ProtectionDescriptor](class_mip_protectiondescriptor.md) dont les autorisations d’accès sont définies par cette instance [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Retourne** : nouvelle instance [ProtectionDescriptor](class_mip_protectiondescriptor.md)
  
### <a name="setname"></a>SetName
Définit un nom pour la stratégie de protection.

Paramètres :  
* **value** : nom de la stratégie de protection


  
### <a name="setdescription"></a>SetDescription
Définit la description de la stratégie de protection.

Paramètres :  
* **value** : description de la stratégie


  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Définit l’heure d’expiration de la stratégie de protection.

Paramètres :  
* **value** : heure d’expiration de la stratégie


  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.

Paramètres :  
* **value** : valeur indiquant si la stratégie autorise l’accès au contenu hors connexion ou non


  
### <a name="setreferrer"></a>SetReferrer
Définit l’adresse du référent de stratégie de protection.

Paramètres :  
* **uri** : adresse du référent de la stratégie


Le référent est un URI qui peut être montré à l’utilisateur en cas d’échec de l’acquisition de la stratégie de protection. L’URI contient des informations sur la façon dont cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Définit les données spécifiques de l’application qui doivent être chiffrées.

Paramètres :  
* **value** : données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront chiffrées par le service de protection. Ces données chiffrées ne dépendent pas des données signées définies par SetSignedAppData.
  
### <a name="setsignedappdata"></a>SetSignedAppData
Définit les données spécifiques de l’application qui doivent être signées.

Paramètres :  
* **value** : données spécifiques à l’application


Une application peut spécifier un dictionnaire des données spécifiques à l’application qui seront signées par le service de protection. Ces données signées ne dépendent pas des données chiffrées définies par SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder"></a>~ProtectionDescriptorBuilder
_Pas encore documenté._
