---
title: Configuration pour Windows Phone | Azure RMS
description: Les applications Windows Phone peuvent utiliser Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 8c36466511749b6148f58c439702c8cd0f252a64
ms.sourcegitcommit: 5390bd1e0e4851b81a59094e80202f0761b7810f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80068507"
---
# <a name="windows-phone-setup"></a>Configuration pour Windows Phone

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Les applications Windows Phone peuvent utiliser Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations à l’aide d’Azure Active Directory Rights Management (AAD RM).

Cette rubrique explique comment configurer votre environnement pour créer vos propres applications.

-   [Conditions préalables](#prerequisites)
-   [Configuration de votre environnement de développement](#configuring-your-development-environment)
-   [Voir aussi](#see-also)

## <a name="prerequisites"></a>Composants requis


Vous devez disposer des logiciels suivants sur votre système de développement :

-   Système d’exploitation [Windows 8.1](https://windows.microsoft.com/windows-8/meet)
-   [Outils de développement Windows Phone 8.1 (SDK)](https://developer.microsoft.com/windows/downloads/sdk-archive)
-   Microsoft [Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/) ou version ultérieure, ou Visual Studio 2012 Express (inclus dans le SDK Windows Phone 8.0/8.1)
-   Package MS RMS SDK 4.2 pour Windows Phone. Pour plus d’informations, consultez [Prise en main](get-started.md).
-   Bibliothèque d’authentification : Nous vous recommandons d’utiliser la [bibliothèque Azure ADAL (Active Directory Authentication Library)](https://msdn.microsoft.com/library/jj573266.aspx), mais vous pouvez aussi recourir à d’autres bibliothèques d’authentification.

Lisez la rubrique [Nouveautés](release-notes.md) pour obtenir des informations sur les mises à jour des API, des informations sur les appareils et les environnements, les notes de publication et les questions les plus fréquentes (FAQ).

Passez en revue les informations contenues dans le guide de [développement Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx) dans le Centre de développement Windows Phone.

## <a name="configuring-your-development-environment"></a>Configuration de votre environnement de développement


-   Ouvrez *Visual Studio*.
-   Cliquez sur **Fichier**. Dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.
-   Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Visual C\#** , **Application vide (Windows Phone)** , puis cliquez sur **OK**.

    ![Créer un projet](../media/wpsetup-newproj.png)

-   Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis sélectionnez **Ajouter une référence** pour ouvrir la boîte de dialogue **Ajouter une référence**.

    ![Ajouter une référence](../media/wpsetup-addref.png)

-   Cliquez sur **Parcourir** dans l’angle inférieur gauche de la boîte de dialogue **Ajouter une référence**, puis sélectionnez le fichier *Microsoft.RightsManagment.dll* figurant dans le dossier dans lequel vous avez extrait le package.
-   **Applications gérées** : pour créer une application gérée, vous devez ajouter cette référence. Sélectionnez **Windows 8.1**-&gt;**Extensions**, puis cochez la case **Package Windows Visual C++ Runtime pour Windows**

    ![Ajouter des extensions](../media/wpsetup-refmngr.png)

-   **Ajout de fonctionnalités** : votre application a besoin de la fonctionnalité « Internet (client et serveur) » pour utiliser le SDK. Pour ajouter cette fonctionnalité à votre application, ouvrez le fichier *Package.appxmanifest* dans le projet et accédez à l’onglet **Fonctionnalités** pour l’ajouter.

Vous êtes maintenant prêt à créer vos propres applications Windows Phone.

### <a name="see-also"></a>Voir aussi

[Mise en route](get-started.md)

[Nouveautés](release-notes.md)

[Concepts de base](core-concepts.md)

[Développement Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx)

[Informations de référence sur l’API Windows](https://msdn.microsoft.com/library/dn891914.aspx)

[Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/)

[SDK Windows Phone](https://developer.microsoft.com/windows/downloads/sdk-archive)
