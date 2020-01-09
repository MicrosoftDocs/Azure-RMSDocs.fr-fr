---
title: Classer à l’aide du client d’étiquetage unifié Azure Information Protection
description: Instructions sur la façon de classer vos documents et e-mails lorsque vous utilisez le client d’étiquetage unifié Azure Information Protection pour Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 975332c439530697d6460d2348531488d2b83e15
ms.sourcegitcommit: 40693000ce86110e14ffce3b553e42149d6b7dc2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2019
ms.locfileid: "75326590"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>Guide de l’utilisateur : classer un fichier ou un e-mail à l’aide du client d’étiquetage unifié Azure Information Protection pour Windows

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Utilisez ces instructions pour classifier (mais pas protéger) vos documents et e-mails. Si vous devez également protéger vos documents et e-mails, consultez les [instructions de classification et protection](clientv2-classify-protect.md). Si vous ne savez pas quel ensemble d’instructions utiliser, contactez votre administrateur ou votre support technique.

Le plus simple pour classifier vos documents et vos e-mails consiste à le faire quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Cependant, vous pouvez également classifier les fichiers à l’aide de l’**Explorateur de fichiers**. Cette méthode, qui prend en charge d’autres types de fichiers, est un moyen pratique de classifier plusieurs fichiers à la fois. 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Utilisation des applications Office pour classifier vos documents et vos e-mails

Dans l’onglet dossier de **démarrage** , sélectionnez le bouton **sensibilité** sur le ruban, puis sélectionnez l’une des étiquettes qui a été configurée pour vous. Exemple :

![Exemple de bouton sensibilité](../media/sensitivity-not-set-callout.png)

Ou, si vous avez sélectionné **afficher la barre** à partir du bouton **sensibilité** , vous pouvez sélectionner une étiquette à partir de la barre de Azure information protection. Exemple :

![Exemple de barre Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Pour définir une étiquette, par exemple « général », sélectionnez **général**. Si vous ne savez pas quelle étiquette appliquer au document ou à l’e-mail actifs, utilisez les info-bulles pour en savoir plus sur chaque étiquette et sur le moment de l’appliquer. 

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

- Si votre administrateur a récemment configuré une nouvelle étiquette pour vous, essayez de fermer toutes les instances de votre application Office, puis de la rouvrir. Cette action recherche les modifications apportées à vos étiquettes.

- L’étiquette peut être dans une stratégie délimitée qui n’inclut pas votre compte. Contactez votre support technique ou votre administrateur.


## <a name="using-file-explorer-to-classify-files"></a>Utilisation de l’Explorateur de fichiers pour classifier des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour la classification que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement classifiés.

Quand vous utilisez l’Explorateur de fichiers pour classifier vos fichiers, si l’une ou plusieurs des étiquettes apparaissent estompées, les fichiers que vous avez sélectionnés ne prennent pas en charge la classification sans également les protéger.

Le guide de l’administrateur contient la liste complète des types de fichiers qui prennent en charge la classification sans protection : [Types de fichiers pris en charge pour la classification seule](clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

### <a name="to-classify-a-file-by-using-file-explorer"></a>Pour classifier un fichier à l’aide de l’Explorateur de fichiers

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**. Exemple :
    
    ![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification comme l’a effectuée votre administrateur. 
    
    Si aucune des étiquettes n’est sélectionnable (elles apparaissent estompées) : le fichier sélectionné ne prend pas en charge la classification. Exemple :
    
    ![Aucune étiquette n’est disponible dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. Si vous avez sélectionné un fichier qui ne prend pas en charge la classification, cliquez sur **Fermer**. Vous ne pouvez pas classifier ce fichier sans également le protéger.
    
    Si vous avez sélectionné une étiquette, cliquez sur **Appliquer** et attendez que le message **Tâche terminée** s’affiche pour voir les résultats. Cliquez ensuite sur **Fermer**.

Si vous changez d’avis sur l’étiquette que vous avez choisie, répétez tout simplement ce processus et choisissez une autre étiquette.

La classification que vous avez spécifiée reste avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. 

## <a name="other-instructions"></a>Autres instructions

Autres instructions du Guide de l’utilisateur pour le Azure Information Protection client d’étiquetage unifié pour Windows :

- [Que voulez-vous faire ?](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs

Consultez [vue d’ensemble des étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels).

