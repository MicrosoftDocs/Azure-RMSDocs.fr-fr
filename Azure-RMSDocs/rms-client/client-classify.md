---
title: Classifier des fichiers et e-mails avec Azure Information Protection
description: Instructions sur la classification de vos documents et e-mails.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/06/2017
ms.topic: article
ms.service: information-protection
ms.assetid: d65c7690-fab7-4823-845c-8c73903e9c79
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: a7c92c85dafd11c5bd3cfb6ae16a0f62d34b6e53
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42807876"
---
# <a name="user-guide-classify-a-file-or-email-by-using-azure-information-protection"></a>Guide de l’utilisateur : Classifier un fichier ou un e-mail avec Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

> [!NOTE]
> Utilisez ces instructions pour classifier (mais pas protéger) vos documents et e-mails. Si vous devez également protéger vos documents et e-mails, consultez les [instructions de classification et protection](client-classify-protect.md). Si vous ne savez pas quel ensemble d’instructions utiliser, contactez votre administrateur ou votre support technique.

Le plus simple pour classifier vos documents et vos e-mails consiste à le faire quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Cependant, vous pouvez également classifier les fichiers à l’aide de l’**Explorateur de fichiers**. Cette méthode, qui prend en charge d’autres types de fichiers, est un moyen pratique de classifier plusieurs fichiers à la fois. 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Utilisation des applications Office pour classifier vos documents et vos e-mails

Utilisez la barre Azure Information Protection et sélectionnez une des étiquettes qui a été configurée pour vous. 

Par exemple, l’image suivante montre que le document n’a pas encore été étiqueté, car la **Sensibilité** affiche **Non défini**. Pour définir une étiquette, comme « Général », cliquez sur **Général**. Si vous ne savez pas quelle étiquette appliquer au document ou à l’e-mail actifs, utilisez les info-bulles pour en savoir plus sur chaque étiquette et sur le moment de l’appliquer. 

![Exemple de barre Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Si une étiquette est déjà appliquée au document et que vous souhaitez la modifier, vous pouvez sélectionner une autre étiquette. Si les étiquettes ne sont pas affichées dans la barre, cliquez d’abord sur l’icône **Modifier l’étiquette**, en regard de la valeur actuelle de l’étiquette.

> [!TIP]
> Vous pouvez également sélectionner des étiquettes à l’aide du bouton **Protéger** sous l’onglet **Fichier**.

Outre la sélection manuelle, les étiquettes peuvent également être appliquées comme suit :

- Votre administrateur a configuré une étiquette par défaut, que vous pouvez conserver ou modifier.

- Votre administrateur a configuré recommandé des invites pour sélectionner une étiquette spécifique lorsque des données sensibles sont détectées. Vous pouvez accepter la recommandation (et l’étiquette est appliquée), ou la rejeter (l’étiquette recommandée n’est pas appliquée).

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Exceptions de la barre Azure Information Protection 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>Vous ne voyez pas cette barre Information Protection dans vos applications Office ?

- Le client Azure Information Protection n’est peut-être pas [installé](install-client-app.md).

- Le client est installé, mais votre administrateur a configuré un paramètre qui n’affiche pas la barre. Sélectionnez plutôt des étiquettes en utilisant le bouton **Protéger** sous l’onglet **Fichier** dans le ruban Office. 

##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>L’étiquette que vous souhaitez voir ne s’affiche pas dans la barre ? 

- Si votre administrateur a récemment configuré une nouvelle étiquette pour vous, essayez de fermer toutes les instances de votre application Office, puis de la rouvrir. Cette action recherche les modifications apportées à vos étiquettes.

- L’étiquette peut être dans une stratégie délimitée qui n’inclut pas votre compte. Contactez votre support technique ou votre administrateur.


## <a name="using-file-explorer-to-classify-files"></a>Utilisation de l’Explorateur de fichiers pour classifier des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour la classification que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement classifiés.

Quand vous utilisez l’Explorateur de fichiers pour classifier vos fichiers, si l’une ou plusieurs des étiquettes apparaissent estompées, les fichiers que vous avez sélectionnés ne prennent pas en charge la classification sans également les protéger.

Le guide de l’administrateur contient la liste complète des types de fichiers qui prennent en charge la classification sans protection : [Types de fichiers pris en charge pour la classification seule](client-admin-guide-file-types.md#file-types-supported-for-classification-only).

### <a name="to-classify-a-file-by-using-file-explorer"></a>Pour classifier un fichier à l’aide de l’Explorateur de fichiers

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**. Par exemple :
    
    ![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification comme l’a effectuée votre administrateur. 
    
    Si aucune des étiquettes n’est sélectionnable (elles apparaissent estompées) : le fichier sélectionné ne prend pas en charge la classification. Par exemple :
    
    ![Aucune étiquette n’est disponible dans la boîte de dialogue Classifier et protéger - Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)

3. Si vous avez sélectionné un fichier qui ne prend pas en charge la classification, cliquez sur **Fermer**. Vous ne pouvez pas classifier ce fichier sans également le protéger.
    
    Si vous avez sélectionné une étiquette, cliquez sur **Appliquer** et attendez que le message **Tâche terminée** s’affiche pour voir les résultats. Cliquez ensuite sur **Fermer**.

Si vous changez d’avis sur l’étiquette que vous avez choisie, répétez tout simplement ce processus et choisissez une autre étiquette.

La classification que vous avez spécifiée reste avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. 
## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    
Consultez [Configuration de la stratégie Azure Information Protection](../configure-policy.md).

