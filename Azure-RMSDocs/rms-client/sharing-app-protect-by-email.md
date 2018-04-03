---
title: Partager des documents protégés avec l’application de partage RMS - AIP
description: Instructions à suivre pour partager un document par e-mail en toute sécurité.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4c1cd1d3-78dd-4f90-8b37-dcc9205a6736
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 71bc303aaadf6856cce2f63db0acf5280fbe172b
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="protect-a-file-that-you-share-by-email-by-using-the-rights-management-sharing-application"></a>Protégez un fichier partagé par courrier électronique à l’aide de l’application de partage Rights Management

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Lorsque vous protégez un fichier que vous le partagez par e-mail, il crée une nouvelle version du fichier d’origine. Le fichier d’origine reste non protégé et la nouvelle version est protégée et automatiquement jointe à un e-mail que vous envoyez ensuite.

Dans certains cas (pour les fichiers créés par Microsoft Word, Excel et PowerPoint), l’application de partage RMS crée deux versions du fichier et les joint au message. La deuxième version du fichier est dotée d’une extension **.ppdf** et il est un cliché instantané PDF du fichier. Cette version du fichier garantit que les destinataires peuvent toujours lire le fichier, même s’ils n’ont pas l’application que vous avez utilisée pour le créer. Cela est souvent le cas quand vous lisez vos e-mails sur un appareil mobile et que vous souhaitez afficher les pièces jointes. Pour ouvrir le fichier, vous avez simplement besoin de l’application de partage RMS. Vous pouvez ensuite lire le fichier joint, mais vous ne pourrez pas le modifier sans ouvrir l’autre version du fichier dans l’application prenant en charge un service Rights Management.

Si votre organisation utilise Azure Information Protection, vous pouvez effectuer le suivi de vos fichiers grâce au partage :

-   Sélectionnez une option pour recevoir des e-mails lorsque quelqu’un tente d’ouvrir ces pièces jointes protégées. Chaque fois que quelqu’un accède au fichier, vous recevrez une notification vous indiquant qui a tenté d’ouvrir le fichier et à quel moment, et si cette personne a réussi ou non (elle a bien été authentifiée).

-   Utilisez le site de suivi de la documentation. Vous pouvez même cesser de partager le fichier en supprimant l’accès à ce dernier sur le site de suivi de document. Pour plus d’informations, consultez [Suivre et révoquer vos documents lorsque vous utilisez l’application de partage RMS](sharing-app-track-revoke.md).

## <a name="using-outlook-to-protect-a-file-that-you-share-by-email"></a>Avec Outlook : Pour protéger un fichier partagé par e-mail

1.  Créez votre e-mail et joignez le fichier. Puis, dans l’onglet **Message** du groupe **RMS** , cliquez sur **Partage protégé** , puis sur **Partage protégé** à nouveau :

    ![Complément Outlook pour l'application de partage RMS](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    Si vous ne voyez pas ce bouton, il est probable que l’application de partage RMS ne soit pas installée sur votre ordinateur, que la version la plus récente ne soit pas installée ou que votre ordinateur doive être redémarré pour terminer l’installation. Pour plus d’informations sur l’installation de l’application de partage, consultez [Télécharger et installer l’application de partage Rights Management](install-sharing-app.md).

2.  Spécifiez les options souhaitées pour ce fichier dans la [boîte de dialogue Partage protégé](sharing-app-dialog-box.md), puis cliquez sur **Envoyer maintenant**.

### <a name="other-ways-to-protect-a-file-that-you-share-by-email"></a>Autres méthodes pour protéger un fichier partagé par e-mail
En plus de partager un fichier protégé à l’aide d’Outlook, vous pouvez également utiliser ces alternatives :

-   Depuis l’Explorateur de fichiers : Cette méthode fonctionne pour tous les fichiers.

-   À partir d’une application Office : cette méthode fonctionnant pour les applications prises en charge par l’application de partage RMS à l’aide du complément Office, le groupe **RMS** apparaît sur le ruban.

#### <a name="using-file-explorer-or-an-office-application-to-protect-a-file-that-you-share-by-email"></a>Avec l’Explorateur de fichiers ou une application Office : Pour protéger un fichier partagé par e-mail

1.  Utilisez l’une des options suivantes :

    -   Pour l’Explorateur de fichiers : cliquez avec le bouton droit sur le fichier, sélectionnez **Protéger avec RMS**, puis **Partage protégé** :

        ![Option de menu Partage protégé](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   Pour les applications Office, Word, Excel et PowerPoint : Assurez-vous d’abord d’avoir enregistré le fichier. Puis, dans l’onglet **Accueil** du groupe **RMS** , cliquez sur **Partage protégé** puis sur **Partage protégé** à nouveau :

        ![Complément de barre d'outils Office](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    Si vous ne voyez pas ces options de protection, il est probable que l’application de partage RMS ne soit pas installée sur votre ordinateur, que la version la plus récente ne soit pas installée ou que votre ordinateur doive être redémarré pour terminer l’installation. Pour plus d’informations sur l’installation de l’application de partage, consultez [Télécharger et installer l’application de partage Rights Management](install-sharing-app.md).

2.  Spécifiez les options souhaitées pour ce fichier dans la [boîte de dialogue Partage protégé](sharing-app-dialog-box.md), puis cliquez sur **Envoyer**.

3.  Il se peut qu’une boîte de dialogue s’affiche brièvement pour vous informer que le fichier est protégé et un e-mail spécialement créé pour vous pour indiquer aux destinataires que les pièces jointes sont protégées avec Microsoft RMS et qu’ils doivent se connecter. Lorsqu’ils cliquent sur le lien pour se connecter, ils voient des instructions et des liens pour pouvoir ouvrir vos pièces jointes protégées.

    Exemple :

    ![E-mail pour Azure Information Protection](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    Vous vous demandez : [qu’est-ce que le fichier .ppdf créé automatiquement ?](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)

4.  Facultatif : Vous pouvez modifier n’importe quel élément de cet e-mail. Par exemple, vous pouvez ajouter ou modifier l’objet ou le texte du message.

    > [!WARNING]
    > Bien que vous puissiez ajouter ou supprimer des personnes de cet e-mail, cela ne modifie pas les autorisations que vous avez spécifiées dans la boîte de dialogue **Partage protégé** concernant la pièce jointe. Par exemple, si vous souhaitez modifier ces autorisations, accordez l’autorisation d’ouvrir le fichier à une nouvelle personne, fermez l’e-mail sans l’enregistrer ni l’envoyer, puis revenez à l’étape 1.

5.  Envoyez l’e-mail.

## <a name="examples-and-other-instructions"></a>Exemples et autres instructions
Pour obtenir des exemples et des instructions concernant l’utilisation de l’application de partage Rights Management, voir les sections suivantes dans le Guide d’utilisation de l’application de partage Rights Management :

-   [Exemples d’utilisation de l’application de partage RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Que voulez-vous faire ?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]