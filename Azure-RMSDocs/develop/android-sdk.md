---
title: Configuration pour Android | Azure RMS
description: "Les applications Android peuvent utiliser Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations dans leurs applications."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 986f6932-159b-4791-bd1a-7640a83ee792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 3225e143bc80fa35c3e4b96317cdd264f63ac098
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="android-setup"></a>Configuration pour Android

Les applications Android peuvent utiliser Microsoft Rights Management SDK 4.2 pour activer la protection intégrée des informations en utilisant Azure Active Directory Rights Management (AAD RM).

Cette rubrique explique comment configurer votre environnement pour créer vos propres applications.

-   [Prérequis](#prerequisites)
-   [Facultatif](#optional)
-   [Configuration de votre environnement de développement](#configuring-your-development-environment)
-   [Voir aussi](#see-also)

## <a name="prerequisites"></a>Conditions préalables

Nous recommandons les logiciels suivants sur votre système de développement :

-   Système d’exploitation Windows ou OS X pour exécuter l’environnement de développement [Eclipse](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
-   Ce guide suppose que vous utilisez le SDK Eclipse à partir d’Eclipse Juno 4.2 et avec une installation par défaut.
-   Java à partir de Java 1.6.
-   [Plug-in Outils ADT (Android Developer Tools)](http://developer.android.com/sdk/installing/index.html). REMARQUE : Vous devrez peut-être redémarrer Eclipse pour terminer l’installation.

     

-   Le package MS RMS SDK 4.2 pour Android. Pour plus d’informations, consultez [Prise en main](get-started.md).

    Ce SDK peut être utilisé pour développer pour Android 4.0.3 (API niveau 15) et ultérieur.

-   Bibliothèque d’authentification : nous vous recommandons d’utiliser la [bibliothèque ADAL (Azure AD Authentication Library)](https://msdn.microsoft.com/library/jj573266.aspx). Vous pouvez cependant utiliser aussi d’autres bibliothèques d’authentification qui prennent en charge OAuth 2.0.

    Pour plus d’informations, consultez [ADAL pour Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

    **Remarque** : Si votre application ne doit pas utiliser la bibliothèque ADAL comme bibliothèque d’authentification OAuth 2.0, il est conseillé d’examiner ces conseils qui concernent Android : [Some SecureRandom Thoughts](http://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html).

     

Lisez la rubrique [Nouveautés](release-notes.md) pour obtenir des informations sur les mises à jour des API, les notes de publication et les questions les plus fréquentes (FAQ).

## <a name="optional"></a>Facultatif

Notre bibliothèque d’interface utilisateur fournit une interface utilisateur réutilisable pour les opérations de protection et de consommation pour les développeurs qui ne veulent pas créer leur propre interface utilisateur personnalisée : [Bibliothèque d’interface utilisateur et exemple d’application pour Android](https://github.com/AzureAD/rms-sdk-ui-for-android).

## <a name="configuring-your-development-environment"></a>Configuration de votre environnement de développement

**Remarque** : Version préliminaire de MS RMS SDK 4.2 : dans cette version préliminaire, les captures d’écran n’ont pas été mises à jour pour montrer la modification du nom des chemins, de com/microsoft/protection en com/microsoft/rightsmanagment. Le texte a cependant été mis à jour.

 
-   Ouvrez l’environnement de développement Eclipse.
-   Pour créer un projet d’application Android, dans le menu **Fichier**, cliquez sur **Nouveau**, cliquez sur **Projet**, puis sélectionnez **Projet d’application Android**.

    ![Créez une application Android](../media/Android-setup-01c.png)

-   Entrez le nom de l’application. Le nom du projet et le nom du package sont renseignés en fonction du nom de l’application.
-   Cliquez sur **Suivant** et choisissez où vous voulez créer l’espace de travail.

    ![Entrez le nom de l’application](../media/Android-setup-02a.jpg)

-   Cliquez sur **Suivant** et sélectionnez une icône pour votre application.

    ![Sélectionnez une icône pour votre application](../media/Android-setup-03.png)

-   Cliquez sur **Suivant** et sélectionnez **Activité vide** pour créer l’activité.

    ![Créez l’activité](../media/Android-setup-04.png)

-   Cliquez sur **Suivant** et indiquez un nom pour l’activité. Vous pouvez laisser *MainActivity* comme nom par défaut avec un nom d’affichage *activity\_main*.

    ![Spécifiez un nom pour l’activité](../media/Android-setup-05a.jpg)

-   Cliquez sur **Terminer**.

    ![Terminez la création](../media/Android-setup-06.jpg)

-   Votre projet a été créé, ainsi que la classe d’activité principale *MainActivity.java*.

**Faire référence au SDK**

-   Accédez au dossier où vous avez extrait *adrms\_android\_sdk.zip*. Dans le dossier « SDK > com > microsoft > rightsmanagement », vérifiez que les fichiers *.classpath*, *.project* et *project.properties* ne sont pas marqués en lecture seule.
-   Pour faire référence au SDK, vous devez l’importer dans l’espace de travail.

    Dans Eclipse, cliquez sur **Fichier**. Dans le menu **Fichier**, cliquez sur **Importer**. Dans la boîte de dialogue **Importer**, sélectionnez **Android / Code Android existant dans l’espace de travail**.

    ![Importez-le dans l’espace de travail](../media/Android-setup-07.png)

-   Cliquez sur **Suivant**. Accédez au dossier où vous avez extrait *adrms\_android\_sdk.zip*. Le SDK doit apparaître dans la liste comme **com.microsoft.rightsmanagement**.

    ![Naviguez pour sélectionner le dossier](../media/Android-setup-08c.jpg)

-   Quand vous cliquez sur **Terminer**, le projet de SDK s’affiche comme frère de votre application précédemment créée.

    ![Le projet du SDK s’affiche en tant que frère de votre application](../media/Android-setup-09.jpg)

-   Cliquez avec le bouton droit sur l’icône **Projet** et examinez les propriétés du projet.
-   Accédez à l’onglet **Android**.
-   Cliquez sur **Ajouter**, puis sélectionnez la bibliothèque *com.microsoft.rightsmanagement* à partir de l’espace de travail.

    ![Ajoutez la bibliothèque](../media/Android-setup-10b.jpg)

-   Cliquez sur **OK**.

    Comme MS RMS SDK 4.2 se connecte avec AAD RM, **INTERNET** et **ACCESS\_NETWORK\_STATE** doivent être accordés à l’application. Pour cela, ouvrez le fichier *AndroidManifest.xml* à la racine du projet.

    Pour ajouter les autorisations, cliquez sur **Ajouter**, puis sélectionnez **Utilise les autorisations**.

    ![Ajoutez des autorisations](../media/Android-setup-11d.jpg)

-   Vous pouvez vérifier l’étape du manifeste en consultant le manifeste dans l’affichage de l’éditeur de texte. Vérifiez que les lignes suivantes s’affichent :


    <uses-sdk      android:minSdkVersion="15"      android:targetSdkVersion="19"/> <uses-permission android:name="android.permission.INTERNET"/> <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> <uses-permission/>


**Remarque** : Le SDK utilise *android.support.v4*

-   Vous êtes maintenant prêt à créer vos propres applications Android.

### <a name="see-also"></a>Voir aussi

[Prise en main](get-started.md)

[Nouveautés](release-notes.md)

[Terminologie et concepts du développement](core-concepts.md)

[Informations de référence sur l’API Android](https://msdn.microsoft.com/library/dn758245.aspx)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]