---
title: Classer à l’aide du client d’étiquetage unifié Azure Information Protection
description: Instructions comment classer vos documents et e-mails lorsque vous utilisez Azure Information Protection unifiée étiquetage client pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: c7ec1c5f6a929d9b6b810b647e6cb6dbe3c42316
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767961"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>Guide de l’utilisateur : Classifier un fichier ou un e-mail en utilisant le client d’étiquetage unifié Azure Information Protection pour Windows

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Utilisez ces instructions pour classifier (mais pas protéger) vos documents et e-mails. Si vous devez également protéger vos documents et e-mails, consultez les [instructions de classification et protection](clientv2-classify-protect.md). Si vous ne savez pas quel ensemble d’instructions utiliser, contactez votre administrateur ou votre support technique.

La façon la plus simple de classifier vos documents et vos e-mails consiste à le faire quand vous les créez ou que vous les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Cependant, vous pouvez également classifier les fichiers à l’aide de l’**Explorateur de fichiers**. Cette méthode, qui prend en charge d’autres types de fichiers, est un moyen pratique de classifier plusieurs fichiers à la fois. 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Utilisation des applications Office pour classifier vos documents et vos e-mails

À partir de la **accueil** onglet, sélectionnez le **sensibilité** bouton sur le ruban, puis sélectionnez une des étiquettes qui a été configurée pour vous. Exemple :

![Exemple de bouton de sensibilité](../media/sensitivity-not-set-callout.png)

Ou, si vous avez sélectionné **afficher la barre** à partir de la **sensibilité** bouton, vous pouvez sélectionner une étiquette à partir de la barre Azure Information Protection. Exemple :

![Exemple de barre Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Pour définir une étiquette, comme « Général », sélectionnez **général**. Si vous ne savez pas quelle étiquette appliquer au document ou à l’e-mail actifs, utilisez les info-bulles pour en savoir plus sur chaque étiquette et sur le moment de l’appliquer. 

Si une étiquette est déjà appliquée au document et que vous souhaitez la modifier, vous pouvez sélectionner une autre étiquette. Si vous avez affiché la barre Azure Information Protection, et les étiquettes ne sont pas affichées dans la barre pour sélectionner, cliquez d’abord sur le **modifier l’étiquette** icône, en regard de la valeur actuelle de l’étiquette.

Outre la sélection manuelle, les étiquettes peuvent également être appliquées comme suit :

- Votre administrateur a configuré une étiquette par défaut, que vous pouvez conserver ou modifier.

- Votre administrateur a configuré les étiquettes à définir automatiquement lors de la détection des informations sensibles.

- Votre administrateur a configuré recommandé des étiquettes lorsque des informations sensibles sont détectées et vous êtes invité à accepter la recommandation (et l’étiquette est appliquée), ou la rejeter (l’étiquette recommandée n’est pas appliqué).

### <a name="exceptions-for-the-sensitivity-button"></a>Exceptions pour le bouton de sensibilité

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Ne voyez pas le bouton de sensibilité dans vos applications Office ?

- Vous ne disposez pas de client Azure Information Protection unifié étiquetage [installé](install-unifiedlabelingclient-app.md).

- Si vous ne voyez pas un **sensibilité** bouton sur le ruban, mais apparaissent un **protéger** bouton avec des étiquettes au lieu de cela, vous avez le client Azure Information Protection est installé et pas Azure Information Protection client d’étiquetage unifié. [Plus d’informations](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>L’étiquette que vous souhaitez voir ne s’affiche pas dans la barre ? 

- Si votre administrateur a récemment configuré une nouvelle étiquette pour vous, essayez de fermer toutes les instances de votre application Office, puis de la rouvrir. Cette action recherche les modifications apportées à vos étiquettes.

- L’étiquette peut être dans une stratégie délimitée qui n’inclut pas votre compte. Contactez votre support technique ou votre administrateur.


## <a name="using-file-explorer-to-classify-files"></a>Utilisation de l’Explorateur de fichiers pour classifier des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour la classification que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement classifiés.

Quand vous utilisez l’Explorateur de fichiers pour classifier vos fichiers, si l’une ou plusieurs des étiquettes apparaissent estompées, les fichiers que vous avez sélectionnés ne prennent pas en charge la classification sans également les protéger.

Le guide de l’administrateur contient la liste complète des types de fichiers qui prennent en charge la classification sans protection : [Types de fichiers pris en charge pour la classification uniquement](clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

### <a name="to-classify-a-file-by-using-file-explorer"></a>Pour classifier un fichier à l’aide de l’Explorateur de fichiers

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**. Exemple :
    
    ![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification comme l’a effectuée votre administrateur. 
    
    Si aucune des étiquettes ne peut être sélectionnée (elles apparaissent estompées) : Le fichier sélectionné ne prend pas en charge la classification. Exemple :
    
    ![Aucune étiquette n’est disponible dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. Si vous avez sélectionné un fichier qui ne prend pas en charge la classification, cliquez sur **Fermer**. Vous ne pouvez pas classifier ce fichier sans également le protéger.
    
    Si vous avez sélectionné une étiquette, cliquez sur **Appliquer** et attendez que le message **Tâche terminée** s’affiche pour voir les résultats. Cliquez ensuite sur **Fermer**.

Si vous changez d’avis sur l’étiquette que vous avez choisie, répétez tout simplement ce processus et choisissez une autre étiquette.

La classification que vous avez spécifiée reste avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. 

## <a name="other-instructions"></a>Autres instructions

Guident de plus d’instructions pratiques à partir de l’utilisateur pour le client d’étiquetage unifié d’Azure Information Protection pour Windows :

- [Que voulez-vous faire ?](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs

Consultez [vue d’ensemble des étiquettes de sensibilité](/Office365/SecurityCompliance/sensitivity-labels).

