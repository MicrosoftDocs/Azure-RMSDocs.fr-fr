---
title: Supprimer des étiquettes Azure Information Protection
description: Instructions pour supprimer des étiquettes de classification et la protection des fichiers qui ont été étiquetés par Azure Information Protection ou protégés par Rights Management.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 09173541f4d332750457a488d7edb97ec7f4319c
ms.sourcegitcommit: 03dc2eb973b20897b30659c2ac6cb43ce0a40e71
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2020
ms.locfileid: "75960275"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>Guide de l’utilisateur : Supprimer des étiquettes et retirer la protection des fichiers et e-mails étiquetés par Azure Information Protection ou protégés par Rights Management

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8*
>
> *Instructions pour : [Azure information protection client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Lorsque le [client Azure Information Protection est installé sur votre ordinateur](install-client-app.md), vous pouvez supprimer des étiquettes de classification et la protection de fichiers et messages électroniques.

Lorsque l’étiquette que vous supprimez est configurée pour appliquer la protection, cette action supprime également la protection du fichier. Vous pouvez être invité à expliquer la raison pour laquelle vous avez supprimé l’étiquette.

> [!IMPORTANT]
> Vous devez être le propriétaire du fichier pour supprimer la protection, ou avoir reçu des autorisations pour supprimer la protection (autorisation **d’extraction** ou de **contrôle total** Rights Management).

Si vous souhaitez choisir une autre étiquette ou un autre jeu de paramètres de protection, il est inutile de supprimer l’étiquette ou la protection. Choisissez plutôt une nouvelle étiquette et si nécessaire, définissez des autorisations personnalisées si votre administrateur autorise cette configuration. 

Vous pouvez supprimer des étiquettes et des protections des documents Office quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Vous pouvez également supprimer les étiquettes et la protection à l’aide de l’**Explorateur de fichiers**, qui prend en charge des types de fichiers supplémentaires et constitue un moyen pratique de supprimer les étiquettes et la protection de plusieurs fichiers à la fois.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Utilisation des applications Office pour supprimer les étiquettes et la protection des documents et des e-mails

Dans la barre Information Protection, cliquez sur l’icône **Supprimer l’étiquette** :

![Barre Azure Information Protection : supprimer l’étiquette](../media/delete-label.png)

Si l’icône **Supprimer l’étiquette** n’est pas immédiatement disponible, cliquez d’abord sur l’icône **Modifier l’étiquette** :

![Barre Azure Information Protection : modifier l’étiquette](../media/edit-label.png)

Si vous ne voyez toujours pas l’icône **supprimer une étiquette** , votre administrateur ne vous autorise pas à utiliser cette option, car tous les documents et e-mails doivent avoir une étiquette.

> [!NOTE]
> Si vous ne voyez pas cette barre Information Protection dans vos applications Office :
>
> - Si vous voyez un bouton **Protéger** sur le ruban, sélectionnez **Protéger**, puis sélectionnez **Afficher la barre**.
> 
> - Le client Azure Information Protection n’est pas [installé](install-client-app.md), ou le client est en cours d’exécution en [mode Protection uniquement](client-protection-only-mode.md).

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Utilisation de l’Explorateur de fichiers pour supprimer des étiquettes et la protection des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement supprimer les étiquettes et les protections d’un seul fichier, de plusieurs fichiers ou d’un dossier. Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés. 

1. Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger**.

2. Pour supprimer une étiquette : dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, sélectionnez **Supprimer l’étiquette**. Si l’étiquette a été configurée pour appliquer la protection, cette protection est automatiquement supprimée.

3. Pour supprimer la protection personnalisée d’un seul fichier : dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, désactivez l’option **Protéger avec des autorisations personnalisées**. 
    
    Si vous ne voyez pas l’option **Protéger par des autorisations personnalisées**, votre administrateur ne vous permet pas d’utiliser cette option.
    
4. Pour supprimer la protection personnalisée de plusieurs fichiers : dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, cliquez sur **Supprimer les autorisations personnalisées**.
    
    Si vous ne voyez pas l’option **Supprimer les autorisations personnalisées**, votre administrateur ne vous permet pas d’utiliser cette option.

5. Cliquez sur **Appliquer** et attendez le message **Tâche terminée** pour voir les résultats. Cliquez ensuite sur **Fermer**.


## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    
Pour des instructions de configuration permettant d’activer le paramètre de stratégie **Rendre l’option des autorisations personnalisées disponible aux utilisateurs**, consultez [Configuration des paramètres de stratégie Azure Information Protection](../configure-policy-settings.md).

Autres instructions de configuration : [Configuration de la stratégie Azure Information Protection](../configure-policy.md).

