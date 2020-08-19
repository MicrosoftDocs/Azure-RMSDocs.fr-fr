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
ms.openlocfilehash: 638a8ec54a850a051795c00b2b1aef4ef47866ff
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564067"
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

## <a name="remarks"></a>Notes

Ce guide n’est pas exhaustif. Pour découvrir comment configurer le client RMS 2.1, consultez [Notes sur le déploiement du client RMS 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx).

## <a name="related-topics"></a>Rubriques connexes

* [Procédure : installation et configuration d’un serveur RMS](how-to-install-and-configure-an-rms-server.md)
* [Comment : utiliser l’authentification ADAL](how-to-use-adal-authentication.md)
* [Installer le Kit de développement logiciel (SDK)](install-the-rms-sdk.md)
* [Notes sur le déploiement du client RMS 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx)
