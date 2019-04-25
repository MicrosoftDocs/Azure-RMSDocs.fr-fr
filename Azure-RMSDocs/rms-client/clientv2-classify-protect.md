---
title: Classifier et protéger à l’aide du client d’étiquetage unifié Azure Information Protection pour Windows
description: Instructions comment classifier et protéger vos documents et e-mails lorsque vous utilisez Azure Information Protection unifiée étiquetage client pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 0404acb6f79100a78d955a94f67ea0a0a7aaf604
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181342"
---
# <a name="user-guide-classify-and-protect-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>Guide de l’utilisateur : Classifier et protéger un fichier ou un e-mail en utilisant le client d’étiquetage unifié Azure Information Protection pour Windows

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Utilisez ces instructions pour classifier et protéger vos documents et e-mails. Si vous avez uniquement besoin de classifier et non de protéger vos documents et e-mails, consultez les [instructions de classification seule](clientv2-classify.md). Si vous ne savez pas quel ensemble d’instructions utiliser, contactez votre administrateur ou votre support technique.

La façon la plus simple de classifier et de protéger vos documents et vos e-mails consiste à le faire quand vous les créez ou que vous les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Cependant, vous pouvez également classer et protéger les fichiers à l’aide de **l’Explorateur de fichiers**. Cette méthode prend en charge d’autres types de fichiers et est un moyen pratique pour classer et protéger plusieurs fichiers à la fois. Cette méthode prend en charge la protection des documents Office, des fichiers PDF, des fichiers texte et image et d’un large éventail d’autres fichiers. 

Si votre étiquette applique une protection à un document, il n’est pas approprié d’enregistrer un document protégé sur SharePoint ou OneDrive. Ces emplacements ne prennent pas en charge les éléments suivants pour les fichiers protégés : Co-création, Office Online, recherche, aperçu du document, miniature et eDiscovery.

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Partager un fichier en toute sécurité avec des personnes extérieures à votre organisation

Le partage de fichiers protégés avec d’autres utilisateurs est sécurisé. Par exemple, vous joignez un document protégé à un e-mail.

Avant de partager des fichiers avec des personnes extérieures à votre organisation, contactez le support technique ou votre administrateur afin de savoir comment protéger des fichiers pour les utilisateurs externes.

Par exemple, si votre organisation communique régulièrement avec des personnes d’une autre organisation, votre administrateur peut avoir configuré des étiquettes qui définissent une protection permettant à ces personnes de lire et d’utiliser des documents protégés. Vous pouvez ensuite sélectionner ces étiquettes pour classifier et protéger les documents à partager.

Vous pouvez également, si les utilisateurs externes ont [les comptes business-to-business (B2B)](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) créées pour eux, vous pouvez utiliser [Explorateur de fichiers pour définir des autorisations personnalisées](#using-file-explorer-to-classify-and-protect-files) pour un document avant de le partager. Si vous définissez vos propres autorisations personnalisées et que le document est déjà protégé pour une utilisation interne, commencez par en faire une copie afin de conserver les autorisations d’origine. Utilisez ensuite cette copie pour définir des autorisations personnalisées.


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Utilisation des applications Office pour classifier et protéger vos documents et vos e-mails

À partir de la **accueil** onglet, sélectionnez le **sensibilité** bouton sur le ruban, puis sélectionnez une des étiquettes qui a été configurée pour vous. Exemple :

![Exemple de bouton de sensibilité](../media/sensitivity-not-set-callout.png)

Ou, si vous avez sélectionné **afficher la barre** à partir de la **sensibilité** bouton, vous pouvez sélectionner une étiquette à partir de la barre Azure Information Protection. Exemple :

![Exemple de barre Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Pour définir une étiquette, telles que «**confidentiel** \ **tous les employés**», sélectionnez **confidentiel** , puis **tous les employés**. Si vous ne savez pas quelle étiquette appliquer au document ou à l’e-mail actifs, utilisez les info-bulles pour en savoir plus sur chaque étiquette et sur le moment de l’appliquer. Si une étiquette est déjà appliquée au document et que vous souhaitez la modifier, vous pouvez sélectionner une autre étiquette. Si vous avez affiché la barre Azure Information Protection, et les étiquettes ne sont pas affichées dans la barre pour sélectionner, cliquez d’abord sur le **modifier l’étiquette** icône, en regard de la valeur actuelle de l’étiquette.

Outre la sélection manuelle, les étiquettes peuvent également être appliquées comme suit :

- Votre administrateur a configuré une étiquette par défaut, que vous pouvez conserver ou modifier.

- Votre administrateur a configuré les étiquettes à définir automatiquement lors de la détection des informations sensibles.

- Votre administrateur a configuré recommandé des étiquettes lorsque des informations sensibles sont détectées et vous êtes invité à accepter la recommandation (et l’étiquette est appliquée), ou la rejeter (l’étiquette recommandée n’est pas appliqué).

### <a name="exceptions-for-the-sensitivity-button"></a>Exceptions pour le bouton de sensibilité

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Ne voyez pas le bouton de sensibilité dans vos applications Office ?

- Vous ne disposez pas de client Azure Information Protection unifié étiquetage [installé](install-unifiedlabelingclient-app.md).

- Si vous ne voyez pas un **sensibilité** bouton sur le ruban, mais apparaissent un **protéger** bouton avec des étiquettes au lieu de cela, vous avez le client Azure Information Protection est installé et pas Azure Information Protection client d’étiquetage unifié. [Plus d’informations](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>L’étiquette que vous souhaitez voir ne s’affiche pas dans la barre ? 

Raisons possibles :

- Si votre administrateur a récemment configuré une nouvelle étiquette pour vous, essayez de fermer toutes les instances de votre application Office, puis de la rouvrir. Cette action recherche les modifications apportées à vos étiquettes.

- Si l’étiquette manquante applique la protection, il est possible que vous disposiez d’une édition d’Office qui ne prend pas en charge l’application de la protection Rights Management. Pour vérifier, cliquez sur **Protéger** > **Aide et commentaires**. Dans la boîte de dialogue, vérifiez si vous avez un message dans la section **État du client** indiquant **Ce client n’est pas sous licence pour Office Professionnel Plus**. 
    
    Vous n’avez pas besoin d’Office Professionnel Plus si vous avez des applications Office d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est affectée à l’utilisateur.

- L’étiquette peut être dans une stratégie délimitée qui n’inclut pas votre compte. Contactez votre support technique ou votre administrateur.


### <a name="safely-sharing-by-email"></a>Partage sécurisé par e-mail

Quand vous partagez des documents Office par e-mail, vous pouvez attacher le document à un e-mail que vous protégez : le document est alors automatiquement protégé avec les mêmes restrictions que celles qui s’appliquent à l’e-mail. 

Toutefois, vous souhaiterez peut-être protéger le document, puis l’attacher à l’adresse e-mail. Protégez également l’e-mail si son contenu présente des informations sensibles. Un avantage de la protection du document avant de le joindre à un message électronique :

- Vous pouvez appliquer des autorisations différentes au document et à l’e-mail.

## <a name="using-file-explorer-to-classify-and-protect-files"></a>Utilisation de l’Explorateur de fichiers pour classifier et protéger des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier et protéger un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour les options de classification et de protection que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement configurés avec ces options.

Lorsque vous utilisez l’Explorateur de fichiers pour classifier et protéger vos fichiers, si l’une ou plusieurs des étiquettes apparaissent estompées, les fichiers que vous avez sélectionnés ne prennent pas en charge la classification. Pour ces fichiers, vous pouvez sélectionner une étiquette uniquement si votre administrateur l’a configurée pour appliquer une protection. Ou bien, vous pouvez spécifier vos propres paramètres de protection. 

Certains fichiers sont automatiquement exclus de la classification et de la protection, car leur modification peut interrompre l’exécution de votre ordinateur. Bien que vous puissiez sélectionner ces fichiers, ils sont ignorés en tant que fichier ou dossier exclu. Exemples : des fichiers exécutables ou votre dossier Windows.

Le guide d’administration contient une liste complète des types de fichiers pris en charge, et des fichiers et dossiers qui sont automatiquement exclus : [Types pris en charge par le client d’étiquetage unifié Azure Information Protection de fichiers](clientv2-admin-guide-file-types.md).


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Pour classer et protéger un fichier à l’aide de l’Explorateur de fichiers

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**. Exemple :
    
    ![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification et la protection comme les a effectuées votre administrateur. 

   - Si aucune des étiquettes ne peut être sélectionnée (elles apparaissent estompées) : Le fichier sélectionné ne prend pas en charge la classification, mais vous pouvez le protéger avec des autorisations personnalisées (étape 3). Exemple :

     ![Aucune étiquette n’est disponible dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. Vous pouvez spécifier vos propres paramètres de protection plutôt que d’utiliser les paramètres de protection que votre administrateur peut avoir inclus dans votre étiquette sélectionnée. Pour ce faire, sélectionnez **Protéger par des autorisations personnalisées**.
    
    Toute autorisation personnalisée que vous spécifiez remplace (plutôt que complète) les paramètres de protection que votre administrateur peut avoir définis pour l’étiquette de votre choix.  

4. Si vous avez sélectionné l’option d'autorisations personnalisées, spécifiez maintenant ce qui suit :

   - **Sélectionner des autorisations** : Sélectionnez le niveau d’accès que vous voulez donner aux utilisateurs quand vous protégez les fichiers sélectionnés.
    
   - **Sélectionner des utilisateurs, des groupes ou des organisations** : Spécifiez les personnes qui doivent disposer des autorisations que vous avez sélectionnées pour vos fichiers. Entrez leur adresse e-mail complète, une adresse e-mail de groupe ou un nom de domaine de l’organisation pour tous les utilisateurs appartenant à cette organisation. 
    
     Vous pouvez également utiliser l’icône de carnet d’adresses pour sélectionner des utilisateurs ou des groupes dans le carnet d’adresses Outlook.
        
    - **Expiration d’accès** : Sélectionnez cette option uniquement pour les fichiers urgents afin que les personnes que vous avez spécifié ne peut pas ouvrir votre fichier sélectionné ou les fichiers après une date que vous définissez. Vous pouvez toujours ouvrir le fichier d’origine mais, le jour spécifié, après minuit (dans votre fuseau horaire), les personnes que vous avez désignées ne pourront plus l’ouvrir.
    
     Notez que si ce paramètre a été précédemment configuré à l’aide des autorisations personnalisées à partir d’une application Office 2010, la date d’expiration spécifiée ne s’affiche pas dans cette boîte de dialogue, mais est toujours définie. Il s’agit seulement d’un problème d’affichage lorsque la date d’expiration a été configurée dans Office 2010.

5. Cliquez sur **Appliquer** et attendez le message **Tâche terminée** pour voir les résultats. Cliquez ensuite sur **Fermer**.

Les fichiers sélectionnés sont maintenant classifiés et protégés, conformément à vos sélections. Dans certains cas (quand l’ajout d’une protection modifie l’extension du nom du fichier), le fichier d’origine dans l’Explorateur de fichiers est remplacé par un nouveau fichier associé à l’icône de verrou d’Azure Information Protection. Exemple :

![Fichier protégé avec une icône de verrou pour Azure Information Protection](../media/Pfile.png)

Si vous changez d’avis sur la classification et la protection, ou avez besoin de modifier vos paramètres, répétez simplement ce processus avec vos nouveaux paramètres.

La classification et la protection que vous avez spécifiées restent avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. 

## <a name="other-instructions"></a>Autres instructions
Guident de la plus obtenir des instructions à partir de l’utilisateur pour le client d’étiquetage unifiée Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    

Consultez [vue d’ensemble des étiquettes de sensibilité](/Office365/SecurityCompliance/sensitivity-labels).
