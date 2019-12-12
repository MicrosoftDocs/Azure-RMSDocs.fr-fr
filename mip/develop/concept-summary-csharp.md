---
title: Présentation du wrapper C# du kit SDK Microsoft information protection
description: Présentation rapide de la prise en main du wrapper .NET MIP SDK et des différences entre le wrapper .NET et C++ le kit de développement logiciel (SDK).
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 6b2f26a61cd491574fd9f4a1e74fbfab4752257a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "60175190"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Prise en main avec le wrapper Microsoft Information Protection .NET

Le wrapper .NET du kit de développement logiciel (SDK) Microsoft Information Protection permet aux développeurs d’intégrer l’expérience Microsoft Information Protection dans leurs propres applications et services. Les fonctionnalités de classification, d’étiquetage et de protection du kit de développement logiciel (SDK) permettent de s’assurer que les informations sont classées, étiquetées et protégées, quel que soit l’endroit où elles transitent. 

Le wrapper managé et toutes les dépendances peuvent être installés par le biais de NuGet dans Visual Studio.

## <a name="supported-platforms"></a>Plates-formes prises en charge

Le wrapper Microsoft Information Protection .NET est pris en charge sur les plateformes .NET suivantes :

* .NET Standard 2.0
* .NET 4,0

## <a name="installing-the-package"></a>Installation du package

À partir de la console du gestionnaire de package dans Visual Studio 2017, installez le package en exécutant :

`install-package Microsoft.InformationProtection.File`

Aucun package supplémentaire n’est requis. Toutes les bibliothèques tierces sont incluses et seront copiées dans le dossier de sortie de la Build.

## <a name="wrapper-details"></a>Détails du Wrapper

Le wrapper .NET est un wrapper managé généré par [SWIG](https://swig.org/) . Le wrapper utilise des C++ bibliothèques compilées à partir du kit de développement logiciel (SDK) Microsoft information protection. Ces dll sont les mêmes que celles incluses dans la C++ version du kit de développement logiciel (SDK).

## <a name="concept-overlap"></a>Chevauchement du concept

Il existe quelques différences fondamentales entre la C++ version du kit de développement logiciel (SDK) et le wrapper managé.

* Le wrapper .NET ne requiert pas l’utilisation d’observateurs pour les opérations asynchrones. Toutes les opérations asynchrones sont implémentées via le [modèle asynchrone basé sur des tâches](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap).
* Le wrapper .NET requiert les délégués qui font partie du C++ Kit de développement logiciel (SDK) : AuthDelegate et ConsentDelegate. Ces délégués sont implémentés via les interfaces `IAuthDelegate` et `IConsentDelegate`

## <a name="next-steps"></a>Étapes suivantes

Ensuite, passez en revue [démarrage rapide-initialisation du kit de développement logiciel C# (MIP) SDK de Microsoft information protection](quick-app-initialization-csharp.md) pour commencer à créer une application console de base avec un MIP.
