---
title: Test de votre application | Azure RMS
description: Apprenez à préparer le test des applications avec Azure RMS ou un serveur RMS s’exécutant sur Windows Server.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: c4c6ac4e2f8463e7d17f8ebd609a1276edbce1f7
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568194"
---
# <a name="testing-your-application"></a>Tester votre application

Ici, vous apprenez à préparer le test de l’application.

## <a name="instructions"></a>Instructions

Vous pouvez réaliser le test avec Azure RMS ou un serveur RMS en cours d’exécution sur Windows Server.  Commencez par tester avec Azure RMS et testez avec le serveur RMS (si cela est nécessaire pour votre déploiement).

- Pour réaliser le test avec Azure RMS, consultez [Procédure : Utilisation de l’authentification ADAL](how-to-use-adal-authentication.md).
- Pour réaliser le test avec un serveur RMS, consultez [Comment : installer et configurer un serveur RMS](how-to-install-and-configure-an-rms-server.md).
- Pour installer le runtime développeur :

   Le client Rights Management Services 2.1 doit être installé sur l’ordinateur sur lequel vous testez votre application.
  - Pour tester votre application sur un ordinateur autre que votre ordinateur de développement, installez le client RMS 2.1 sur cet ordinateur à partir de la [page de téléchargement du client AD RMS](https://www.microsoft.com/download/details.aspx?id=38396).
  - Rights Management Services SDK 2.1 doit avoir déjà été installé sur votre ordinateur de développement.

    Pour obtenir de l’aide sur l’installation de RMS SDK 2.1, consultez [Installer le kit SDK](install-the-rms-sdk.md).

## <a name="remarks"></a>Remarques

Ce guide n’est pas exhaustif. Pour découvrir comment configurer le client RMS 2.1, consultez [Notes sur le déploiement du client RMS 2.1](../rms-client/client-deployment-notes.md).

## <a name="related-topics"></a>Rubriques connexes

* [Procédure : installation et configuration d’un serveur RMS](how-to-install-and-configure-an-rms-server.md)
* [Comment : utiliser l’authentification ADAL](how-to-use-adal-authentication.md)
* [Installer le SDK](install-the-rms-sdk.md)
* [Notes sur le déploiement du client RMS 2.1](../rms-client/client-deployment-notes.md)