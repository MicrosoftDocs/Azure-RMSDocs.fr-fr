---
title: 'Procédure : Débogage d’une application avec gestion des droits | Azure RMS'
description: La rubrique suivante indique comment déboguer une application et utiliser le journal des événements Windows.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 58791e2ac3070a8cde1ee9307544d9bc35ab2f40
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178878"
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

**Remarque**  Le journal est activé par défaut et la valeur 3 est définie pour le niveau de commentaires.

 

Pour modifier les paramètres de la fonctionnalité de journalisation, vous pouvez utiliser l’interface utilisateur pour l’Observateur d’événements Windows ou Wevtutil, un outil de ligne de commande intégré à Windows.

Via l’interface Wevtutil, vous pouvez contrôler le niveau de commentaires de votre journal.

À ce stade, nous prenons en charge 3 niveaux de journalisation :

-   Niveau 2 : erreur
-   Niveau 3 : avertissement
-   Niveau 4 : informations

Par exemple, la commande suivante active le journal des événements MSIPC et affecte la valeur informations au niveau de commentaires.

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

**Remarque**  Dans l’Observateur d’événements Windows, dans le menu **Affichage**, sélectionnez **Afficher les journaux d’analyse et de débogage** pour afficher le journal de débogage MSIPC.
