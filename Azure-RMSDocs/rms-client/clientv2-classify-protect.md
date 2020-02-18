---
title: Classifier & protéger Azure Information Protection client d’étiquetage unifié
description: Instructions sur la classification et la protection de vos documents et e-mails lors de l’utilisation du client d’étiquetage unifié Azure Information Protection pour Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: f51d3a901808a4689e651c6736c6ac8294e1e602
ms.sourcegitcommit: 98d539901b2e5829a2aad685d10fb13fd8d7dec4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2020
ms.locfileid: "77423072"
---
# <a name="user-guide-classify-and-protect-with-the-azure-information-protection-unified-labeling-client"></a>Guide de l’utilisateur : classifier et protéger avec le client d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Utilisez ces instructions pour classifier et protéger vos documents et e-mails. Si vous avez uniquement besoin de classifier et non de protéger vos documents et e-mails, consultez les [instructions de classification seule](clientv2-classify.md). Si vous ne savez pas quel ensemble d’instructions utiliser, contactez votre administrateur ou votre support technique.

Le plus simple pour classifier et protéger vos documents et vos e-mails consiste à le faire quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Cependant, vous pouvez également classer et protéger les fichiers à l’aide de **l’Explorateur de fichiers**. Cette méthode prend en charge d’autres types de fichiers et est un moyen pratique pour classer et protéger plusieurs fichiers à la fois. Cette méthode prend en charge la protection des documents Office, des fichiers PDF, des fichiers texte et image et d’un large éventail d’autres fichiers. 

Si votre étiquette applique la protection à un document, il est possible que le document protégé ne convienne pas à un enregistrement sur SharePoint ou OneDrive. Vérifiez si votre administrateur a [activé les étiquettes de sensibilité pour les fichiers Office dans SharePoint et OneDrive (version préliminaire publique)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Partager un fichier en toute sécurité avec des personnes extérieures à votre organisation

Le partage de fichiers protégés avec d’autres utilisateurs est sécurisé. Par exemple, vous joignez un document protégé à un e-mail.

Avant de partager des fichiers avec des personnes extérieures à votre organisation, contactez le support technique ou votre administrateur afin de savoir comment protéger des fichiers pour les utilisateurs externes.

Par exemple, si votre organisation communique régulièrement avec des personnes d’une autre organisation, votre administrateur peut avoir configuré des étiquettes qui définissent une protection permettant à ces personnes de lire et d’utiliser des documents protégés. Vous pouvez ensuite sélectionner ces étiquettes pour classifier et protéger les documents à partager.

Si les utilisateurs externes ont des [comptes B2B (Business-to-Business)](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) créés pour eux, vous pouvez également utiliser l' [Explorateur de fichiers pour définir des autorisations personnalisées](#using-file-explorer-to-classify-and-protect-files) pour un document avant de le partager. Si vous définissez vos propres autorisations personnalisées et que le document est déjà protégé pour une utilisation interne, commencez par en faire une copie afin de conserver les autorisations d’origine. Utilisez ensuite cette copie pour définir des autorisations personnalisées.


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Utilisation des applications Office pour classifier et protéger vos documents et vos e-mails

Dans l’onglet dossier de **démarrage** , sélectionnez le bouton **sensibilité** sur le ruban, puis sélectionnez l’une des étiquettes qui a été configurée pour vous. Par exemple :

![Exemple de bouton sensibilité](../media/sensitivity-not-set-callout.png)

Ou, si vous avez sélectionné **afficher la barre** à partir du bouton **sensibilité** , vous pouvez sélectionner une étiquette à partir de la barre de Azure information protection. Par exemple :

![Exemple de barre Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Pour définir une étiquette, par exemple «**confidentiel** \ **tous les employés**», sélectionnez **confidentiel** , puis **tous les employés**. Si vous ne savez pas quelle étiquette appliquer au document ou à l’e-mail actifs, utilisez les info-bulles pour en savoir plus sur chaque étiquette et sur le moment de l’appliquer.

Si une étiquette est déjà appliquée au document et que vous souhaitez la modifier, vous pouvez sélectionner une autre étiquette. Si vous avez affiché la barre de Azure Information Protection et que les étiquettes ne s’affichent pas dans la barre que vous sélectionnez, cliquez d’abord sur l’icône **modifier l’étiquette** , en regard de la valeur de l’étiquette active.

Outre la sélection manuelle, les étiquettes peuvent également être appliquées comme suit :

- Votre administrateur a configuré une étiquette par défaut, que vous pouvez conserver ou modifier.

- Votre administrateur a configuré des étiquettes à définir automatiquement lorsque des informations sensibles sont détectées.

- Votre administrateur a configuré des étiquettes recommandées lorsque des informations sensibles sont détectées, et vous êtes invité à accepter la recommandation (et l’étiquette est appliquée) ou à la rejeter (l’étiquette recommandée n’est pas appliquée).

### <a name="exceptions-for-the-sensitivity-button"></a>Exceptions pour le bouton de sensibilité

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Vous ne voyez pas le bouton sensibilité dans vos applications Office ?

- Vous n’avez peut-être pas [installé](install-unifiedlabelingclient-app.md)le client d’étiquetage unifié Azure information protection.

- Si vous ne voyez pas de bouton **sensibilité** sur le ruban, mais que vous voyez un bouton **protéger** avec des étiquettes à la place, le client Azure information protection (Classic) est installé et non le client d’étiquetage unifié Azure information protection. [Informations complémentaires](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>L’étiquette que vous souhaitez voir ne s’affiche pas dans la barre ? 

Raisons possibles :

- Si votre administrateur a récemment configuré une nouvelle étiquette pour vous, essayez de fermer toutes les instances de votre application Office, puis de la rouvrir. Cette action recherche les modifications apportées à vos étiquettes.

- Si l’étiquette manquante applique la protection, il est possible que vous disposiez d’une édition d’Office qui ne prend pas en charge l’application de la protection Rights Management. Pour vérifier, cliquez sur **sensibilité** > **aide et commentaires**. Dans la boîte de dialogue, vérifiez si vous avez un message dans la section **État du client** indiquant **Ce client n’est pas sous licence pour Office Professionnel Plus**. 
    
    Vous n’avez pas besoin d’Office Professionnel Plus si vous avez des applications Office d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est affectée à l’utilisateur.

- L’étiquette peut être dans une stratégie délimitée qui n’inclut pas votre compte. Contactez votre support technique ou votre administrateur.


### <a name="safely-sharing-by-email"></a>Partage sécurisé par e-mail

Quand vous partagez des documents Office par e-mail, vous pouvez attacher le document à un e-mail que vous protégez : le document est alors automatiquement protégé avec les mêmes restrictions que celles qui s’appliquent à l’e-mail. 

Toutefois, vous souhaiterez peut-être tout d’abord protéger le document, puis l’attacher à l’e-mail. Protégez également l’e-mail si son contenu présente des informations sensibles. L’avantage de protéger le document avant de l’attacher à un message électronique est que vous pouvez appliquer des autorisations différentes au document par rapport à l’e-mail.

## <a name="using-file-explorer-to-classify-and-protect-files"></a>Utilisation de l’Explorateur de fichiers pour classifier et protéger des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier et protéger un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour les options de classification et de protection que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement configurés avec ces options.

Lorsque vous utilisez l’Explorateur de fichiers pour classifier et protéger vos fichiers, si l’une ou plusieurs des étiquettes apparaissent estompées, les fichiers que vous avez sélectionnés ne prennent pas en charge la classification. Pour ces fichiers, vous pouvez sélectionner une étiquette uniquement si votre administrateur l’a configurée pour appliquer une protection. Ou bien, vous pouvez spécifier vos propres paramètres de protection. 

Certains fichiers sont automatiquement exclus de la classification et de la protection, car leur modification peut interrompre l’exécution de votre ordinateur. Bien que vous puissiez sélectionner ces fichiers, ils sont ignorés en tant que fichier ou dossier exclu. Exemples : des fichiers exécutables ou votre dossier Windows.

Le Guide de l’administrateur contient la liste complète des types de fichiers pris en charge, ainsi que les fichiers et dossiers qui sont automatiquement exclus : les [types de fichiers pris en charge par le client d’étiquetage unifié Azure information protection](clientv2-admin-guide-file-types.md).


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Pour classer et protéger un fichier à l’aide de l’Explorateur de fichiers

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**. Par exemple :
    
    ![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification et la protection comme les a effectuées votre administrateur. 

   - Si aucune des étiquettes ne peut être sélectionnée (elles apparaissent estompées) : le fichier sélectionné ne prend pas en charge la classification, mais vous pouvez le protéger avec des autorisations personnalisées (étape 3). Par exemple :

     ![Aucune étiquette n’est disponible dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. Vous pouvez spécifier vos propres paramètres de protection plutôt que d’utiliser les paramètres de protection que votre administrateur peut avoir inclus dans votre étiquette sélectionnée. Pour ce faire, sélectionnez **Protéger par des autorisations personnalisées**.
    
    Toute autorisation personnalisée que vous spécifiez remplace (plutôt que complète) les paramètres de protection que votre administrateur peut avoir définis pour l’étiquette de votre choix.  

4. Si vous avez sélectionné l’option d'autorisations personnalisées, spécifiez maintenant ce qui suit :

   - **Sélectionner des autorisations** : sélectionnez le niveau d’accès que vous voulez donner aux utilisateurs quand vous protégez les fichiers sélectionnés.
    
   - **Sélectionner des utilisateurs, des groupes ou des organisations** : spécifiez les personnes qui doivent disposer des autorisations que vous avez sélectionnées pour vos fichiers. Entrez leur adresse e-mail complète, une adresse e-mail de groupe ou un nom de domaine de l’organisation pour tous les utilisateurs appartenant à cette organisation. 
    
     Vous pouvez également utiliser l’icône de carnet d’adresses pour sélectionner des utilisateurs ou des groupes dans le carnet d’adresses Outlook.
        
    - Faire **expirer l’accès**: sélectionnez cette option uniquement pour les fichiers respectant le temps afin que les personnes que vous avez spécifiées ne puissent pas ouvrir le ou les fichiers sélectionnés après une date que vous avez définie. Vous pouvez toujours ouvrir le fichier d’origine mais, le jour spécifié, après minuit (dans votre fuseau horaire), les personnes que vous avez désignées ne pourront plus l’ouvrir.
    
     Notez que si ce paramètre a été précédemment configuré à l’aide des autorisations personnalisées à partir d’une application Office 2010, la date d’expiration spécifiée ne s’affiche pas dans cette boîte de dialogue, mais est toujours définie. Il s’agit seulement d’un problème d’affichage lorsque la date d’expiration a été configurée dans Office 2010.

5. Cliquez sur **Appliquer** et attendez le message **Tâche terminée** pour voir les résultats. Cliquez ensuite sur **Fermer**.

Les fichiers sélectionnés sont maintenant classifiés et protégés, conformément à vos sélections. Dans certains cas (quand l’ajout d’une protection modifie l’extension du nom du fichier), le fichier d’origine dans l’Explorateur de fichiers est remplacé par un nouveau fichier associé à l’icône de verrou d’Azure Information Protection. Par exemple :

![Fichier protégé avec une icône de verrou pour Azure Information Protection](../media/Pfile.png)

Si vous changez d’avis sur la classification et la protection, ou avez besoin de modifier vos paramètres, répétez simplement ce processus avec vos nouveaux paramètres.

La classification et la protection que vous avez spécifiées restent avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. 

## <a name="other-instructions"></a>Autres instructions
Pour plus d’informations sur les instructions du Guide de l’utilisateur pour Azure Information Protection client d’étiquetage unifiée, procédez comme suit :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    

Consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels).
