---
title: TelemetryConfiguration struct
description: Documente la structure TelemetryConfiguration
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a152f604feabe66e354b0c85abd2d7cfca64e7b5
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535805"
---
# <a name="struct-telemetryconfiguration"></a>TelemetryConfiguration struct 
Paramètres de télémétrie personnalisés (rarement utilisés)
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String hostNameOverride  |  Nom de l’instance de télémétrie de l’hôte. S’il n’est pas défini, MIP agit comme son propre hôte.
public std :: String libraryNameOverride  |  Nom de fichier de la bibliothèque de télémétrie (DLL) de remplacement.
public std :: shared_ptr \<HttpDelegate\> httpDelegateOverride  |  Si cette valeur est définie, la gestion HTTP sera gérée par cette instance
public std :: shared_ptr \<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Si cette valeur est définie, la gestion des tâches asynchrones sera gérée par cette instance, taskDispatcherDelegateOverides ne doit pas être partagée, car elle peut contenir des objets de télémétrie et empêcher sa sortie tant que taskDispatcher n’est pas libéré.
public bool isNetworkDetectionEnabled  |  Si cette valeur est définie, le composant de télémétrie effectue un test ping de l’état du réseau sur le thread
public bool isLocalCachingEnabled  |  Si cette valeur est définie, le composant de télémétrie utilisera la mise en cache sur disque
public bool isTraceLoggingEnabled  |  Si cette valeur est définie, le composant de télémétrie écrit les journaux d’avertissements et d’erreurs sur le disque
public bool isTelemetryOptedOut  |  Si cette valeur est définie, seules les données de télémétrie des données de service nécessaires seront envoyées
public bool isFastShutdownEnabled  |  Si cette valeur est définie, aucun événement ne sera chargé lors de l’arrêt, les événements d’audit seront téléchargés immédiatement lors de la journalisation
public std :: map \<std::string, std::string\> customSettings  |  Paramètres de télémétrie personnalisés >
public std :: map \<std::string, std::vector\<std::string\> \> maskedProperties  |  Événements/propriétés de télémétrie qui doivent être masqués
  
## <a name="members"></a>Membres
  
### <a name="hostnameoverride-struct-member"></a>hostNameOverride, membre de struct
Nom de l’instance de télémétrie de l’hôte. S’il n’est pas défini, MIP agit comme son propre hôte.
  
### <a name="librarynameoverride-struct-member"></a>libraryNameOverride, membre de struct
Nom de fichier de la bibliothèque de télémétrie (DLL) de remplacement.
  
### <a name="httpdelegate"></a>HttpDelegate
Si cette valeur est définie, la gestion HTTP sera gérée par cette instance
  
### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
Si cette valeur est définie, la gestion des tâches asynchrones sera gérée par cette instance, taskDispatcherDelegateOverides ne doit pas être partagée, car elle peut contenir des objets de télémétrie et empêcher sa sortie tant que taskDispatcher n’est pas libéré.
  
### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie effectue un test ping de l’état du réseau sur le thread
  
### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie utilisera la mise en cache sur disque
  
### <a name="istraceloggingenabled-struct-member"></a>isTraceLoggingEnabled, membre de struct
Si cette valeur est définie, le composant de télémétrie écrit les journaux d’avertissements et d’erreurs sur le disque
  
### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut, membre de struct
Si cette valeur est définie, seules les données de télémétrie des données de service nécessaires seront envoyées
  
### <a name="isfastshutdownenabled-struct-member"></a>isFastShutdownEnabled, membre de struct
Si cette valeur est définie, aucun événement ne sera chargé lors de l’arrêt, les événements d’audit seront téléchargés immédiatement lors de la journalisation
  
### <a name="customsettings-struct-member"></a>customSettings, membre de struct
Paramètres de télémétrie personnalisés >
  
### <a name="maskedproperties-struct-member"></a>maskedProperties, membre de struct
Événements/propriétés de télémétrie qui doivent être masqués