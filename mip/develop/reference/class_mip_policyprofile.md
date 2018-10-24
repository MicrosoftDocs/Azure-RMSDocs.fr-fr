---
title: mip PolicyProfile, classe
description: Informations de référence pour la classe mip PolicyProfile
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 387e28780cb0ef02d56050f534d4783fdebc286e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446860"
---
# <a name="class-mippolicyprofile"></a>mip::PolicyProfile, classe 
La classe [PolicyProfile](class_mip_policyprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection. Une application classique a besoin d’une seule classe [PolicyProfile](class_mip_policyprofile.md), mais elle peut créer plusieurs profils si nécessaire.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtenir les paramètres définis sur le profil.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre le déchargement du moteur de stratégie avec l’ID spécifié.
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Démarre l’ajout d’un nouveau moteur de stratégie au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtenir les paramètres définis sur le profil.

  
**Retourne** : paramètres définis sur le profil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Démarre une opération d’énumération de moteurs.

Paramètres :  
* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Démarre le déchargement du moteur de stratégie avec l’ID spécifié.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera transféré de façon opaque vers les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync"></a>AddEngineAsync
Démarre l’ajout d’un nouveau moteur de stratégie au profil.

Paramètres :  
* **settings** : objet [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) qui spécifie les paramètres du moteur. 


* **context** : paramètre qui sera transféré de façon opaque vers les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Démarre la suppression du moteur de stratégie avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.

Paramètres :  
* **id** : ID unique du moteur. 


* **context** : paramètre qui sera passé dans les fonctions de l’observateur. 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) est appelé en cas de réussite ou d’échec.