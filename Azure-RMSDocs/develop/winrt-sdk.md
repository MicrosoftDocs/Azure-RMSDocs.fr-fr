---
title: Configuration pour le Windows Store | Azure RMS
description: Les applications du Windows Store peuvent utiliser Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 0382a1a97d65938c5d90d10d4e572697558223cc
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568356"
---
# <a name="windows-store-setup"></a>Configuration pour le Windows Store

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Les applications du Windows Store peuvent utiliser le Kit Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations à l’aide d’Azure Active Directory Rights Management (AAD RM).

Cette rubrique vous guide tout au long du processus de configuration de votre environnement pour créer vos propres applications.

-   [Composants requis](#prerequisites)
-   [Facultatif](#optional)
-   [Configuration de votre environnement de développement](#configuring-your-development-environment)
-   [Voir aussi](#see-also)

## <a name="prerequisites"></a>Prérequis


Vous devez disposer des logiciels suivants sur votre système de développement :

-   Système d’exploitation [Windows 8.1](https://windows.microsoft.com/windows-8/meet)
-   [SDK Windows pour Windows 8.1](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/) ou version ultérieure, ou Visual Studio 2012 Express (inclus dans le SDK Windows pour Windows 8.0/8.1)
-   Package RMS SDK 4.2 pour les applications du Windows Store. Pour plus d’informations, consultez [prise en main](get-started.md).
-   Bibliothèque d’authentification : Nous vous recommandons d’utiliser la [bibliothèque Azure ADAL (Active Directory Authentication Library)](/previous-versions/azure/jj573266(v=azure.100)), mais vous pouvez aussi recourir à d’autres bibliothèques d’authentification.

Lisez la rubrique [Nouveautés](release-notes.md) pour obtenir des informations sur les mises à jour des API, des informations sur les appareils et les environnements, les notes de publication et les questions les plus fréquentes (FAQ).

## <a name="optional"></a>Facultatif

Notre bibliothèque d’interface utilisateur fournit une interface utilisateur réutilisable pour les opérations de protection et de consommation pour les développeurs qui ne souhaitent pas créer leur propre interface utilisateur personnalisée ([Bibliothèque d’interface utilisateur pour les applications du Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore)). Nous fournissons également un exemple d’application du Windows Store ([Exemple d’application RMS pour le Windows Store](https://github.com/AzureADSamples/rms-samples-for-windowsstore)).

## <a name="configuring-your-development-environment"></a>Configuration de votre environnement de développement


-   Ouvrez Visual Studio.
-   Cliquez sur **Fichier**, sur **Nouveau**, puis sur **Projet**.
-   Dans la boîte de dialogue **nouveau projet** , cliquez sur **Visual C \#** et sélectionnez **application vide (Windows)** , puis cliquez sur **OK**.

    ![Création d’un projet](../media/winrtsetup-newproj.png)

-   Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur votre projet, puis sélectionnez **Ajouter une référence** pour ouvrir la boîte de dialogue **Ajouter une référence**.

    ![Ajouter la référence](../media/winrtsetup-addref.png)

-   Dans la boîte de dialogue **Ajouter une référence**, cliquez sur **Parcourir**, puis sélectionnez le fichier *Microsoft.RightsManagement.dll* figurant dans le dossier dans lequel vous avez extrait le package du SDK.
-   **Applications gérées** : pour créer une application gérée, vous devez ajouter cette référence. Sélectionnez **Windows 8.1** - &gt; **Extensions** et cochez la case **package Windows Visual C++ Runtime pour Windows**

    ![Ajouter des extensions](../media/winrtsetup-refmngr.png)

-   **Ajout de fonctionnalités** : votre application a besoin de la fonctionnalité « Internet (client et serveur) » pour utiliser le SDK. Pour ajouter cette fonctionnalité à votre application, ouvrez le fichier *Package.appxmanifest* dans le projet et accédez à l’onglet **Fonctionnalités** pour l’ajouter.

Vous êtes maintenant prêt à créer vos propres applications du Windows Store.

### <a name="see-also"></a>Voir aussi

[Prise en main](get-started.md)

[Nouveautés](release-notes.md)

[Concepts et termes de développement](core-concepts.md)

[Windows 8](https://windows.microsoft.com/windows-8/meet)

[Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/)

[Référence de l’API Windows](/previous-versions/windows/desktop/msipcthin2/winrt)