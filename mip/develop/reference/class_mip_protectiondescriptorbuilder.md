---
title: ProtectionDescriptorBuilder de classe
description: 'Documente la classe protectiondescriptorbuilder :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2e5573a896ef0935c33e85a2ed7f73451ced8e7c
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567155"
---
# <a name="class-protectiondescriptorbuilder"></a>ProtectionDescriptorBuilder de classe 
Construit un ProtectionDescriptor qui décrit la protection associée à un élément de contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr\<ProtectionDescriptor\> Build()  |  Crée un ProtectionDescriptor dont les autorisations d’accès sont définies par cette instance ProtectionDescriptorBuilder.
public void SetName(const std::string& value)  |  Définit un nom pour la stratégie de protection.
public void SetDescription(const std::string& value)  |  Définit la description de la stratégie de protection.
public void SetContentValidUntil (const std :: Chrono :: time_point \<std::chrono::system_clock\>& valeur)  |  Définit l’heure d’expiration de la stratégie de protection.
public void SetAllowOfflineAccess(bool value)  |  Définit si la stratégie de protection autorise l’accès au contenu hors connexion ou non.
public void SetReferrer(const std::string& uri)  |  Définit l’adresse du référent de stratégie de protection.
public void SetEncryptedAppData (const std :: map \<std::string, std::string\>& valeur)  |  Définit les données spécifiques de l’application qui doivent être chiffrées.
public void SetSignedAppData (const std :: map \<std::string, std::string\>& valeur)  |  Définit les données spécifiques de l’application qui doivent être signées.
public void SetDoubleKeyUrl (const std :: String& doubleKeyUrl)  |  Définit l’URL de clé double à utiliser pour la protection personnalisée.
  
## <a name="members"></a>Membres
  
### <a name="build-function"></a>Build, fonction
Crée un ProtectionDescriptor dont les autorisations d’accès sont définies par cette instance ProtectionDescriptorBuilder.

  
**Retourne** : nouvelle instance ProtectionDescriptor
  
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
  
### <a name="setdoublekeyurl-function"></a>SetDoubleKeyUrl fonction)
Définit l’URL de clé double à utiliser pour la protection personnalisée.

Paramètres :  
* **valeur**: URL de clé double

