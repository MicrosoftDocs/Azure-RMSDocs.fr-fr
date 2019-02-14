---
title: mip::FileProfile, classe
description: Décrit la classe mip::fileprofile de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: f6578d4bb3a8926b38b02b06ca2ca525dc524582
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256326"
---
# <a name="class-mipfileprofile"></a>mip::FileProfile, classe 
La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’un seul profil.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres de profil.
public ListEnginesAsync void (const std::shared_ptr\<void\>& contexte)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr\<void\>& context)  |  Démarre l’ajout d’un nouveau moteur de fichier au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings (fonction)
Retourne les paramètres de profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (fonction)
Démarre une opération d’énumération de moteurs.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (fonction)
Démarre le déchargement du moteur de fichier avec l’ID spécifié.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync-function"></a>AddEngineAsync (fonction)
Démarre l’ajout d’un nouveau moteur de fichier au profil.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (fonction)
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
