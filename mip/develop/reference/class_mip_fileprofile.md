---
title: mip::FileProfile, classe
description: Décrit la classe mip::fileprofile de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: b9f5fba87246d0ce89c3e34733bf311b23478334
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60185128"
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