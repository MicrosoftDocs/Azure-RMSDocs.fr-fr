---
title: 'MIP, struct :: TelemetryConfiguration'
description: Documentation des structures associées au kit de développement logiciel (MIP) Microsoft Information Protection.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 4e3e9be086bbcddea5398ccfbe549ffc2ca1aae6
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567525"
---
# <a name="struct-miptelemetryconfiguration"></a>MIP, struct :: TelemetryConfiguration 
Paramètres de télémétrie personnalisés (rarement utilisés)
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String hostNameOverride  |  Nom de l’instance de télémétrie de l’hôte. S’il n’est pas défini, MIP agit comme son propre hôte.
public std :: String libraryNameOverride  |  Nom de fichier de la bibliothèque de télémétrie (DLL) de remplacement.
public std :: shared_ptr\<HttpDelegate\> httpDelegateOverride  |  Si cette valeur est définie, la gestion HTTP sera gérée par cette instance
public std :: shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Si cette valeur est définie, la gestion des tâches asynchrones sera gérée par cette instance, taskDispatcherDelegateOverides ne doit pas être partagée, car elle peut contenir des objets de télémétrie et empêcher sa sortie tant que taskDispatcher n’est pas libéré.
public bool isNetworkDetectionEnabled  |  Si cette valeur est définie, le composant de télémétrie effectue un test ping de l’état du réseau sur le thread
public bool isLocalCachingEnabled  |  Si cette valeur est définie, le composant de télémétrie utilisera la mise en cache sur disque
public bool isTraceLoggingEnabled  |  Si cette valeur est définie, le composant de télémétrie écrit les journaux d’avertissements et d’erreurs sur le disque
public bool isTelemetryOptedOut  |  Si cette valeur est définie, seules les données de télémétrie des données de service nécessaires seront envoyées
public bool isFastShutdownEnabled  |  Si cette valeur est définie, aucun événement ne sera chargé lors de l’arrêt, les événements d’audit seront téléchargés immédiatement lors de la journalisation
public std :: Map\<std :: String, std :: String\> customSettings  |  Paramètres de télémétrie personnalisés >
  
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