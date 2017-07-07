---
title: "Procédure : Débogage d’une application avec gestion des droits | Azure RMS"
description: "La rubrique suivante indique comment déboguer une application et utiliser le journal des événements Windows."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 0995a18f77f40bf345be3e69860032fdb63a9b38
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-debug-a-rights-enabled-application"></a>Comment : déboguer une application avec gestion des droits

La rubrique suivante indique comment déboguer une application et utiliser le journal des événements Windows.

## <a name="debugging-your-application"></a>Débogage de votre application

Dans Rights Management Services SDK 2.1, les vérifications anti-débogage dans la version développeur de notre runtime sont désactivées.

Vous pouvez activer le suivi du débogage à l’aide de la clé de Registre suivante. (Pour désactiver le suivi du débogage, remplacez la valeur par 0.) Rien d’autre n’est nécessaire pour le débogage dans cette version.


```
HKEY_LOCAL_MACHINE
   SOFTWARE
      Microsoft
         MSIPC
            "Trace" = 00000001
            Data type
            dword
```

### <a name="application-logging-by-using-the-windows-event-log"></a>Journalisation des applications à l’aide du journal des événements Windows

Le nom du journal des événements est Microsoft-RMS-MSIPC/Debug. Cela signifie que votre journal apparaît dans l’Observateur d’événements Windows sous la forme « Journaux des applications et des services\\Microsoft\\RMS\\MSIPC\\Debug ».

**Remarque** Le journal est activé par défaut et la valeur 3 est définie pour le niveau de commentaires.

 

Pour modifier les paramètres de la fonctionnalité de journalisation, vous pouvez utiliser l’interface utilisateur pour l’Observateur d’événements Windows ou Wevtutil, un outil de ligne de commande intégré à Windows.

Via l’interface Wevtutil, vous pouvez contrôler le niveau de commentaires de votre journal.

À ce stade, nous prenons en charge 3 niveaux de journalisation :

-   Niveau 2 : erreur
-   Niveau 3 : avertissement
-   Niveau 4 : informations

Par exemple, la commande suivante active le journal des événements MSIPC et affecte la valeur informations au niveau de commentaires.

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

**Remarque** Dans l’Observateur d’événements Windows, dans le menu **Affichage**, sélectionnez **Afficher les journaux d’analyse et de débogage** pour afficher le journal de débogage MSIPC.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]