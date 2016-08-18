---
title: "Fichiers d’environnement de développement | Azure RMS"
description: "Cette rubrique présente les fichiers d’environnement de développement et leurs emplacements d’installation relatifs sur votre ordinateur."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 6b5bc9612ac17a2d6905200383d9b8df4c504efe
ms.openlocfilehash: 3d6e7c2b40ba80988e93186fd68a12e6216b477d


---

# Fichiers d’environnement de développement

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
|Msipc_s.lib|\lib|Fournit le point d’entrée d’[<strong>IpcInitialize</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) pour les applications x86.|
|Msipc.lib|\lib\x64|Bibliothèque à laquelle se lier pour créer des applications x64 à l’aide de RMS SDK 2.1.|
|Msipc_s.lib|\lib\x64|Fournit le point d’entrée d’[<strong>IpcInitialize</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) pour les applications x64.|
|Genmanifest.exe|\tools|Génère un manifeste pour une utilisation pendant le développement d’une application prenant en charge RMS.|
 

 

 



<!--HONumber=Jul16_HO3-->


