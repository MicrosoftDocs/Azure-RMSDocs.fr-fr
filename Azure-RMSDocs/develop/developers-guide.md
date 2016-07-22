---
title: "Guide du développeur | Azure RMS"
description: "Vue d’ensemble de l’utilisation des outils de développement ; SDK, bibliothèques supplémentaires et exemples de code."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: c9d5ec961989283c5201a81f862b2da45ed64340


---

# Guide du développeur

## Vue d'ensemble ##
Ce guide décrit notre suite de kits SDK Rights Management et un ensemble croissant d’outils et d’exemples de code qui couvrent toutes les plateformes prises en charge. 

## Kits de développement logiciel (SDK) ##
Trois générations de SDK RMS sont disponibles. Elles sont décrites dans le tableau suivant.

| SDK | Description |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Ensemble d’outils simplifié de nouvelle génération qui fournit une expérience de développement légère pour offrir à vos applications Android, iOS, Mac OS X, Windows Phone/RT et Linux/C++ une protection des informations par le biais des services Microsoft Rights Management. |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | SDK performant permettant aux développeurs d’applications de bureau Windows et aux fournisseurs de solutions de serveur d’intégrer la gestion des droits à leurs produits.|
|[AD RMS SDK](https://msdn.microsoft.com/library/cc530379(v=vs.85).aspx)|** REMARQUE ** : AD RMS SDK exploitant les fonctionnalités exposées par le client dans Msdrm.dll peut être utilisé avec Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 et Windows Vista. Il sera peut-être modifié ou indisponible dans les versions ultérieures. Utilisez plutôt Microsoft Rights Management Services SDK 2.1 qui exploite les fonctionnalités exposées par le client dans Msipc.dll.|
|[API de script AD RMS](https://msdn.microsoft.com/en-us/library/bb968797(v=vs.85).aspx)| Permet de créer des scripts pour gérer une installation AD RMS.|

## Exemples de code et outils
Cette collection d’exemples de code RMS fournis par Microsoft et d’outils de prise en charge pour les développeurs couvre tous les systèmes d’exploitation pris en charge (Android, iOS/OS X, Windows Phone et Windows Desktop). Elle est régulièrement mise à jour pour garantir la compatibilité avec son SDK pris en charge.

### Android

Les éléments suivants sont exécutés sur Android et pris en charge par [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) et versions ultérieures du SDK 4.x

- [La bibliothèque d’interface utilisateur et l’exemple d’application](https://github.com/AzureAD/rms-sdk-ui-for-android) disponibles dans GitHub vous permettent d’être rapidement opérationnel et de réutiliser notre interface utilisateur standard dans vos applications.
- [Les scénarios d’utilisation Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) dans Java représentent des scénarios de développement importants pour vous familiariser avec RMS SDK. Ces exemples traitent entre autres de l’utilisation du format de fichier protégé Microsoft, des formats de fichiers protégés personnalisés et des contrôles d’interface utilisateur personnalisés.

### iOS / OS X

Les éléments suivants sont exécutés sur iOS / OS X et pris en charge par [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) et versions ultérieures du SDK 4.x

- [Les scénarios d’utilisation iOS/OS X](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx) dans Objective C représentent des scénarios de développement importants pour vous familiariser avec RMS SDK. Ces exemples traitent entre autres de l’utilisation du format de fichier protégé Microsoft, des formats de fichiers protégés personnalisés et des contrôles d’interface utilisateur personnalisés.
- [La bibliothèque d’interface utilisateur et l’exemple d’application](https://github.com/AzureAD/rms-sdk-ui-for-ios) disponibles dans GitHub vous permettent d’être rapidement opérationnel et de réutiliser notre interface utilisateur standard dans vos applications. Prise en charge sur **iOS uniquement**.

### Windows Desktop

Les éléments suivants sont exécutés sur Windows Desktop et pris en charge par [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) et versions ultérieures du SDK 2.x

- [Read PFILE protected PDF](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) est un exemple de code simple disponible sur notre blog RMS Developer’s Corner. Il utilise l’API de fichier MSIPC pour déchiffrer et ouvrir un document PDF protégé par PFILE.
- [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) est une représentation .NET (C#) de RMS SDK 2.1 qui permet de simplifier la compatibilité RMS de votre application gérée.
- [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) est un exemple d’application compatible RMS qui décrit les étapes de base que chaque application compatible RMS doit effectuer lors de la protection et de la consommation de contenu limité.
- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un exemple d’application de protection contre la perte de données (DLP) compatible RMS qui décrit les étapes de base que chaque application DLP compatible RMS doit effectuer à l’aide de l’API de fichier pour protéger et consommer du contenu limité.
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un exemple qui montre comment utiliser RMS SDK dans une application Azure pour protéger les données dans le stockage d’objets blob Azure.
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un outil qui peut fournir des informations sur n’importe quel fichier protégé par RMS, telles que l’ID de contenu ou les droits d’utilisateur.
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un exemple qui montre comment générer une application Windows qui surveille des répertoires du système de fichiers et applique des stratégies de protection RMS lors de chaque modification, par exemple en cas d’ajout ou de modification de fichier.

### Windows Store et Windows Phone

- [Bibliothèque d’interface utilisateur pour Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore) - Bibliothèque d’interface utilisateur pour Microsoft RMS SDK v4.1 pour les applications du Windows Store. Cette bibliothèque est facultative et un développeur peut choisir de créer sa propre interface utilisateur lors de l’utilisation de Microsoft RMS SDK v4.1

- [Bibliothèque d’interface utilisateur pour Windows Phone](https://github.com/AzureAD/rms-sdk-ui-for-winphone) - Bibliothèque d’interface utilisateur pour Microsoft RMS SDK v4.1 pour les applications Windows Phone. Cette bibliothèque est facultative et un développeur peut choisir de créer sa propre interface utilisateur lors de l’utilisation de Microsoft RMS SDK v4.1

- [Exemple d’application](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore) - L’exemple pour Microsoft RMS SDK v4.1 pour les applications du Windows Store représente un exemple de consommation de document de base pour la plateforme.



<!--HONumber=Jun16_HO4-->


