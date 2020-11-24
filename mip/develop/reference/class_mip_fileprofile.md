---
title: FileProfile de classe
description: 'Documente la classe fileprofile :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 6a7ed521ce5a277a72e8b151c8331d537484c86a
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566926"
---
# <a name="class-fileprofile"></a>FileProfile de classe 
La classe FileProfile est la classe de base pour l’utilisation des opérations Microsoft Information Protection.
Une application classique a besoin d’un seul profil.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres de profil.
public std :: shared_ptr \<AsyncControl\> ListEnginesAsync (const std :: shared_ptr \<void\> contexte&)  |  Démarre une opération d’énumération de moteurs.
public std :: shared_ptr \<AsyncControl\> UnloadEngineAsync (const std :: string& ID, const std :: shared_ptr \<void\>& Context)  |  Démarre le déchargement du moteur de fichier avec l’ID spécifié.
public std :: shared_ptr \<AsyncControl\> AddEngineAsync (const FileEngine :: settings& Settings, const std :: shared_ptr \<void\>& Context)  |  Démarre l’ajout d’un nouveau moteur de fichier au profil.
public std :: shared_ptr \<AsyncControl\> DeleteEngineAsync (const std :: string& ID, const std :: shared_ptr \<void\>& Context)  |  Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.
public void AcquirePolicyAuthToken (Cloud Cloud, const std :: shared_ptr \<AuthDelegate\>& authDelegate) const  |  Déclenchez un rappel d’authentification pour la stratégie.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Retourne les paramètres de profil.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync fonction)
Démarre une opération d’énumération de moteurs.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync fonction)
Démarre le déchargement du moteur de fichier avec l’ID spécifié.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="addengineasync-function"></a>AddEngineAsync fonction)
Démarre l’ajout d’un nouveau moteur de fichier au profil.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync fonction)
Démarre la suppression du moteur de fichier avec l’ID spécifié. Toutes les données du profil spécifié seront supprimées.

  
**Retourne**: objet de contrôle asynchrone.
FileProfile::Observer est appelé en cas de réussite ou d’échec.
  
### <a name="acquirepolicyauthtoken-function"></a>AcquirePolicyAuthToken fonction)
Déclenchez un rappel d’authentification pour la stratégie.

Paramètres :  
* **Cloud**: Cloud Azure 


* **authDelegate**: rappel d’authentification qui sera appelé


MIP ne met pas en cache ou ne fait rien d’autre avec la valeur retournée par le délégué auth. Cette fonction est recommandée pour les applications qui ne sont pas « connectées » jusqu’à ce que MIP demande un jeton d’authentification. Elle permet à une application d’extraire un jeton avant que MIP en ait réellement besoin.