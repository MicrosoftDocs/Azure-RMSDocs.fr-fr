---
title: 'MIP :: MipContext, classe'
description: 'Documente la classe MIP :: mipcontext du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 9efbe9330014458a26f62e4dfac9ea24ad5d4475
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73561028"
---
# <a name="class-mipmipcontext"></a>MIP :: MipContext, classe 
MipContext représente l’état partagé par tous les profils, moteurs et gestionnaires.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void ShutDown ()  |  Arrêtez MIP.
public bool IsFeatureEnabled (fonctionnalité FlightingFeature) const  |  Obtient une valeur indiquant si une fonctionnalité est activée ou non.
public const ApplicationInfo& GetApplicationInfo() const  |  Obtient la description de l’application.
public const std :: String & GetMipPath () const  |  Obtenir le chemin d’accès de fichier pour les journaux, les caches, etc.
public bool IsOfflineOnly ()  |  Obtient le paramètre en mode hors connexion uniquement.
public std :: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Obtient l’implémentation du journal.
public LoggerDelegate * GetRawLoggerDelegate ()  |  Obtient l’implémentation du journal.
public static MIP_API std :: shared_ptr&lt;MipContext&gt; __CDECL MIP :: MipContext :: Create | Créez une instance MipContext à utiliser lors de l’initialisation des profils.
public static MIP_API std :: shared_ptr&lt;MipContext&gt; __CDECL MIP :: MipContext :: CreateWithCustomFeatureSettings | Créez une nouvelle instance MipContext avec des paramètres de fonctionnalités personnalisés.

## <a name="members"></a>Membres
  
### <a name="shutdown-function"></a>Fonction ShutDown
Arrêtez MIP.
Cette méthode doit être appelée avant l’arrêt du processus/DLL
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled fonction)
Obtient une valeur indiquant si une fonctionnalité est activée ou non.

Paramètres :  
* **fonctionnalité**: fonctionnalité à activer/désactiver



  
**Retourne**: si une fonctionnalité est activée ou non si un FeatureFlightingDelegate n’a pas été fourni par une application, la valeur true est toujours retournée.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo fonction)
Obtient la description de l’application.

  
**Retourne**: description de l’application
  
### <a name="getmippath-function"></a>GetMipPath fonction)
Obtenir le chemin d’accès de fichier pour les journaux, les caches, etc.

  
**Retourne**: chemin d’accès au fichier (avec le répertoire feuille « MIP »)
  
### <a name="isofflineonly-function"></a>IsOfflineOnly fonction)
Obtient le paramètre en mode hors connexion uniquement.

  
**Retourne**: indique si l’application est en cours d’exécution en mode hors connexion uniquement
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate fonction)
Obtient l’implémentation du journal.

  
**Retourne** : enregistreur d’événements
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate fonction)
Obtient l’implémentation du journal.

  
**Retourne** : enregistreur d’événements

### <a name="create-function"></a>Créer une fonction
Créez une instance MipContext à utiliser lors de l’initialisation des profils.

**Retourne**: instance MipContext.

### <a name="createwithcustomfeaturesettings-function"></a>CreateWithCustomFeatureSettings fonction)
Créez une nouvelle instance MipContext avec des paramètres de fonctionnalités personnalisés.

**Retourne**: instance MipContext.