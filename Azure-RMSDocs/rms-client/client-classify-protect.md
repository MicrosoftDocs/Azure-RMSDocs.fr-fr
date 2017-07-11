---
title: "Classifier et protéger un document avec Azure Information Protection"
description: Instructions sur la classification et la protection de vos documents et e-mails.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 960fe1abf2fa4f5b8976f190454d31849736298a
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="classify-and-protect-a-file-or-email-by-using-azure-information-protection" class="xliff"></a>

# Classifier et protéger un fichier ou un e-mail avec Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

Le plus simple pour classifier et protéger vos documents et vos e-mails consiste à le faire quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Toutefois, vous pouvez également classifier et protéger des fichiers à l’aide de l’**Explorateur de fichiers**, lequel prend en charge des types de fichiers supplémentaires et constitue un moyen pratique de classifier et protéger plusieurs fichiers à la fois. Cette méthode prend en charge la protection des documents Office, des fichiers PDF, des fichiers texte et image et d’un large éventail d’autres fichiers. 

<a id="safely-share-a-file-with-people-outside-your-organization" class="xliff"></a>

### Partager un fichier en toute sécurité avec des personnes extérieures à votre organisation

Le partage de fichiers protégés avec d’autres utilisateurs est sécurisé. Par exemple, vous joignez le fichier à un e-mail ou envoyez une invitation à partir de votre site SharePoint.

Si vous partagez régulièrement des fichiers avec des personnes extérieures à votre organisation, votre administrateur peut avoir configuré une étiquette pour vous qui définit la protection de sorte que ces personnes puissent les lire. Sinon, vous pouvez utiliser votre [application Office pour définir des autorisations personnalisées](#set-custom-permissions-for-a-document) ou utiliser l’[Explorateur de fichiers pour définir des autorisations personnalisées](#using-file-explorer-to-classify-and-protect-files) pour un fichier avant de le partager. 

Si vous définissez vos propres autorisations personnalisées et que le fichier est déjà protégé pour une utilisation interne, commencez par en faire une copie afin de conserver les autorisations d’origine. Utilisez ensuite cette copie pour définir des autorisations personnalisées.  

Lorsque le fichier est protégé avec vos autorisations personnalisées, partagez le fichier comme vous le faites habituellement. Si c’est la première fois que les utilisateurs avec lesquels vous partagez le fichier reçoivent un fichier protégé, ils auront peut-être besoin d’instructions pour l’afficher. Pour ces utilisateurs, vous pouvez copier et coller le message suivant : **J’ai protégé ce fichier avec Microsoft Azure Information Protection. Pour une première utilisation, consultez ces [instructions](https://aka.ms/rms-signup).**


<a id="using-office-apps-to-classify-and-protect-your-documents-and-emails" class="xliff"></a>

## Utilisation des applications Office pour classifier et protéger vos documents et vos e-mails

Utilisez la barre Azure Information Protection et sélectionnez une des étiquettes qui a été configurée pour vous. 

Par exemple, l’image suivante montre que le document n’a pas encore été étiqueté, car la **Sensibilité** affiche **Non défini**. Pour définir une étiquette, par exemple « Interne », cliquez sur **Interne**. Si vous ne savez pas quelle étiquette appliquer au document ou à l’e-mail actifs, utilisez les info-bulles pour en savoir plus sur chaque étiquette et sur le moment de l’appliquer.

![Exemple de barre Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Si une étiquette est déjà appliquée au document et que vous souhaitez la modifier, vous pouvez sélectionner une autre étiquette. Si les étiquettes ne sont pas affichées dans la barre, cliquez d’abord sur l’icône **Modifier l’étiquette**, en regard de la valeur actuelle de l’étiquette.

Outre la sélection manuelle, les étiquettes peuvent également être appliquées comme suit :

- Votre administrateur a configuré une étiquette par défaut, que vous pouvez conserver ou modifier.

- Votre administrateur a configuré recommandé des invites pour sélectionner une étiquette spécifique lorsque des données sensibles sont détectées. Vous pouvez accepter la recommandation (et l’étiquette est appliquée), ou la rejeter (l’étiquette recommandée n’est pas appliquée).

<a id="exceptions-for-the-azure-information-protection-bar" class="xliff"></a>

### Exceptions de la barre Azure Information Protection 

<a id="dont-see-this-information-protection-bar-in-your-office-apps" class="xliff"></a>

##### Vous ne voyez pas cette barre Information Protection dans vos applications Office ?

- Le client Azure Information Protection n’est pas [installé](install-client-app.md), ou le client est en cours d’exécution en [mode Protection uniquement](client-protection-only-mode.md).
 
<a id="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar" class="xliff"></a>

##### L’étiquette que vous souhaitez voir ne s’affiche pas dans la barre ? 

- Si votre administrateur a récemment configuré une nouvelle étiquette pour vous, essayez de fermer toutes les instances de votre application Office, puis de la rouvrir. Cette action recherche les modifications apportées à vos étiquettes.

- Si l’étiquette manquante applique la protection, il est possible que vous disposiez d’une édition d’Office qui ne prend pas en charge l’application de la protection Rights Management. Pour vérifier, cliquez sur **Protéger** > **Aide et commentaires**, et vérifiez si vous avez un message dans la section **État du client** indiquant **Ce client n'est pas sous licence pour Office Professionnel Plus.** 

- L’étiquette peut être dans une stratégie délimitée qui n’inclut pas votre compte. Contactez votre support technique ou votre administrateur.

<a id="set-custom-permissions-for-a-document" class="xliff"></a>

### Définir des autorisations personnalisées pour un document

Vous pouvez spécifier vos propres paramètres de protection pour les documents plutôt que d’utiliser les paramètres de protection que votre administrateur peut avoir inclus dans votre étiquette sélectionnée.

1. Dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger** > **Autorisations personnalisées** :

    ![Option Autorisations personnalisées](../media/custom-permissions-callout.png)
    
    Notez que toute autorisation personnalisée que vous spécifiez remplace (plutôt que complète) les paramètres de protection que votre administrateur peut avoir définis pour l’étiquette de votre choix.  

2. Indiquez les éléments suivants dans la boîte de dialogue **Microsoft Azure Information Protection** :

    - **Protéger avec des autorisations personnalisées** : assurez-vous de sélectionner cette option afin de pouvoir spécifier et appliquer vos autorisations personnalisées. Désactivez cette option pour supprimer toutes les autorisations personnalisées.
    
    - **Sélectionner des autorisations** : si vous souhaitez protéger le fichier afin que vous seul puissiez y accéder, sélectionnez **Pour moi uniquement**. Dans le cas contraire, sélectionnez le niveau d’accès que vous souhaitez accorder aux personnes spécifiées.

    - **Sélectionner des utilisateurs, des groupes ou des organisations** : spécifiez les personnes qui doivent disposer des autorisations que vous avez sélectionnées pour vos fichiers. Entrez leur adresse e-mail complète, une adresse e-mail de groupe ou un nom de domaine de l’organisation pour tous les utilisateurs appartenant à cette organisation. Attention, les adresses e-mail personnelles ne sont actuellement pas prises en charge.
        
    - **Faire expirer l’accès** : sélectionnez cette option uniquement pour les fichiers pour lesquels le temps est un facteur critique afin que les personnes que vous avez spécifiées ne soient pas en mesure d’ouvrir le fichier ou les fichiers sélectionnés après une date que vous définissez. Vous serez toujours en mesure d’ouvrir le fichier d’origine mais après minuit (sur votre fuseau horaire), au jour que vous définissez, les personnes que vous avez spécifiées ne pourront pas ouvrir le fichier.

5. Cliquez sur **Appliquer** et attendez que le message **Autorisations personnalisées appliquées** s’affiche. Cliquez ensuite sur **Fermer**.


<a id="keyboard-shortcuts-for-the-azure-information-protection-bar" class="xliff"></a>

### Raccourcis clavier de la barre Azure Information Protection

Pour accéder à la barre Azure Information Protection à l’aide du clavier, utilisez la combinaison de touches suivante :

- Appuyez sur **Ctrl** + **Maj** + **~** 

Utilisez ensuite la touche de tabulation pour sélectionner les étiquettes et autres commandes de la barre (icônes **Masquer les étiquettes** et **Supprimer l’étiquette**), puis appuyez sur la touche Entrée pour les sélectionner.

<a id="using-file-explorer-to-classify-and-protect-files" class="xliff"></a>

## Utilisation de l’Explorateur de fichiers pour classifier et protéger des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier et protéger un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour les options de classification et de protection que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement configurés avec ces options.

Lorsque vous utilisez l’Explorateur de fichiers pour classifier et protéger vos fichiers, si l’une ou plusieurs des étiquettes apparaissent estompées, les fichiers que vous avez sélectionnés ne prennent pas en charge la classification. Pour ces fichiers, vous pouvez sélectionner une étiquette uniquement si votre administrateur l’a configurée pour appliquer une protection. Ou bien, vous pouvez spécifier vos propres paramètres de protection. 

Certains fichiers sont automatiquement exclus de la classification et de la protection, car leur modification peut interrompre l’exécution de votre ordinateur. Bien que vous puissiez sélectionner ces fichiers, ils sont ignorés en tant que fichier ou dossier exclu. Exemples : des fichiers exécutables ou votre dossier Windows.

Le guide d’administration contient une liste complète des types de fichiers pris en charge et des fichiers et dossiers qui sont automatiquement exclus : [Types de fichiers pris en charge par le client Azure Information Protection](client-admin-guide-file-types.md).


<a id="to-classify-and-protect-a-file-by-using-file-explorer" class="xliff"></a>

### Pour classer et protéger un fichier à l’aide de l’Explorateur de fichiers

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**. Exemple :
    
    ![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification et la protection comme les a effectuées votre administrateur. 

    - Si aucune des étiquettes ne peut être sélectionnée (elles apparaissent estompées) : le fichier sélectionné ne prend pas en charge la classification, mais vous pouvez le protéger avec des autorisations personnalisées (étape 3). Exemple :

    ![Aucune étiquette n’est disponible dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)
    
    - Si vous ne voyez pas les étiquettes, mais une option **Protection prédéfinie par l’entreprise** dans cette boîte de dialogue : le client s’exécute en [mode protection uniquement](client-protection-only-mode.md). Sélectionnez un modèle pour appliquer la protection que votre administrateur a configurée pour vous, ou bien sélectionnez **Autorisations personnalisées** pour spécifier vos propres paramètres de protection, puis passez à l’étape 4.
    
    ![Aucune étiquette dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/info-protect-dialog-labels-protection-only.png)
    
3. Si vous souhaitez spécifier vos propres paramètres de protection plutôt que d’utiliser les paramètres de protection que votre administrateur peut avoir inclus dans votre étiquette sélectionnée, sélectionnez la protection **Protéger avec des autorisations personnalisées**.
    
    Toute autorisation personnalisée que vous spécifiez remplace (plutôt que complète) les paramètres de protection que votre administrateur peut avoir définis pour l’étiquette de votre choix.  

4. Si vous avez sélectionné l’option d'autorisations personnalisées, spécifiez maintenant ce qui suit :

    - **Sélectionner des autorisations** : sélectionnez le niveau d’accès que vous voulez donner aux utilisateurs quand vous protégez les fichiers sélectionnés.
    
    - **Sélectionner des utilisateurs** : spécifiez les personnes qui doivent disposer des autorisations que vous avez sélectionnées pour vos fichiers. Vous serez peut-être en mesure de les sélectionner dans le carnet d’adresses (par exemple, les personnes de votre organisation et vos contacts d’autres organisations). Pour les autres, saisissez leur adresse e-mail complète, une adresse e-mail de groupe ou un nom de domaine de l’organisation pour tous les utilisateurs appartenant à cette organisation. Attention, les adresses e-mail personnelles ne sont actuellement pas prises en charge.
        
    - **Faire expirer l’accès** : sélectionnez cette option uniquement pour les fichiers pour lesquels le temps est un facteur critique afin que les personnes que vous avez spécifiées ne soient pas en mesure d’ouvrir le fichier ou les fichiers sélectionnés après une date que vous définissez. Vous serez toujours en mesure d’ouvrir le fichier d’origine mais après minuit (sur votre fuseau horaire), au jour que vous définissez, les personnes que vous avez spécifiées ne pourront pas ouvrir le fichier.
    
    Notez que si ce paramètre a été précédemment configuré à l’aide des autorisations personnalisées à partir d’une application Office 2010, la date d’expiration spécifiée ne s’affiche pas dans cette boîte de dialogue, mais est toujours définie. Il s’agit seulement d’un problème d’affichage lorsque la date d’expiration a été configurée dans Office 2010.

5. Cliquez sur **Appliquer** et attendez le message **Tâche terminée** pour voir les résultats. Cliquez ensuite sur **Fermer**.

Les fichiers sélectionnés sont maintenant classifiés et protégés, conformément à vos sélections. Dans certains cas (quand l’ajout d’une protection modifie l’extension du nom du fichier), le fichier d’origine dans l’Explorateur de fichiers est remplacé par un nouveau fichier associé à l’icône de verrou d’Azure Information Protection. Exemple :

![Fichier protégé avec une icône de verrou pour Azure Information Protection](../media/Pfile.png)

Si vous changez d’avis sur la classification et la protection, ou avez besoin de modifier vos paramètres, répétez simplement ce processus avec vos nouveaux paramètres.

La classification et la protection que vous avez spécifiées restent avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. Si vous avez protégé le fichier, vous pouvez suivre son utilisation et au besoin, révoquer son accès. Pour plus d’informations, consultez [Suivre et révoquer vos documents protégés quand vous utilisez Azure Information Protection](client-track-revoke.md). 


<a id="other-instructions" class="xliff"></a>

## Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
