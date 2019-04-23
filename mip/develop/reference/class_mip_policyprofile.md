---
title: mip::PolicyProfile, classe
description: Décrit la classe mip::policyprofile de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 45af1f4d072a1d8a690aa8f459950ae500df3db8
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173335"
---
# <a name="class-mippolicyprofile"></a>mip::PolicyProfile, classe 
La classe [PolicyProfile](class_mip_policyprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [PolicyProfile](class_mip_policyprofile.md), mais elle peut créer plusieurs profils si nécessaire.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtenir les paramètres définis sur le profil.
public ListEnginesAsync void (const std::shared_ptr\<void\>& contexte)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr\<void\>& context)  |  Démarre l’ajout d’un nouveau moteur de stratégie au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings (fonction)
Obtenir les paramètres définis sur le profil.

  
**Retourne**: Paramètres définis sur le profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (fonction)
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (fonction)
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera transféré de façon opaque vers les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync-function"></a>AddEngineAsync (fonction)
Démarre l’ajout d’un nouveau moteur de stratégie au profil.

Paramètres :  
* **settings** : objet [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) qui spécifie les paramètres du moteur. 


* **context** : paramètre qui sera transféré de façon opaque vers les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (fonction)
Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.