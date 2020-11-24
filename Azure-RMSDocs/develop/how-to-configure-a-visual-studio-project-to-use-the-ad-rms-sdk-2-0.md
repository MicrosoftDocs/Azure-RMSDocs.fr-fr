---
title: Configurer Visual Studio| Azure RMS
description: Instructions sur la configuration d’un projet Visual Studio en vue d’utiliser le SDK RMS 2.1.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 9fd65730baf1fefad6dd4e39341dab1260b51dd0
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2020
ms.locfileid: "95567468"
---
# <a name="configure-visual-studio"></a>Configurer Visual Studio

Cette rubrique contient des instructions sur la configuration d’un projet Visual Studio en vue d’utiliser le SDK Rights Management Services 2.1.

## <a name="prerequisites"></a>Prérequis

-   [Installer le SDK](install-the-rms-sdk.md)

**Instructions**

### <a name="step-1-configure-a-visual-studio-project-to-use-rmssdk21"></a>Étape 1 : Configurer un projet Visual Studio pour utiliser RMS SDK 2.1

Ces instructions sont spécifiques à Microsoft Visual Studio 2010. Si vous utilisez une autre version de Microsoft Visual Studio, vos boîtes de dialogue de paramètres peuvent être légèrement différentes.

Ces instructions concernent la création d’une application 32 bits native.

1.  Ajoutez le répertoire Include du SDK RMS 2.1 à votre projet Visual Studio 2010.

    Sous **Propriétés de configuration** , sélectionnez **Répertoires VC + +** , puis ajoutez le répertoire include Kit de développement logiciel (SDK) RMS 2,1, **$ (MSIPCSDKDIR) \\ Inc**, au champ **répertoires Include** .

    ![Propriétés de configuration - Champ Répertoires Include](../media/include_directories.png)

2.  Ajoutez le répertoire des bibliothèques du SDK RMS 2.1 à votre projet Visual Studio 2010.

    Sous **Propriétés de configuration**, sélectionnez **Répertoires VC++**, puis ajoutez le répertoire des bibliothèques de RMS SDK 2.1 au champ **Répertoires de bibliothèques** de votre plateforme.

    -   Pour Win32, utilisez **$ (MSIPCSDKDIR) \\ lib**
    -   Pour x64, utilisez **$ (MSIPCSDKDIR) \\ lib \\ x64**

    ![Propriétés de configuration - Champ Répertoires de bibliothèques](../media/library_directories.png)

3.  Ajoutez les fichiers de bibliothèque du SDK RMS 2.1 comme dépendances Visual Studio 2010.

    Sous **éditeur de liens**, sélectionnez **entrée** , puis ajoutez le kit de développement logiciel (SDK) RMS fichiers de bibliothèque 2,1 ; **MSIPC. lib** et **MSIPC \_ s. lib**, dans le champ **dépendances supplémentaires** .

    ![Éditeur de liens - Fichiers de bibliothèque - Champ Dépendances](../media/additional_dependencies.png)

4.  Ajoutez la DLL du SDK RMS 2.1 comme DLL chargée en différé.

    Sous **Éditeur de liens**, sélectionnez **Entrée**, puis ajoutez le fichier DLL de RMS SDK 2.1 (**Msipc.dll**) au champ **Chargement différé des DLL**.

    ![Éditeur de liens - Champ Chargement différé des DLL](../media/delay_loaded.png)

5.  Créez des informations de version pour le fichier binaire créé.

    Sous **Explorateur de solutions**, sélectionnez **Fichiers de ressources**, puis ajoutez le nom du fichier binaire dans le champ **OriginalFileName**.

    ![Explorateur de solutions - Champ Fichiers de ressources](../media/original_file_name.png)

## <a name="related-topics"></a>Rubriques connexes

* [Installer le SDK](install-the-rms-sdk.md)
