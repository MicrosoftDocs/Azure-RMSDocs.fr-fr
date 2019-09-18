---
title: mip::FileProfile, classe
description: 'Documente la classe MIP :: fileprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 9971ae734b17186bd9ba942ca7dc991ab3e4ef15
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070609"
---
# <a name="class-mipfileprofile"></a>mip::FileProfile, classe 
La classe [FileProfile](class_mip_fileprofile.md) est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’un seul profil.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres de profil.
public void ListEnginesAsync (const std :: shared_ptr\<void\>& Context)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public void AddEngineAsync (const FileEngine :: Settings & Settings, const std :\<:\>shared_ptr void & Context)  |  Démarre l’ajout d’un nouveau moteur de fichier au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
public static FILE_API void _ _ cdecl Mip :: FileProfile :: LoadAsync | Démarre le chargement d’un profil en fonction des paramètres fournis
public static const FILE_API Char * _ _ cdecl Mip :: FileProfile :: GetVersion | Obtient la version de la bibliothèque.


## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Retourne les paramètres de profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync fonction)
Démarre le déchargement du moteur de fichier avec l’ID spécifié.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de fichier au profil.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.

### <a name="loadasync-function"></a>LoadAsync, fonction
Démarre le chargement d’un profil en fonction des paramètres fournis.

[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.

### <a name="getversion-function"></a>GetVersion, fonction
Obtient la version de la bibliothèque.
