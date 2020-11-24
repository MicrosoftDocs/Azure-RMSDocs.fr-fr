---
title: Classifier & protéger Azure Information Protection client
description: Instructions sur la classification et la protection de vos documents et e-mails lorsque vous utilisez le client Azure Information Protection pour Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: da5c20824af73ed28a602cffb79c3e4167db5bf7
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568115"
---
# <a name="user-guide-classify-and-protect-with-the-azure-information-protection-client"></a>Guide de l’utilisateur : classifier et protéger avec le client Azure Information Protection

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

> [!NOTE]
> Utilisez ces instructions pour classifier et protéger vos documents et e-mails. Si vous avez uniquement besoin de classifier et non de protéger vos documents et e-mails, consultez les [instructions de classification seule](client-classify.md). Si vous ne savez pas quel ensemble d’instructions utiliser, contactez votre administrateur ou votre support technique.

Le plus simple pour classifier et protéger vos documents et vos e-mails consiste à le faire quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Cependant, vous pouvez également classer et protéger les fichiers à l’aide de **l’Explorateur de fichiers**. Cette méthode prend en charge d’autres types de fichiers et est un moyen pratique pour classer et protéger plusieurs fichiers à la fois. Cette méthode prend en charge la protection des documents Office, des fichiers PDF, des fichiers texte et image et d’un large éventail d’autres fichiers. 

Si votre étiquette applique une protection à un document, il n’est pas approprié d’enregistrer un document protégé sur SharePoint ou OneDrive. Ces emplacements ne prennent pas en charge les éléments suivants pour les fichiers protégés : co-création, Office pour le Web, recherche, aperçu du document, miniature et eDiscovery.

> [!TIP]
> Demandez à votre administrateur de migrer vos étiquettes vers des étiquettes de sensibilité unifiée prises en charge pour ces emplacements lorsque [SharePoint est activé pour les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Partager un fichier en toute sécurité avec des personnes extérieures à votre organisation

Le partage de fichiers protégés avec d’autres utilisateurs est sécurisé. Par exemple, vous joignez un document protégé à un e-mail.

Avant de partager des fichiers avec des personnes extérieures à votre organisation, contactez le support technique ou votre administrateur afin de savoir comment protéger des fichiers pour les utilisateurs externes.

Par exemple, si votre organisation communique régulièrement avec des personnes d’une autre organisation, il se peut que votre administrateur ait configuré des étiquettes de sorte que ces personnes puissent lire et utiliser des documents protégés. Si c’est le cas, sélectionnez ces étiquettes pour classifier et protéger les documents à partager.

Ou bien, si des [comptes B2B](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) ont été créés pour les utilisateurs externes, vous pouvez utiliser votre [application Office pour définir des autorisations personnalisées](#set-custom-permissions-for-a-document) ou utiliser l’[Explorateur de fichiers afin de définir des autorisations personnalisées](#using-file-explorer-to-classify-and-protect-files) pour un document avant de le partager. Si vous définissez vos propres autorisations personnalisées et que le document est déjà protégé pour une utilisation interne, commencez par en faire une copie afin de conserver les autorisations d’origine. Utilisez ensuite cette copie pour définir des autorisations personnalisées.


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Utilisation des applications Office pour classifier et protéger vos documents et vos e-mails

Utilisez la barre Azure Information Protection ou le bouton **Protéger** dans le ruban pour sélectionner une des étiquettes qui a été configurée pour vous. 

Par exemple, l’image suivante montre que le document n’a pas encore été étiqueté, car la **Sensibilité** affiche **Non définie** dans la barre Azure Information Protection. Pour définir une étiquette, comme « Général », cliquez sur **Général**. Si vous ne savez pas quelle étiquette appliquer au document ou à l’e-mail actifs, utilisez les info-bulles pour en savoir plus sur chaque étiquette et sur le moment de l’appliquer. 

![Exemple de barre Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Si une étiquette est déjà appliquée au document et que vous souhaitez la modifier, vous pouvez sélectionner une autre étiquette. Si les étiquettes ne sont pas affichées dans la barre, cliquez d’abord sur l’icône **Modifier l’étiquette**, en regard de la valeur actuelle de l’étiquette.

Outre la sélection manuelle, les étiquettes peuvent également être appliquées comme suit :

- Votre administrateur a configuré une étiquette par défaut, que vous pouvez conserver ou modifier.

- Votre administrateur a configuré recommandé des invites pour sélectionner une étiquette spécifique lorsque des données sensibles sont détectées. Vous pouvez accepter la recommandation (et l’étiquette est appliquée), ou la rejeter (l’étiquette recommandée n’est pas appliquée).

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Exceptions de la barre Azure Information Protection 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>Vous ne voyez pas cette barre Information Protection dans vos applications Office ?

Raisons possibles :

- Le client Azure Information Protection n’est pas [installé](install-client-app.md).

- Le client est installé, mais votre administrateur a configuré un paramètre qui n’affiche pas la barre. Sélectionnez plutôt des étiquettes en utilisant le bouton **Protéger** sous l’onglet **Fichier** dans le ruban Office. 

- Votre client s’exécute en [mode Protection uniquement](client-protection-only-mode.md).
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>L’étiquette que vous souhaitez voir ne s’affiche pas dans la barre ? 

Raisons possibles :

- Si votre administrateur a récemment configuré une nouvelle étiquette pour vous, essayez de fermer toutes les instances de votre application Office, puis de la rouvrir. Cette action recherche les modifications apportées à vos étiquettes.

- Si l’étiquette manquante applique la protection, il est possible que vous disposiez d’une édition d’Office qui ne prend pas en charge l’application de la protection Rights Management. Pour vérifier, cliquez sur **protéger**  >  **l’aide et les commentaires**. Dans la boîte de dialogue, vérifiez si vous avez un message dans la section **État du client** indiquant **Ce client n’est pas sous licence pour Office Professionnel Plus**. 
    
    Vous n’avez pas besoin d’Office professionnel plus si vous avez des applications Office à partir de Microsoft 365 Apps for Business ou Microsoft 365 Business Premium quand l’utilisateur se voit attribuer une licence pour Azure Rights Management (également appelée Azure Information Protection pour Office 365).

- L’étiquette peut être dans une stratégie délimitée qui n’inclut pas votre compte. Contactez votre support technique ou votre administrateur.

### <a name="set-custom-permissions-for-a-document"></a>Définir des autorisations personnalisées pour un document

Si vous y êtes autorisé par votre administrateur, vous pouvez spécifier vos propres paramètres de protection pour les documents au lieu d’utiliser les paramètres de protection que votre administrateur peut avoir inclus dans votre étiquette sélectionnée. Cette option est spécifique aux documents et n’est pas disponible avec Outlook.

1. Dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger** > **Autorisations personnalisées** :

    ![Option des autorisations personnalisées](../media/custom-permissions-callout.png)
    
    Si vous ne voyez pas **Autorisations personnalisées**, votre administrateur ne vous permet pas d’utiliser cette option.
    
    Notez que toute autorisation personnalisée que vous spécifiez remplace (plutôt que complète) les paramètres de protection que votre administrateur peut avoir définis pour l’étiquette de votre choix.  

2. Indiquez les éléments suivants dans la boîte de dialogue **Microsoft Azure Information Protection** :

    - **Protéger avec des autorisations personnalisées** : assurez-vous de sélectionner cette option afin de pouvoir spécifier et appliquer vos autorisations personnalisées. Désactivez cette option pour supprimer toutes les autorisations personnalisées.
    
    - **Sélectionner des autorisations** : si vous souhaitez protéger le fichier afin que vous seul puissiez y accéder, sélectionnez **Pour moi uniquement**. Dans le cas contraire, sélectionnez le niveau d’accès que vous souhaitez accorder aux personnes spécifiées.
    
    - **Sélectionner des utilisateurs, des groupes ou des organisations** : spécifiez les personnes qui doivent disposer des autorisations que vous avez sélectionnées pour vos fichiers. Entrez leur adresse e-mail complète, une adresse e-mail de groupe ou un nom de domaine de l’organisation pour tous les utilisateurs appartenant à cette organisation. 
        
        Vous pouvez également utiliser l’icône de carnet d’adresses pour sélectionner des utilisateurs ou des groupes dans le carnet d’adresses Outlook.
    
    - Faire **expirer l’accès**: sélectionnez cette option uniquement pour les fichiers respectant le temps afin que les personnes que vous avez spécifiées ne puissent pas ouvrir le ou les fichiers sélectionnés après une date que vous avez définie. Vous pouvez toujours ouvrir le fichier d’origine mais, le jour spécifié, après minuit (dans votre fuseau horaire), les personnes que vous avez désignées ne pourront plus l’ouvrir.

5. Cliquez sur **Appliquer** et attendez que le message **Autorisations personnalisées appliquées** s’affiche. Cliquez ensuite sur **Fermer**.

### <a name="safely-sharing-by-email"></a>Partage sécurisé par e-mail

Quand vous partagez des documents Office par e-mail, vous pouvez attacher le document à un e-mail que vous protégez : le document est alors automatiquement protégé avec les mêmes restrictions que celles qui s’appliquent à l’e-mail. 

Cependant, nous vous recommandons de commencer par protéger le document avant de l’attacher à l’e-mail. Protégez également l’e-mail si son contenu présente des informations sensibles. Protéger le document avant de l’attacher à un e-mail a deux avantages :

- Vous pouvez tracer et révoquer si nécessaire le document une fois que vous l’avez envoyé par e-mail.

- Vous pouvez appliquer des autorisations différentes au document et à l’e-mail.

## <a name="using-file-explorer-to-classify-and-protect-files"></a>Utilisation de l’Explorateur de fichiers pour classifier et protéger des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier et protéger un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour les options de classification et de protection que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement configurés avec ces options.

Lorsque vous utilisez l’Explorateur de fichiers pour classifier et protéger vos fichiers, si l’une ou plusieurs des étiquettes apparaissent estompées, les fichiers que vous avez sélectionnés ne prennent pas en charge la classification. Pour ces fichiers, vous pouvez sélectionner une étiquette uniquement si votre administrateur l’a configurée pour appliquer une protection. Ou bien, vous pouvez spécifier vos propres paramètres de protection. 

Certains fichiers sont automatiquement exclus de la classification et de la protection, car leur modification peut interrompre l’exécution de votre ordinateur. Bien que vous puissiez sélectionner ces fichiers, ils sont ignorés en tant que fichier ou dossier exclu. Exemples : des fichiers exécutables ou votre dossier Windows.

Le guide d’administration contient une liste complète des types de fichiers pris en charge et des fichiers et dossiers qui sont automatiquement exclus : [Types de fichiers pris en charge par le client Azure Information Protection](client-admin-guide-file-types.md).


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Pour classer et protéger un fichier à l’aide de l’Explorateur de fichiers

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**. Par exemple :
    
    ![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification et la protection comme les a effectuées votre administrateur. 

   - Si aucune des étiquettes ne peut être sélectionnée (elles apparaissent estompées) : le fichier sélectionné ne prend pas en charge la classification, mais vous pouvez le protéger avec des autorisations personnalisées (étape 3). Par exemple :

     ![Aucune étiquette n’est disponible dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)
    
   - Si vous ne voyez pas les étiquettes, mais une option **Protection prédéfinie par l’entreprise** dans cette boîte de dialogue : le client s’exécute en [mode protection uniquement](client-protection-only-mode.md). Sélectionnez un modèle pour appliquer la protection que votre administrateur a configurée pour vous, ou bien sélectionnez **Autorisations personnalisées** pour spécifier vos propres paramètres de protection, puis passez à l’étape 4.
    
     ![Aucune étiquette dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/info-protect-dialog-labels-protection-only.png)
    
3. Si vous y êtes autorisé par votre administrateur, vous pouvez spécifier vos propres paramètres de protection plutôt que d’utiliser les paramètres de protection que votre administrateur peut avoir inclus dans l’étiquette que vous avez sélectionnée. Pour ce faire, sélectionnez **Protéger par des autorisations personnalisées**.
    
    Si vous ne voyez pas **Protéger par des autorisations personnalisées**, votre administrateur ne vous permet pas d’utiliser cette option.
    
    Toute autorisation personnalisée que vous spécifiez remplace (plutôt que complète) les paramètres de protection que votre administrateur peut avoir définis pour l’étiquette de votre choix.  

4. Si vous avez sélectionné l’option d'autorisations personnalisées, spécifiez maintenant ce qui suit :

   - **Sélectionner des autorisations** : sélectionnez le niveau d’accès que vous voulez donner aux utilisateurs quand vous protégez les fichiers sélectionnés.
    
   - **Sélectionner des utilisateurs, des groupes ou des organisations** : spécifiez les personnes qui doivent disposer des autorisations que vous avez sélectionnées pour vos fichiers. Entrez leur adresse e-mail complète, une adresse e-mail de groupe ou un nom de domaine de l’organisation pour tous les utilisateurs appartenant à cette organisation. 
    
     Vous pouvez également utiliser l’icône de carnet d’adresses pour sélectionner des utilisateurs ou des groupes dans le carnet d’adresses Outlook.
        
   - **Faire expirer l’accès** : sélectionnez cette option uniquement pour les fichiers pour lesquels le temps est un facteur critique afin que les personnes que vous avez spécifiées ne soient pas en mesure d’ouvrir le fichier ou les fichiers sélectionnés après une date que vous définissez. Vous serez toujours en mesure d’ouvrir le fichier d’origine mais après minuit (sur votre fuseau horaire), au jour que vous définissez, les personnes que vous avez spécifiées ne pourront pas ouvrir le fichier.
    
     Notez que si ce paramètre a été précédemment configuré à l’aide des autorisations personnalisées à partir d’une application Office 2010, la date d’expiration spécifiée ne s’affiche pas dans cette boîte de dialogue, mais est toujours définie. Il s’agit seulement d’un problème d’affichage lorsque la date d’expiration a été configurée dans Office 2010.

5. Cliquez sur **Appliquer** et attendez le message **Tâche terminée** pour voir les résultats. Cliquez ensuite sur **Fermer**.

Les fichiers sélectionnés sont maintenant classifiés et protégés, conformément à vos sélections. Dans certains cas (quand l’ajout d’une protection modifie l’extension du nom du fichier), le fichier d’origine dans l’Explorateur de fichiers est remplacé par un nouveau fichier associé à l’icône de verrou d’Azure Information Protection. Par exemple :

![Fichier protégé avec une icône de verrou pour Azure Information Protection](../media/Pfile.png)

Si vous changez d’avis sur la classification et la protection, ou avez besoin de modifier vos paramètres, répétez simplement ce processus avec vos nouveaux paramètres.

La classification et la protection que vous avez spécifiées restent avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. Si vous avez protégé le fichier, vous pouvez suivre son utilisation et au besoin, révoquer son accès. Pour plus d’informations, consultez [Suivre et révoquer vos documents protégés quand vous utilisez Azure Information Protection](client-track-revoke.md). 


## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    
Pour des instructions de configuration permettant d’activer le paramètre de stratégie **Rendre l’option des autorisations personnalisées disponible aux utilisateurs**, consultez [Configuration des paramètres de stratégie Azure Information Protection](../configure-policy-settings.md).

Autres instructions de configuration : [Configuration de la stratégie Azure Information Protection](../configure-policy.md).