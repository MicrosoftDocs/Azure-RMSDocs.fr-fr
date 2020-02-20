---
title: mip::FileProfile, classe
description: 'Documente la classe MIP :: fileprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 44d6024473555c0745ff3156ff5cd004f83b6f6b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488141"
---
# <a name="class-mipfileprofile"></a>mip::FileProfile, classe 
La classe FileProfile est la classe racine pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’un seul profil.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres de profil.
public std :: shared_ptr\<AsyncControl\> ListEnginesAsync (const std :: shared_ptr\<void\>& contexte)  |  Démarre une opération d’énumération de moteurs.
public std :: shared_ptr\<AsyncControl\> UnloadEngineAsync (const std :: String & ID, const std :: shared_ptr\<void\>contexte &)  |  Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public std :: shared_ptr\<AsyncControl\> AddEngineAsync (const FileEngine :: Settings & Settings, const std :: shared_ptr\<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de fichier au profil.
public std :: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std :: String & ID, const std :: shared_ptr\<void\>contexte &)  |  Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Retourne les paramètres de profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync fonction)
Démarre le déchargement du moteur de fichier avec l’ID spécifié.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de fichier au profil.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile :: observer est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile :: observer est appelé en cas de réussite ou d’échec.