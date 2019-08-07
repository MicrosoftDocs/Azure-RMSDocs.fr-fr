---
title: Tâches que vous aviez l’habitude d’effectuer avec l’application de partage RMS - AIP
description: Instructions pour les utilisateurs ayant effectué la mise à niveau de l’application de partage RMS vers le client Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: afa2679bc808e8ee536d5f66bc5cf28de5a6ff7d
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68789835"
---
# <a name="user-guide-tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Guide de l’utilisateur : Tâches que vous aviez l’habitude d’effectuer avec l’application de partage RMS

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Vous avez récemment effectué la mise à niveau de l’application de partage Rights Management (également appelée « application de partage RMS ») vers le client Azure Information Protection ? 

Utilisez les informations suivantes pour être opérationnel rapidement.

|L’application de partage RMS|Comment procéder avec le client Azure Information Protection
|-----------|--------------------|
|Protéger un fichier sur un appareil <br /><br />Également appelé « protéger sur place »|Pour les applications Office : Sélectionnez une étiquette qui applique la protection nécessaire ou définissez des autorisations personnalisées.<br /><br />Pour les autres fichiers : Utilisez l’option de menu Explorateur de fichiers, **Classifier et protéger** pour ouvrir la boîte de dialogue **Classifier et protéger - Azure Information Protection**. Ensuite, sélectionnez une étiquette qui applique la protection nécessaire ou spécifiez vos propres autorisations personnalisées. <br /><br />Pour plus d’informations, voir [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md).
|Protéger un fichier partagé par courrier électronique <br /><br />Également appelé « partage protégé »|Avec Outlook, appliquez une étiquette avec la protection requise à votre e-mail, ou sélectionnez l’option **Ne pas transférer** dans Outlook. Les pièces jointes non protégées qui ont un [type de fichier pris en charge](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sont protégées automatiquement.<br /><br />Remarque : Pour effectuer le suivi d’un document protégé que vous envoyez par e-mail, commencez par le protéger avant de l’attacher à l’e-mail.<br /><br />Pour plus d’informations, voir [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md).
|Modifier des autorisations sur les fichiers protégés <br /><br />Également appelé « reprotéger »|Dans les applications Office qui affichent la barre Azure Information Protection : Sélectionnez une étiquette qui applique la protection nécessaire.<br /><br />Pour les autres fichiers, et si le client Azure Information Protection est en [mode protection uniquement](client-protection-only-mode.md) : Utilisez l’option de menu Explorateur de fichiers, **Classifier et protéger** pour ouvrir la boîte de dialogue **Classifier et protéger - Azure Information Protection**. Ensuite, sélectionnez une étiquette qui applique la protection nécessaire ou spécifiez vos propres autorisations personnalisées.<br /><br />Pour plus d’informations, voir [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md).
|Suivre et révoquer des documents|Dans Word, Excel et PowerPoint : Ouvrez le document, puis cliquez sur l’onglet **Accueil** > Groupe **Protection** > **Protéger** > **Suivre et révoquer**<br /><br />Depuis l’Explorateur de fichiers : Cliquez avec le bouton droit sur un fichier ou un dossier > **Classifier et protéger**. Ensuite, à partir de la boîte de dialogue **Classifier et protéger - Azure Information Protection**, cliquez sur **Suivre et révoquer**. <br /><br />Lorsque vous utilisez PowerShell pour le client Azure Information Protection: Utilisez le paramètre *EnableTracking* avec la cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) pour inscrire le document étiqueté pour le suivi.<br /><br />Pour plus d’informations, consultez [Suivre et révoquer vos documents](client-track-revoke.md).
|Afficher et utiliser les fichiers qui ont été protégés|Pour les documents Office protégés, Office doit être installé. La visionneuse Azure Information Protection peut ouvrir de nombreux autres fichiers protégés, vous permettant ainsi de les lire, les imprimer et les enregistrer si vous disposez des autorisations appropriées pour effectuer ces actions. Cette visionneuse est installée automatiquement avec le client, ou vous pouvez l’installer séparément.<br /><br />Pour plus d’informations, consultez [Ouvrir des fichiers protégés](client-view-use-files.md).
|Supprimer la protection des fichiers|Utilisez l’option de menu Explorateur de fichiers, **Classifier et protéger** pour ouvrir la boîte de dialogue **Classifier et protéger - Azure Information Protection**. <br /><br />Ensuite, dans le cas d’un seul fichier, désactivez l’option **Protéger avec des autorisations personnalisées**. Dans le cas de plusieurs fichiers ou d’un dossier, cliquez sur **Supprimer des autorisations personnalisées**.<br /><br />Pour plus d’informations, consultez [Supprimer des étiquettes et la protection des fichiers et e-mails](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>Vous ne trouvez pas l’option que vous recherchez ?

Si vous recherchez une option spécifique que vous utilisiez avec l’application de partage RMS, consultez le tableau suivant.

|Option dans l’application de partage RMS|Information
|-----------|--------------------|
|**Partage protégé**|Cette option n’est plus disponible dans le ruban Office. Au lieu de partager directement à partir de votre application Office, utilisez l’option contextuelle de l’Explorateur de fichiers, **Classifier et protéger** pour protéger une copie du document avec des autorisations personnalisées, puis partagez le fichier à l’aide du client de messagerie de votre choix ou d’un emplacement de partage. <br /><br /> Vous pouvez également attacher un document Office non protégé à un e-mail que vous protégez : ce document est alors protégé automatiquement avec les mêmes restrictions. Vous ne pouvez cependant pas suivre ni révoquer ce document.
|**M’envoyer un e-mail quand quelqu’un tente d’ouvrir ces documents**|Utilisez le site de suivi de document pour configurer les paramètres de notification de votre messagerie préférée : Recherchez le document protégé que vous avez partagé > **Paramètres** > **Notifications par e-mail**
|**M’autoriser à révoquer de suite l’accès à ces documents**|Cette option n’est plus disponible. Utilisez les paramètres de protection définis par l’administrateur qui n’autorisent pas l’accès hors connexion. En outre, un administrateur peut réduire la période de validité de la licence d’utilisation pour votre locataire, en exécutant [Set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime).
|**Effectuer le suivi de l’utilisation** dans Outlook|La possibilité d’accéder au site de suivi des documents à partir d’Outlook n’est plus disponible. Au lieu de cela, utilisez l’option **Suivre et révoquer** à partir de Word, PowerPoint, Excel ou l’Explorateur de fichiers. Ou, à l’aide d’un navigateur, vous pouvez accéder directement au [site de suivi des documents](https://go.microsoft.com/fwlink/?LinkId=529562).

## <a name="next-steps"></a>Étapes suivantes
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informations supplémentaires pour les administrateurs    
Consultez le [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md).

  
