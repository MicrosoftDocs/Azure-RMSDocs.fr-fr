---
title: 'MIP:: MipContext, classe'
description: 'Documente la classe MIP:: mipcontext du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 1993756ee70788a71060484a52f0897d7d80c593
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69892764"
---
# <a name="class-mipmipcontext"></a>MIP:: MipContext, classe 
MipContext représente l’état partagé par tous les profils, moteurs et gestionnaires.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void ShutDown ()  |  Arrêtez MIP.
public bool IsFeatureEnabled (fonctionnalité FlightingFeature) const  |  Obtient une valeur indiquant si une fonctionnalité est activée ou non.
public const ApplicationInfo& GetApplicationInfo() const  |  Obtient la description de l’application.
public const std:: String & GetMipPath () const  |  Obtenir le chemin d’accès de fichier pour les journaux, les caches, etc.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Obtient l’implémentation du journal.
public LoggerDelegate * GetRawLoggerDelegate ()  |  Obtient l’implémentation du journal.
  
## <a name="members"></a>Membres
  
### <a name="shutdown-function"></a>Fonction ShutDown
Arrêtez MIP.
Cette méthode doit être appelée avant l’arrêt du processus/DLL
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled fonction)
Obtient une valeur indiquant si une fonctionnalité est activée ou non.

Paramètres :  
* **fonctionnalité**: Fonctionnalité à activer/désactiver



  
**Retourne**: Qu’une fonctionnalité soit activée ou non si un FeatureFlightingDelegate n’a pas été fourni par une application, la valeur true est toujours retournée.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo fonction)
Obtient la description de l’application.

  
**Retourne**: Description de l’application
  
### <a name="getmippath-function"></a>GetMipPath fonction)
Obtenir le chemin d’accès de fichier pour les journaux, les caches, etc.

  
**Retourne**: Chemin d’accès du fichier (avec le répertoire feuille «MIP»)
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate fonction)
Obtient l’implémentation du journal.

  
**Retourne**: Enregistreur
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate fonction)
Obtient l’implémentation du journal.

  
**Retourne**: Enregistreur