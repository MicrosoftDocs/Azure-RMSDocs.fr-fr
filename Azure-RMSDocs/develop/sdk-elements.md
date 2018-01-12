---
title: "Fichiers d’environnement de développement | Azure RMS"
description: "Cette rubrique présente les fichiers d’environnement de développement et leurs emplacements d’installation relatifs sur votre ordinateur."
keywords: 
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: f79c0d60bf460c0f8cca68f6b0447303a383c686
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
---
# <a name="development-environment-files"></a>Fichiers d’environnement de développement

Cette rubrique présente les fichiers d’environnement de développement et leurs emplacements d’installation relatifs sur votre ordinateur.

Rights Management Services SDK 2.1 comprend les fichiers suivants, qui sont installés sur votre ordinateur à l’emplacement par défaut ou à l’emplacement que vous avez spécifié : %MsipcSDKDir%.

|Fichier|Chemin|Description|
|----|----|-----------|
|ReadMe.htm| \ | Contient un lien vers l’aide de RMS et les [notes de publication](release-notes-rtm.md).|
|Isvtier5appsigningprivkey.dat|\bin|Contient la clé privée utilisée pour générer un manifeste pour une utilisation pendant le développement d’une application prenant en charge RMS.|
|Isvtier5appsigningpubkey.dat|\bin|Contient la clé publique utilisée pour générer un manifeste pour une utilisation pendant le développement d’une application prenant en charge RMS.|
|Isvtier5appsignsdk_client.xml|\bin|Utilisé pour générer un manifeste pour une utilisation pendant le développement d’une application prenant en charge RMS.|
|NomApp.isv.mcf|\bin|Fichier de configuration de manifeste réutilisable que vous pouvez utiliser pour générer un manifeste pendant le développement d’une application prenant en charge RMS.|
|Ipcsecproc_isv.dll|\bin\x86|DLL utilisée en interne, pour les applications x86, par Active Directory Rights Management Services Client 2.1 quand la hiérarchie des éditeurs de logiciels est employée.|
|Ipcsecproc_ssp_isv.dll|\bin\x86|DLL utilisée en interne, pour les applications x86, par AD RMS 2.1 quand la hiérarchie des éditeurs de logiciels est employée.|
|Ipcsecproc_isv.dll|\bin\x64|DLL utilisée en interne, pour les applications x64, par AD RMS Client 2.1 quand la hiérarchie des éditeurs de logiciels est employée.|
|Ipcsecproc_ssp_isv.dll|\bin\x64|DLL utilisée en interne, pour les applications x64, par AD RMS Client 2.1 quand la hiérarchie des éditeurs de logiciels est employée.|
|Msipc.h|\inc|Principal fichier include de RMS SDK 2.1.|
|Ipcprot.h|\inc|Contient l’interface publique exportée par RMS SDK 2.1.|
|Ipcbase.h|\inc|Contient les types de base et les fonctions d’assistance exportées par RMS SDK 2.1.|
|Ipcerror.h|\inc|Contient les codes d’erreur publics exportés par RMS SDK 2.1.|
|Ipcfile.h|\inc|Contient les interfaces de l’API de fichier exportées par RMS SDK 2.1.|
|Msipc.lib|\lib|Bibliothèque à laquelle se lier pour créer des applications x86 à l’aide de RMS SDK 2.1.|
|Msipc_s.lib|\lib|Fournit le point d’entrée d’[IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) pour les applications x86.|
|Msipc.lib|\lib\x64|Bibliothèque à laquelle se lier pour créer des applications x64 à l’aide de RMS SDK 2.1.|
|Msipc_s.lib|\lib\x64|Fournit le point d’entrée d’[IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) pour les applications x64.|
|Genmanifest.exe|\tools|Génère un manifeste pour une utilisation pendant le développement d’une application prenant en charge RMS.|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]