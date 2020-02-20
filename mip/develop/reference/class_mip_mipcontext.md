---
title: 'MIP :: MipContext, classe'
description: 'Documente la classe MIP :: mipcontext du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 82c39cd6f716bde9232f6a5a461b2ffbfbae1dd0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489909"
---
# <a name="class-mipmipcontext"></a>MIP :: MipContext, classe 
MipContext représente l’état partagé par tous les profils, moteurs et gestionnaires.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void ShutDown ()  |  Arrêtez MIP.
public bool IsFeatureEnabled (fonctionnalité FlightingFeature) const  |  Obtient une valeur indiquant si une fonctionnalité est activée ou non.
public const ApplicationInfo& GetApplicationInfo() const  |  Obtient la description de l’application.
public const std :: String & GetMipPath () const  |  Obtenir le chemin d’accès de fichier pour les journaux, les caches, etc.
public bool IsOfflineOnly ()  |  Obtient le paramètre en mode hors connexion uniquement.
public LogLevel GetThresholdLogLevel () const  |  Obtient le niveau de journalisation du seuil.
public std :: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Obtient l’implémentation du journal.
public LoggerDelegate * GetRawLoggerDelegate ()  |  Obtient l’implémentation du journal.
  
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
  
### <a name="getthresholdloglevel-function"></a>GetThresholdLogLevel fonction)
Obtient le niveau de journalisation du seuil.

  
**Retourne**: niveau du journal de seuil
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate fonction)
Obtient l’implémentation du journal.

  
**Retourne** : enregistreur d’événements
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate fonction)
Obtient l’implémentation du journal.

  
**Retourne** : enregistreur d’événements