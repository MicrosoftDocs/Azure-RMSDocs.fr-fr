---
title: Test de votre application | Azure RMS
description: Instructions de configuration de votre application pour le test.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 8f99338daf79b2a59ddacb914d424da81d2b630b
ms.sourcegitcommit: 8e622a93ff8d07a180e3be6e8b14748354e640bd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2018
---
# <a name="testing-your-application"></a>Test de votre application

Ici, vous apprenez à préparer le test de l’application.

## <a name="instructions"></a>Instructions

Vous pouvez réaliser le test avec Azure RMS ou un serveur RMS en cours d’exécution sur Windows Server.  Commencez par tester avec Azure RMS et testez avec le serveur RMS (si cela est nécessaire pour votre déploiement).

- Pour réaliser le test avec Azure RMS, consultez [Procédure : Utilisation de l’authentification ADAL](how-to-use-adal-authentication.md).
- Pour réaliser le test avec un serveur RMS, consultez [Comment : installer et configurer un serveur RMS](how-to-install-and-configure-an-rms-server.md).
- Pour installer le runtime développeur :

   Le client Rights Management Services 2.1 doit être installé sur l’ordinateur sur lequel vous testez votre application.
   - Pour tester votre application sur un ordinateur autre que votre ordinateur de développement, installez le client RMS 2.1 sur cet ordinateur à partir de la [page de téléchargement du client AD RMS](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
   - Rights Management Services SDK 2.1 doit avoir déjà été installé sur votre ordinateur de développement.

   Pour obtenir de l’aide sur l’installation de RMS SDK 2.1, consultez [Installer le kit SDK](install-the-rms-sdk.md).

## <a name="remarks"></a>Remarques

Ce guide n’est pas exhaustif. Pour découvrir comment configurer le client RMS 2.1, consultez [Notes sur le déploiement du client RMS 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx).

## <a name="related-topics"></a>Rubriques connexes

* [Procédure : installation et configuration d’un serveur RMS](how-to-install-and-configure-an-rms-server.md)
* [Procédure : utilisation de l’authentification ADAL](how-to-use-adal-authentication.md)
* [Installer le SDK](install-the-rms-sdk.md)
* [Notes sur le déploiement du client RMS 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
