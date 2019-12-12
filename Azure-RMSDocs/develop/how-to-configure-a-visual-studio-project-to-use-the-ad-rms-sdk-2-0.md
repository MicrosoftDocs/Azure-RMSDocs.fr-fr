---
title: Configurer Visual Studio| Azure RMS
description: Instructions sur la configuration d’un projet Visual Studio en vue d’utiliser le SDK RMS 2.1.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: d36938daf4dbcbe86331ec6852dfe4ecb04a2959
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "68792403"
---
# <a name="configure-visual-studio"></a>Configurer Visual Studio

Cette rubrique contient des instructions sur la configuration d’un projet Visual Studio en vue d’utiliser le SDK Rights Management Services 2.1.

## <a name="prerequisites"></a>Conditions préalables

-   [Installer le SDK](install-the-rms-sdk.md)

**Instructions**

### <a name="step-1-configure-a-visual-studio-project-to-use-rmssdk21"></a>Étape 1 : configurer un projet Visual Studio pour utiliser kit de développement logiciel (SDK) RMS 2,1

Ces instructions sont spécifiques à Microsoft Visual Studio 2010. Si vous utilisez une autre version de Microsoft Visual Studio, vos boîtes de dialogue de paramètres peuvent être légèrement différentes.

Ces instructions concernent la création d’une application 32 bits native.

1.  Ajoutez le répertoire Include du SDK RMS 2.1 à votre projet Visual Studio 2010.

    Sous **Propriétés de configuration**, sélectionnez **Répertoires VC++** , puis ajoutez le répertoire Include du SDK RMS 2.1 ( **$(MSIPCSDKDIR)\\inc**) au champ **Répertoires Include**.

    ![Propriétés de configuration - Champ Répertoires Include](../media/include_directories.png)

2.  Ajoutez le répertoire des bibliothèques du SDK RMS 2.1 à votre projet Visual Studio 2010.

    Sous **Propriétés de configuration**, sélectionnez **Répertoires VC++** , puis ajoutez le répertoire des bibliothèques du SDK RMS 2.1 au champ **Répertoires de bibliothèques** de votre plateforme.

    -   Pour Win32, utilisez **$(MSIPCSDKDIR)\\lib**
    -   Pour x64, utilisez **$(MSIPCSDKDIR)\\lib\\x64**

    ![Propriétés de configuration - Champ Répertoires de bibliothèques](../media/library_directories.png)

3.  Ajoutez les fichiers de bibliothèque du SDK RMS 2.1 comme dépendances Visual Studio 2010.

    Sous **Éditeur de liens**, sélectionnez **Entrée**, puis ajoutez les fichiers de bibliothèque du SDK RMS 2.1 (**Msipc.lib** et **Msipc\_s.lib**) au champ **Dépendances supplémentaires**.

    ![Éditeur de liens - Fichiers de bibliothèque - Champ Dépendances](../media/additional_dependencies.png)

4.  Ajoutez la DLL du SDK RMS 2.1 comme DLL chargée en différé.

    Sous **Éditeur de liens**, sélectionnez **Entrée**, puis ajoutez le fichier DLL du SDK RMS 2.1 (**Msipc.dll**) au champ **Chargement différé des DLL**.

    ![Éditeur de liens - Champ Chargement différé des DLL](../media/delay_loaded.png)

5.  Créez des informations de version pour le fichier binaire créé.

    Sous **Explorateur de solutions**, sélectionnez **Fichiers de ressources**, puis ajoutez le nom du fichier binaire dans le champ **OriginalFileName**.

    ![Explorateur de solutions - Champ Fichiers de ressources](../media/original_file_name.png)

## <a name="related-topics"></a>Rubriques connexes

* [Installer le SDK](install-the-rms-sdk.md)
