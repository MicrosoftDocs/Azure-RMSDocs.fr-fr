---
title: Guide du développeur RMS | Azure RMS
description: Trois générations du Kit Rights Management SDK sont désormais disponibles.
keywords: ''
author: bryanla
manager: mbaldwin
ms.author: bryanla
ms.date: 12/11/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 0510ead4-2fe7-4269-885b-fe16bcc69888
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c94965a6007ea93e657e719c6c9cd963cf54e66c
ms.sourcegitcommit: 1cd4edd4ba1eb5e10cb61628029213eda316783a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53266439"
---
# <a name="rms-developers-guide"></a>Guide du développeur RMS

## <a name="overview"></a>Vue d’ensemble ##
Trois générations du kit Rights Management SDK sont désormais disponibles : **Microsoft Rights Management 4.2 SDK** pour Android, iOS/OS X, appareils Windows et Linux, **Microsoft Rights Management SDK 2.1** pour le client Windows Desktop et le désormais obsolète kit **AD RMS SDK**.

## <a name="software-development-kits"></a>Kits de développement logiciel (SDK) ##
| SDK | Description |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Ensemble d’outils simplifié de nouvelle génération qui fournit une expérience de développement légère pour offrir à vos applications Android, iOS, Mac OS X, Windows Phone/RT et Linux/C++ une protection des informations par le biais des services Microsoft Rights Management. |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | SDK performant permettant aux développeurs d’applications de bureau Windows et aux fournisseurs de solutions de serveur d’intégrer la gestion des droits à leurs produits.|
|[AD RMS SDK](/azure/information-protection/develop/) |** REMARQUE ** AD RMS SDK exploitant les fonctionnalités exposées par le client dans Msdrm.dll peut être utilisé avec Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 et Windows Vista. Il sera peut-être modifié ou indisponible dans les versions ultérieures. Utilisez plutôt Microsoft Rights Management Services SDK 2.1 qui exploite les fonctionnalités exposées par le client dans Msipc.dll.|
|[API de script AD RMS](/azure/information-protection/develop/) | Permet de créer des scripts pour gérer une installation AD RMS.|

## <a name="code-samples-and-tools"></a>Exemples de code et outils ##
Cette collection d’exemples de code RMS fournis par Microsoft et d’outils de prise en charge pour les développeurs couvre tous les systèmes d’exploitation prise en charge (Android, iOS/OS X, Windows Phone et Windows Desktop). Elle est régulièrement mise à jour pour garantir la compatibilité avec son SDK pris en charge.

| Élément | Système d'exploitation | Version de SDK prise en charge | Description |
|------|------------------|------------------------|-------------|
| [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows Desktop | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) et versions ultérieures du SDK 2.x | **IpcManagedAPI** est une représentation .NET (C#) de RMS SDK 2.1 qui permet de simplifier la compatibilité RMS de votre application gérée.|
| [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) | Windows Desktop | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) et versions ultérieures du SDK 2.x| **IPCNotepad** est un exemple d’application compatible RMS qui décrit les étapes de base que chaque application compatible RMS doit effectuer lors de la protection et de la consommation de contenu limité.|
| [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms)|Windows Desktop|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) et versions ultérieures du SDK 2.x|**IpcDlp** est un exemple d’application de protection contre la perte de données (DLP) compatible RMS qui décrit les étapes de base que chaque application DLP compatible RMS doit effectuer à l’aide de l’API de fichier pour protéger et consommer du contenu limité.|
| [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows Desktop|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) et versions ultérieures du SDK 2.x|**IpcAzureApp** est un exemple qui montre comment utiliser RMS SDK dans une application Azure pour protéger les données dans le stockage d’objets blob Azure.|
| [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows Desktop|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) et versions ultérieures du SDK 2.x|**RmsDocumentInspector** est un outil qui peut fournir des informations sur n’importe quel fichier protégé par RMS, telles que l’ID de contenu ou les droits d’utilisateur.|
| [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows Desktop|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) et versions ultérieures du SDK 2.x|**RmsFileWatcher** est un exemple qui montre comment générer une application Windows qui surveille des répertoires du système de fichiers et applique des stratégies de protection RMS lors de chaque modification, par exemple en cas d’ajout ou de modification de fichier.|
| [Scénarios d’utilisation d'iOS/OS X](https://msdn.microsoft.com/library/dn758307(v=vs.85).aspx) |iOS / OS X|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) et versions ultérieures du SDK 4.x|**Objective C**  Exemples de code représentant des scénarios de développement importants pour vous familiariser avec le Kit RMS SDK. Ces exemples traitent entre autres de l’utilisation du format de fichier protégé Microsoft, des formats de fichiers protégés personnalisés et des contrôles d’interface utilisateur personnalisés.|
| [Bibliothèque d’interface utilisateur et exemple d’application](https://github.com/AzureAD/rms-sdk-ui-for-ios) |iOS|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) et versions ultérieures du SDK 4.x|**Les bibliothèques d’interface utilisateur et l’exemple d’application pour iOS** disponibles dans GitHub vous permettent d’être rapidement opérationnel et de réutiliser notre interface utilisateur standard dans vos applications.|
| [Bibliothèque d’interface utilisateur et exemple d’application](https://github.com/AzureAD/rms-sdk-ui-for-android) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) et versions ultérieures du SDK 4.x|**Les bibliothèques d’interface utilisateur et l’exemple d’application pour Android** disponibles dans GitHub vous permettent d’être rapidement opérationnel et de réutiliser notre interface utilisateur standard dans vos applications.|
| [Scénarios d’utilisation d'Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) et versions ultérieures du SDK 4.x|**Exemples de code Java** représentant des scénarios de développement importants pour vous familiariser avec le Kit RMS SDK. Ces exemples traitent entre autres de l’utilisation du format de fichier protégé Microsoft, des formats de fichiers protégés personnalisés et des contrôles d’interface utilisateur personnalisés.|