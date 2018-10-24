---
title: mip FileProfile, classe
description: Informations de référence pour la classe mip FileProfile
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: f317f1eff0266db1da211e164ec5e427ba7ce17d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445884"
---
# <a name="class-mipfileprofile"></a>mip::FileProfile, classe 
La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’un seul profil.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Retourne les paramètres de profil.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Démarre l’ajout d’un nouveau moteur de fichier au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Retourne les paramètres de profil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Démarre une opération d’énumération de moteurs.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Démarre le déchargement du moteur de fichier avec l’ID spécifié.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync"></a>AddEngineAsync
Démarre l’ajout d’un nouveau moteur de fichier au profil.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.