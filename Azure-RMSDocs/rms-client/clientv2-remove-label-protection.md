---
title: Supprimer des étiquettes à l’aide du client d’étiquetage unifié Azure Information Protection
description: Instructions pour supprimer les étiquettes de sensibilité et la protection des fichiers et des e-mails à l’aide du client d’étiquetage unifié Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 9ca9c53a71e0ef1881b16a1a653bbddf24b042be
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793197"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>Guide de l’utilisateur : Supprimer les étiquettes et la protection des fichiers et des e-mails qui ont été étiquetés par Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*
>
> *Instructions pour : [Azure Information Protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Lorsque le Azure Information Protection client unifié est [installé sur votre ordinateur](install-client-app.md), vous pouvez supprimer les étiquettes de sensibilité et la protection des fichiers et des e-mails.

Lorsque l’étiquette de sensibilité que vous supprimez est configurée pour appliquer la protection, cette action supprime également la protection du fichier. Vous pouvez être invité à expliquer la raison pour laquelle vous avez supprimé l’étiquette.

> [!IMPORTANT]
> Vous devez être le propriétaire du fichier pour supprimer la protection, ou avoir reçu des autorisations pour supprimer la protection (autorisation **d’extraction** ou de **contrôle total** Rights Management).

Si vous souhaitez choisir une autre étiquette ou un autre jeu de paramètres de protection, il est inutile de supprimer l’étiquette ou la protection. Au lieu de cela, choisissez une nouvelle étiquette et, si nécessaire, vous pouvez définir des autorisations personnalisées à l’aide de l’Explorateur de fichiers. 

Vous pouvez supprimer des étiquettes et des protections des documents Office quand vous les créez ou que vous les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Vous pouvez également supprimer les étiquettes et la protection à l’aide de l’**Explorateur de fichiers**, qui prend en charge des types de fichiers supplémentaires et constitue un moyen pratique de supprimer les étiquettes et la protection de plusieurs fichiers à la fois.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Utilisation des applications Office pour supprimer les étiquettes et la protection des documents et des e-mails

Dans l’onglet dossier de **démarrage** , sélectionnez le bouton **sensibilité** sur le ruban et désactivez l’étiquette actuellement sélectionnée.

Ou, si vous avez sélectionné **afficher la barre** à partir du bouton **sensibilité** , vous pouvez sélectionner l’icône **Supprimer l’étiquette** dans la barre de Azure information protection:

![Barre Azure Information Protection : supprimer l’étiquette](../media/v2delete-label.png)

Si l’icône **Supprimer l’étiquette** n’est pas immédiatement disponible, sélectionnez d’abord l’icône modifier l' **étiquette** :

![Barre Azure Information Protection : modifier l’étiquette](../media/v2edit-label.png)

Si vous ne voyez toujours pas l’icône **supprimer une étiquette** , votre administrateur ne vous autorise pas à utiliser cette option, car tous les documents et e-mails doivent avoir une étiquette.

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Utilisation de l’Explorateur de fichiers pour supprimer des étiquettes et la protection des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement supprimer les étiquettes et les protections d’un seul fichier, de plusieurs fichiers ou d’un dossier. Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés. 

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**.

2. Pour supprimer une étiquette : Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, sélectionnez **Supprimer l’étiquette**. Si l’étiquette a été configurée pour appliquer la protection, cette protection est automatiquement supprimée.

3. Pour supprimer la protection personnalisée d’un seul fichier : Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, désactivez l’option **Protéger avec des autorisations personnalisées**. 

4. Pour supprimer la protection personnalisée de plusieurs fichiers : Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, cliquez sur **Supprimer les autorisations personnalisées**.

5. Cliquez sur **Appliquer** et attendez le message **Tâche terminée** pour voir les résultats. Cliquez ensuite sur **Fermer**.


## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    

Consultez [vue d’ensemble des étiquettes de sensibilité](/Office365/SecurityCompliance/sensitivity-labels).

