---
title: mip::FileProfile, classe
description: 'Documente la classe MIP :: fileprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a436024aefe58a73ea03747fce5c5f2f4b4fc4b1
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558799"
---
# <a name="class-mipfileprofile"></a>mip::FileProfile, classe 
La classe FileProfile est la classe racine pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’un seul profil.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres de profil.
public void ListEnginesAsync (const std :: shared_ptr\<void\>& Context)  |  Démarre une opération d’énumération de moteurs.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public void AddEngineAsync (const FileEngine :: Settings & Settings, const std :: shared_ptr\<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de fichier au profil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
public static FILE_API void __CDECL MIP :: FileProfile :: LoadAsync | Démarre le chargement d’un profil en fonction des paramètres fournis
public static const FILE_API char * __CDECL MIP :: FileProfile :: GetVersion | Obtient la version de la bibliothèque.

## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Retourne les paramètres de profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.
FileProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync fonction)
Démarre le déchargement du moteur de fichier avec l’ID spécifié.
FileProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de fichier au profil.
FileProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
FileProfile :: observer est appelé en cas de réussite ou d’échec.

### <a name="loadasync-function"></a>LoadAsync, fonction
Démarre le chargement d’un profil en fonction des paramètres fournis.

[FileProfile::Observer](class_mip_fileprofile_observer.md) est appelé en cas de réussite ou d’échec.

### <a name="getversion-function"></a>GetVersion, fonction
Obtient la version de la bibliothèque.