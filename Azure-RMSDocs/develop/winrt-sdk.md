---
title: Configuration pour le Windows Store | Azure RMS
description: Les applications du Windows Store peuvent utiliser Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 18da97a07e7d65c69f88167cf440e864d3b29631
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257601"
---
# <a name="windows-store-setup"></a>Configuration pour le Windows Store

Les applications du Windows Store peuvent utiliser le Kit Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations à l’aide d’Azure Active Directory Rights Management (AAD RM).

Cette rubrique vous guide tout au long du processus de configuration de votre environnement pour créer vos propres applications.

-   [Prérequis](#prerequisites)
-   [Facultatif](#optional)
-   [Configuration de votre environnement de développement](#configuring-your-development-environment)
-   [Voir aussi](#see-also)

## <a name="prerequisites"></a>Prérequis


Vous devez disposer des logiciels suivants sur votre système de développement :

-   Système d’exploitation [Windows 8.1](https://windows.microsoft.com/windows-8/meet)
-   [SDK Windows pour Windows 8.1](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/) ou version ultérieure, ou Visual Studio 2012 Express (inclus dans le SDK Windows pour Windows 8.0/8.1)
-   Package RMS SDK 4.2 pour les applications du Windows Store. Pour plus d’informations, consultez [Prise en main](get-started.md).
-   Bibliothèque d’authentification : Nous vous recommandons d’utiliser la [bibliothèque Azure ADAL (Active Directory Authentication Library)](https://msdn.microsoft.com/library/jj573266.aspx), mais vous pouvez aussi recourir à d’autres bibliothèques d’authentification.

Lisez la rubrique [Nouveautés](release-notes.md) pour obtenir des informations sur les mises à jour des API, des informations sur les appareils et les environnements, les notes de publication et les questions les plus fréquentes (FAQ).

## <a name="optional"></a>Facultatif

Notre bibliothèque d’interface utilisateur fournit une interface utilisateur réutilisable pour les opérations de protection et de consommation pour les développeurs qui ne souhaitent pas créer leur propre interface utilisateur personnalisée ([Bibliothèque d’interface utilisateur pour les applications du Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore)). Nous fournissons également un exemple d’application du Windows Store ([Exemple d’application RMS pour le Windows Store](https://github.com/AzureADSamples/rms-samples-for-windowsstore)).

## <a name="configuring-your-development-environment"></a>Configuration de votre environnement de développement


-   Ouvrez Visual Studio.
-   Cliquez sur **Fichier**, sur **Nouveau**, puis sur **Projet**.
-   Dans la boîte de dialogue **Nouveau projet**, cliquez sur **Visual C\#**, sélectionnez **Application vide (Windows)**, puis cliquez sur **OK**.

    ![Créer un projet](../media/winrtsetup-newproj.png)

-   Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur votre projet, puis sélectionnez **Ajouter une référence** pour ouvrir la boîte de dialogue **Ajouter une référence**.

    ![Ajouter une référence](../media/winrtsetup-addref.png)

-   Dans la boîte de dialogue **Ajouter une référence**, cliquez sur **Parcourir**, puis sélectionnez le fichier *Microsoft.RightsManagement.dll* figurant dans le dossier dans lequel vous avez extrait le package du SDK.
-   **Applications gérées** : pour créer une application gérée, vous devez ajouter cette référence. Sélectionnez **Windows 8.1**-&gt;**Extensions**, puis cochez la case **Package Windows Visual C++ Runtime pour Windows**

    ![Ajouter des extensions](../media/winrtsetup-refmngr.png)

-   **Ajout de fonctionnalités** : votre application a besoin de la fonctionnalité « Internet (client et serveur) » pour utiliser le SDK. Pour ajouter cette fonctionnalité à votre application, ouvrez le fichier *Package.appxmanifest* dans le projet et accédez à l’onglet **Fonctionnalités** pour l’ajouter.

Vous êtes maintenant prêt à créer vos propres applications du Windows Store.

### <a name="see-also"></a>Voir aussi

[Prise en main](get-started.md)

[Nouveautés](release-notes.md)

[Terminologie et concepts du développement](core-concepts.md)

[Windows 8](https://windows.microsoft.com/windows-8/meet)

[Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/)

[Informations de référence sur l’API Windows](https://msdn.microsoft.com/library/dn891914.aspx)
