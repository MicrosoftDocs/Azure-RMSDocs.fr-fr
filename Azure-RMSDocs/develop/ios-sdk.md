---
title: Installation iOS et OS X | Azure RMS
description: "Les applications iOS et OS X peuvent utiliser RMS SDK 4.2 pour activer la protection intégrée des informations dans leur application à l’aide d’AAD RM."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b31e5b72-e65e-450a-b1b8-d46e81e9fb34
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 80d79ead119b5dbe86d94f979742ecc2b62d1ef9


---

# Installation iOS et OS X

Les applications iOS et OS X peuvent utiliser Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations dans leur application à l’aide d’Azure Rights Management (Azure RMS).

Cette rubrique explique comment configurer votre environnement pour créer vos propres applications.

**Remarque**  Ce SDK ne prend pas en charge l’iPod Touch.


-   [Conditions préalables](#prerequisites)
-   [Facultatif](#optional)
-   [Configuration de votre environnement de développement](#configuring-your-development-environment)
-   [Voir aussi](#see-also)

## Conditions préalables

Nous vous recommandons de disposer des logiciels suivants sur votre système de développement :

-   OS X est obligatoire pour tout développement iOS.
-   Xcode version 6.0 ou ultérieure

    Xcode est disponible par le biais du [Mac App Store](https://developer.apple.com/technologies/mac/).

-   Package MS RMS SDK 4.2 pour iOS et OS X. Pour plus d’informations, consultez [Prise en main](get-started.md).

    Vous pouvez utiliser ce SDK pour développer pour iOS 7.0 et OS X 10.8 et versions ultérieures.

-   Bibliothèque d’authentification : nous vous recommandons d’utiliser la [bibliothèque ADAL (Azure AD Authentication Library)](https://msdn.microsoft.com/library/jj573266.aspx). Toutefois, vous pouvez aussi utiliser d’autres bibliothèques d’authentification qui prennent en charge OAuth 2.0.

    Pour plus d’informations, consultez [ADAL pour iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) ou [ADAL pour OS X](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal)

Lisez la rubrique [Nouveautés](release-notes.md) pour obtenir des informations sur les mises à jour des API, les notes de publication et les questions les plus fréquentes (FAQ).

## Facultatif

Notre bibliothèque d’interface utilisateur fournit une interface utilisateur réutilisable pour les opérations de protection et de consommation pour les développeurs qui ne souhaitent pas créer leur propre interface utilisateur personnalisée - [Bibliothèque d’interface utilisateur et exemple d’application pour iOS](https://github.com/AzureAD/rms-sdk-ui-for-ios).

## Configuration de votre environnement de développement

-   Pour créer un projet, dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.
-   Sélectionnez **Single View Application**.

    ![Créer un nouveau projet](../media/iOS-Project.png)

-   Entrez un nom et un identificateur pour votre nouveau projet.

    ![Nommez votre projet](../media/iOS-project-options.png)

-   Cliquez sur **Suivant** et sélectionnez l’emplacement de votre projet.
-   Pour ajouter l’infrastructure **MSRightsManagement** aux Frameworks iOS, faites glisser le dossier .framework à partir du dossier d’installation du SDK vers la section **Frameworks** de votre **Project Navigator**.

    ![Définissez un emplacement](../media/ios-add-dependencies-01a.png)

-   Sélectionnez la case d’option **Create groups for any added folders** et décochez la case **Copy items into destination group’s folder (if needed)**.

    Cette action conserve la référence au dossier d’installation du SDK au lieu de créer une copie.

    ![Définissez la référence au dossier d’installation du SDK](../media/iOS-create-groups.png)

-   Pour ajouter MS RMS SDK 4.2 pour le groupe de ressources, faites glisser le fichier MSRightsManagementResources.bundle du dossier MSRightsManagement.framework/Resources vers la section **Frameworks** de votre Project Navigator.

    ![Ajoutez le groupe de ressources](../media/iOS-add-resource-bundle-02a.png)

-   Comme vous l’avez fait quand vous avez copié le Framework, sélectionnez la case d’option **Create groups for any added folders** (Créer des groupes pour tout dossier ajouté) et décochez la case **Copy items into destination group’s folder (if needed)** (Copier les éléments dans le dossier du groupe de destination si nécessaire).
-   Le SDK s’appuie sur d’autres infrastructures, notamment : **CoreData**, **MessageUI**, **SystemConfiguration**, **Libresolv** et **Security**. Pour ajouter ces infrastructures, accédez à la section **Linked Frameworks and Libraries** (Infrastructures et bibliothèques liées) du volet **Summary** (Résumé) de la cible et développez cette section pour les ajouter.

    Les infrastructures **UIKit** et **Foundation** sont obligatoires et généralement présentes par défaut.

    ![Ajoutez des ressources](../media/iOS-add-libraries.png)

-   Ajoutez l’indicateur **-ObjC** à **Other Linker Flags** (Autres indicateurs d’éditeur de lien) dans vos **Build Settings** (Paramètres de build) cibles.

    ![Ajoutez des paramètres de build](../media/iOS-linker-flags.png)

-   Maintenant, votre **Project Navigator** doit ressembler à cette arborescence.

    ![Passez en revue le projet](../media/iOS-verify-setup-01a.png)

-   Vous êtes maintenant prêt à créer vos propres applications iOS/OS X.

### Voir aussi

* [Prise en main](get-started.md)

* [Nouveautés](release-notes.md)

* [Terminologie et concepts du développement](core-concepts.md)

* [Référence d’API iOS / OS X](https://msdn.microsoft.com/library/dn758306.aspx)

 

 



<!--HONumber=Sep16_HO5-->


