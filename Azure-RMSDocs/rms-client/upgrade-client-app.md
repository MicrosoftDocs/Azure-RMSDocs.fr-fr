---
title: "Tâches que vous aviez l’habitude d’effectuer avec l’application de partage RMS - AIP"
description: "Instructions pour les utilisateurs ayant effectué la mise à niveau de l’application de partage RMS vers le client Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 417294ff0890f2371909915a867fbdf56669e972
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2017
---
# <a name="tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Tâches que vous aviez l’habitude d’effectuer avec l’application de partage RMS

Vous avez récemment effectué la mise à niveau de l’application de partage Rights Management (également appelée « application de partage RMS ») vers le client Azure Information Protection ? 

Utilisez les informations suivantes pour être opérationnel rapidement.

|L’application de partage RMS|Comment procéder avec le client Azure Information Protection
|-----------|--------------------|
|Protéger un fichier sur un appareil <br /><br />Également appelé « protéger sur place »|Pour les applications Office : sélectionnez une étiquette qui applique la protection nécessaire ou définissez des autorisations personnalisées.<br /><br />Pour les autres fichiers : dans le menu Explorateur de fichiers, utilisez l’option **Classifier et protéger** pour ouvrir la boîte de dialogue **Classifier et protéger - Azure Information Protection**. Ensuite, sélectionnez une étiquette qui applique la protection nécessaire ou spécifiez vos propres autorisations personnalisées. <br /><br />Pour plus d’informations, voir [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md).
|Protéger un fichier que vous partagez par courrier électronique <br /><br />Également appelé « partage protégé »|Avec Outlook, appliquez une étiquette avec la protection requise à votre e-mail, ou sélectionnez l’option **Ne pas transférer** dans Outlook. Les pièces jointes non protégées qui ont un [type de fichier pris en charge](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sont protégées automatiquement.<br /><br />Remarque : Pour effectuer le suivi d’un document protégé que vous envoyez par e-mail, commencez par le protéger avant de l’attacher à l’e-mail.<br /><br />Pour plus d’informations, voir [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md).
|Modifier des autorisations sur les fichiers protégés <br /><br />Également appelé « reprotéger »|Pour les applications Office qui affichent la barre Azure Information Protection : sélectionnez une étiquette qui applique la protection nécessaire.<br /><br />Pour les autres fichiers, et si le client Azure Information Protection est en [mode protection uniquement](client-protection-only-mode.md) : utilisez l’option du menu Explorateur de fichiers **Classifier et protéger** pour ouvrir la boîte de dialogue **Classifier et protéger - Azure Information Protection**. Ensuite, sélectionnez une étiquette qui applique la protection nécessaire ou spécifiez vos propres autorisations personnalisées.<br /><br />Pour plus d’informations, voir [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md).
|Suivre et révoquer des documents|Pour les applications Office : ouvrez le document puis, cliquez sur l’onglet **Accueil** > groupe **Protection** > **Protéger** > **Suivre et révoquer**<br /><br />Depuis l’Explorateur de fichiers : cliquez avec le bouton droit sur un fichier ou dossier > **Classifier et protéger**. Ensuite, à partir de la boîte de dialogue **Classifier et protéger - Azure Information Protection**, cliquez sur **Suivre et révoquer**. <br /><br />Pour plus d’informations, consultez [Suivre et révoquer vos documents](client-track-revoke.md).
|Afficher et utiliser des fichiers protégés|Pour les documents Office protégés, Office doit être installé. La visionneuse Azure Information Protection peut ouvrir de nombreux autres fichiers protégés, vous permettant ainsi de les lire, les imprimer et les enregistrer si vous disposez des autorisations appropriées pour effectuer ces actions. Cette visionneuse est installée automatiquement avec le client, ou vous pouvez l’installer séparément.<br /><br />Pour plus d’informations, consultez [Ouvrir des fichiers protégés](client-view-use-files.md).
|Supprimer la protection des fichiers|Utilisez l’option de menu Explorateur de fichiers, **Classifier et protéger** pour ouvrir la boîte de dialogue **Classifier et protéger - Azure Information Protection**. <br /><br />Ensuite, dans le cas d’un seul fichier, désactivez l’option **Protéger avec des autorisations personnalisées**. Dans le cas de plusieurs fichiers ou d’un dossier, cliquez sur **Supprimer des autorisations personnalisées**.<br /><br />Pour plus d’informations, consultez [Supprimer des étiquettes et la protection des fichiers et e-mails](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>Vous ne trouvez pas l’option que vous recherchez ?

Si vous recherchez une option spécifique que vous utilisiez avec l’application de partage RMS, consultez le tableau suivant.

|Option dans l’application de partage RMS|Informations
|-----------|--------------------|
|**Partage protégé**|Cette option n’est plus disponible dans le ruban Office. Au lieu de partager directement à partir de votre application Office, utilisez l’option contextuelle de l’Explorateur de fichiers, **Classifier et protéger** pour protéger une copie du document avec des autorisations personnalisées, puis partagez le fichier à l’aide du client de messagerie de votre choix ou d’un emplacement de partage. <br /><br /> Vous pouvez également attacher un document non protégé à un e-mail que vous protégez : ce document est alors protégé automatiquement avec les mêmes restrictions. Vous ne pouvez cependant pas suivre ni révoquer ce document.
|**M’envoyer un e-mail quand quelqu’un tente d’ouvrir ces documents**|Utilisez le site de suivi des documents pour configurer vos paramètres de notification d’e-mail préférés : recherchez le document protégé que vous avez partagé > **Paramètres** > **Notifications d’e-mail**
|**M’autoriser à révoquer de suite l’accès à ces documents**|Cette option n’est plus disponible. Configurez des modèles qui n’autorisent pas l’accès hors connexion. En outre, déterminez si vous devez réduire la période de validité de la licence d’utilisation pour votre locataire, en exécutant [Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime).







[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
