---
# required metadata

title: Fichiers d’environnement de développement | Azure RMS
description: Cette rubrique présente les fichiers d’environnement de développement et leurs emplacements d’installation relatifs sur votre ordinateur.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3760d242-2f8c-4312-aaa5-8d592fd28748

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
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
 

 

 


<!--HONumber=Apr16_HO3-->

