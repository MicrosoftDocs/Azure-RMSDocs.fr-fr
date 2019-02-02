---
title: Kit SDK Microsoft Information Protection C# vue d’ensemble du Wrapper
description: Une vue d’ensemble rapide sur la prise en main avec le wrapper .NET du SDK MIP et les différences entre le wrapper .NET et le Kit de développement logiciel C++.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: ec1d2083449f1cb4ffccb086f71a7085a9251604
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651977"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Mise en route avec le Wrapper de .NET Microsoft Information Protection

Le Wrapper de Microsoft Information Protection SDK .NET permet aux développeurs d’intégrer l’expérience de Microsoft Information Protection dans à leurs propres applications et services. Le Kit de développement logiciel classification, l’étiquetage et aide des fonctionnalités de protection pour vous assurer que les informations sont classées, étiquetés et protégés, quel que soit leur cheminement. 

Le wrapper managé et toutes les dépendances peuvent être installés via NuGet dans Visual Studio.

## <a name="supported-platforms"></a>Plateformes prises en charge

Le Wrapper .NET de Microsoft Information Protection est pris en charge sur les plateformes .NET suivantes :

* .NET Standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>Installation du Package

À partir de la Console du Gestionnaire de Package dans Visual Studio 2017, installez le package en exécutant :

`install-package Microsoft.InformationProtection.File`

Aucun des packages supplémentaires ne sont nécessaires. Toutes les bibliothèques tierces sont inclus et copie vers le dossier de sortie sur la build.

## <a name="wrapper-details"></a>Détails de wrapper

Le wrapper .NET est un [SWIG](https://swig.org/) wrapper managé généré. Le wrapper utilise les bibliothèques C++ compilées à partir de la SDK Microsoft Information Protection. Ces DLL sont ces mêmes DLL qui sont inclus dans la version C++ du SDK.

## <a name="concept-overlap"></a>Chevauchement de concept

Il existe quelques différences fondamentales entre la version C++ du Kit de développement et le wrapper managé.

* Le wrapper .NET ne nécessite pas l’utilisation de l’Observateur des opérations asynchrones. Toutes les opérations asynchrones sont implémentées via la [Task-based Asynchronous Pattern](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap).
* Le wrapper .NET requiert-il les délégués qui font partie du Kit de développement C++ : Authdelegate : et ConsentDelegate. Ces délégués sont implémentées via les interfaces `IAuthDelegate` et `IConsentDelegate`

## <a name="next-steps"></a>Étapes suivantes

Ensuite, passez en revue [Guide de démarrage rapide - initialisation pour Microsoft Information Protection (MIP) SDK C# ](quick-app-initialization-csharp.md) prise en main sur la création d’une application de console de base, prenant en charge MIP.
