---
title: Test de votre application | Azure RMS
description: Instructions de configuration de votre application pour le test.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 9cc96c7f4d75969ec75b1372a4a49499709b0d32


---

# Test de votre application

Cette rubrique contient des instructions sur la configuration de test de votre application.

## Instructions

### Étape 1 : Configuration pour le test

Vous pouvez réaliser le test avec Azure RMS ou un serveur RMS en cours d’exécution sur Windows Server. Nous vous suggérons de commencer votre test sur Azure RMS, puis, si votre déploiement l’exige, de procéder au test avec le serveur RMS.

1. Pour réaliser le test avec Azure RMS, consultez [Procédure : Utilisation de l’authentification ADAL](how-to-use-adal-authentication.md).
2. Pour réaliser le test avec un serveur RMS, consultez [Comment : installer et configurer un serveur RMS](how-to-install-and-configure-an-rms-server.md).
3. Voici comment installer le runtime développeur.

   Le client Rights Management Services 2.1 doit être installé sur l’ordinateur sur lequel vous testez votre application.
   - Si vous testez votre application sur un ordinateur autre que votre ordinateur de développement, vous pouvez installer le client RMS 2.1 sur cet ordinateur à partir de la [page de téléchargement du client AD RMS](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
   - Si vous testez votre application sur votre ordinateur de développement, vous devez déjà avoir installé Rights Management Services SDK 2.1. Le client RMS 2.1 est installé sans assistance à ce stade.

    Pour plus d’informations sur la façon d’installer Rights Management Services SDK 2.1, consultez [Installer le SDK](install-the-rms-sdk.md).

## Remarques

Les instructions de cette rubrique ne sont pas exhaustives. Pour plus d’informations sur la configuration du client RMS 2.1, consultez les [notes sur le déploiement du client RMS 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx).

### Rubriques connexes

* [Comment : installer et configurer un serveur RMS](how-to-install-and-configure-an-rms-server.md)
* [Comment : utiliser l’authentification ADAL](how-to-use-adal-authentication.md)
* [Installer le SDK](install-the-rms-sdk.md)
* [Notes sur le déploiement du client RMS 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 



<!--HONumber=Aug16_HO4-->


