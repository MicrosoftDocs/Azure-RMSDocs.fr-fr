---
title: 'MIP :: MipContext, classe'
description: 'Documente la classe MIP :: mipcontext du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 20ce55ec371582ee16c70f311e0fc38ffc79d2fc
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070611"
---
# <a name="class-mipmipcontext"></a>MIP :: MipContext, classe 
MipContext représente l’état partagé par tous les profils, moteurs et gestionnaires.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public void ShutDown ()  |  Arrêtez MIP.
public bool IsFeatureEnabled (fonctionnalité FlightingFeature) const  |  Obtient une valeur indiquant si une fonctionnalité est activée ou non.
public const ApplicationInfo& GetApplicationInfo() const  |  Obtient la description de l’application.
public const std :: String & GetMipPath () const  |  Obtenir le chemin d’accès de fichier pour les journaux, les caches, etc.
public std :: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Obtient l’implémentation du journal.
public LoggerDelegate * GetRawLoggerDelegate ()  |  Obtient l’implémentation du journal.
public static MIP_API std :: shared_ptr&lt;MipContext&gt; cdecl Mip :: MipContext :: Create | Créez une instance MipContext à utiliser lors de l’initialisation des profils.
public static MIP_API std :: shared_ptr&lt;MipContext&gt; _ _ cdecl Mip :: MipContext :: CreateWithCustomFeatureSettings | Créez une nouvelle instance MipContext avec des paramètres de fonctionnalités personnalisés.

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

  
**Retourne**: Chemin d’accès du fichier (avec le répertoire feuille « MIP »)
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate fonction)
Obtient l’implémentation du journal.

  
**Retourne**: Enregistreur
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate fonction)
Obtient l’implémentation du journal.

**Retourne**: Enregistreur

### <a name="create-function"></a>créer une fonction
Créez une instance MipContext à utiliser lors de l’initialisation des profils.

**Retourne**: Instance MipContext.

### <a name="createwithcustomfeaturesettings-function"></a>CreateWithCustomFeatureSettings fonction)
Créez une nouvelle instance MipContext avec des paramètres de fonctionnalités personnalisés.

**Retourne**: Instance MipContext.

