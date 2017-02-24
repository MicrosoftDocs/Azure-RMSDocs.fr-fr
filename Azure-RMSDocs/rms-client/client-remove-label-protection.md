---
title: "Supprimer des étiquettes de classification et la protection des fichiers et des e-mails | Azure Information Protection"
description: "Instructions pour supprimer des étiquettes de classification et la protection des fichiers qui ont été étiquetés par Azure Information Protection ou protégés par Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0a720ab08596964ed04fdc800ce55f3932a7cc0f
ms.openlocfilehash: fc401131a11426a17be4417d049199fb1c1a8f68


---

# <a name="remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>Supprimer des étiquettes et la protection des fichiers et des e-mails qui ont été étiquetés par Azure Information Protection ou protégés par Rights Management

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

Lorsque le [client Azure Information Protection est installé sur votre ordinateur](install-client-app.md), vous pouvez supprimer des étiquettes de classification et la protection de fichiers et messages électroniques.

Lorsque l’étiquette que vous supprimez est configurée pour appliquer la protection, cette action supprime également la protection du fichier. Vous pouvez être invité à expliquer la raison pour laquelle vous avez supprimé l’étiquette.

> [!IMPORTANT]
> Vous devez être le propriétaire du fichier pour supprimer la protection, ou avoir reçu des autorisations pour supprimer la protection (autorisation d’extraction ou de contrôle total Rights Management).

Si vous souhaitez choisir une autre étiquette ou un autre jeu de paramètres de protection, il est inutile de supprimer l’étiquette ou la protection. Choisissez plutôt une nouvelle étiquette et si nécessaire, définissez des autorisations personnalisées. 

Vous pouvez supprimer des étiquettes et des protections des documents Office quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Vous pouvez également supprimer les étiquettes et la protection à l’aide de l’**Explorateur de fichiers**, qui prend en charge des types de fichiers supplémentaires et constitue un moyen pratique de supprimer les étiquettes et la protection de plusieurs fichiers à la fois.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Utilisation des applications Office pour supprimer les étiquettes et la protection des documents et des e-mails

Dans la barre Information Protection, cliquez sur l’icône **Supprimer l’étiquette** :

![Barre Azure Information Protection : supprimer l’étiquette](../media/delete-label.png)

Si l’icône **Supprimer l’étiquette** n’est pas immédiatement disponible, cliquez d’abord sur l’icône **Modifier l’étiquette** :

![Barre Azure Information Protection : modifier l’étiquette](../media/edit-label.png)

> [!NOTE]
> Si vous ne voyez pas cette barre Information Protection dans vos applications Office :
> 
> - Le client Azure Information Protection n’est pas [installé](install-client-app.md), ou le client est en cours d’exécution en [mode Protection uniquement](client-protection-only-mode.md).

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Utilisation de l’Explorateur de fichiers pour supprimer des étiquettes et la protection des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement supprimer les étiquettes et les protections d’un seul fichier, de plusieurs fichiers ou d’un dossier. Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés. 

1.  Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**.

2. Pour supprimer une étiquette : dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, sélectionnez **Supprimer l’étiquette**. Si l’étiquette a été configurée pour appliquer la protection, cette protection est automatiquement supprimée.

3. Pour supprimer la protection personnalisée d’un seul fichier : dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, désactivez l’option **Protéger avec des autorisations personnalisées**.
    
4. Pour supprimer la protection personnalisée de plusieurs fichiers : dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, cliquez sur **Supprimer les autorisations personnalisées**.

5. Cliquez sur **Appliquer** et attendez le message **Tâche terminée** pour voir les résultats. Cliquez ensuite sur **Fermer**.


## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


