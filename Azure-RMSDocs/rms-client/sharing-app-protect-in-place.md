---
title: "Protéger un fichier sur un appareil (protéger sur place) à l’aide de l’application de partage Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 638c2f27c8d552653dcf3f41d8fad6d44cb08887
ms.openlocfilehash: 5150351ec6772b95d77698dc39a1f69105c02d2c


---

# Protection d'un fichier sur un appareil (Protéger sur place) à l'aide de l'application de partage Rights Management

*S’applique à : Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Lorsque vous protégez un fichier sur place, celui-ci remplace le fichier non protégé d'origine. Vous pouvez ensuite laisser le fichier là où il est, le copier vers un autre dossier ou appareil, ou partager le dossier dans lequel il se trouve : le fichier reste protégé. Vous pouvez aussi joindre le fichier protégé à un e-mail, même si la méthode recommandée pour partager un fichier protégé par e-mail consiste à le faire directement à partir de l’Explorateur de fichiers ou d’une application Office (consultez [Protéger un fichier que vous partagez par e-mail en utilisant l’application de partage Rights Management](sharing-app-protect-by-email.md)).

> [!TIP]
> Si vous rencontrez des erreurs lorsque vous tentez de protéger des fichiers, reportez-vous au [FAQ relatif à l'application de partage Microsoft Rights Management pour Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

## Pour protéger un fichier sur un appareil (Protéger sur place)

1.  Dans l'Explorateur de fichiers, sélectionnez un fichier à protéger. Cliquez avec le bouton droit, sélectionnez **Protéger avec RMS**, puis sélectionnez **Protéger sur place**. Exemple :

    ![Option de menu Protéger sur place](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Si vous ne voyez pas l'option **Protéger avec RMS** , il est probable que l'application de partage RMS ne soit pas installée sur votre ordinateur ou que celui-ci nécessite un redémarrage pour terminer l'installation. Pour plus d’informations sur l’installation de l’application de partage RMS, consultez [Télécharger et installer l’application de partage Rights Management](install-sharing-app.md).

2.  Effectuez l'une des opérations suivantes :

    -   Sélectionnez un modèle de stratégie : il s'agit d'une autorisation prédéfinie qui restreint généralement l'accès et l'utilisation à certaines personnes au sein de votre organisation. Par exemple, si le nom de votre organisation est « Contoso, Ltd », voici ce que vous pouvez lire : **Contoso, Ltd - Affichage confidentiel uniquement**. Si vous protégez un fichier sur cet ordinateur pour la première fois, vous devez commencer par sélectionner **Protection définie par la société** pour télécharger les modèles.

        La prochaine fois que vous cliquerez sur l’option **Protéger sur place**, vous aurez jusqu’à 10 modèles affichés, prêts à être sélectionnés. Si le nombre de modèles disponibles est supérieur à 10 et que vous ne voyez pas celui qui vous intéresse, cliquez sur **Protection définie par la société** pour télécharger et afficher tous les modèles.

        Lorsque vous sélectionnez un modèle de stratégie, vous pouvez également protéger plusieurs fichiers et un dossier. Lorsque vous sélectionnez un dossier, tous les fichiers qu'il contient sont automatiquement sélectionnées pour la protection. En revanche, les nouveaux fichiers que vous créez dans ce dossier ne le sont pas.

    -   Sélectionnez **Autorisations personnalisées**: Choisissez cette option si les modèles n'offrent pas le niveau de protection nécessaire, ou si vous souhaitez définir vous-même explicitement les options de protection. Spécifiez les options souhaitées pour ce fichier dans la boîte de dialogue [Ajouter une protection](sharing-app-dialog-box.md), puis cliquez sur **Appliquer**.

3.  Avant que le focus revienne sur l'Explorateur de fichiers, il se peut qu'une boîte de dialogue s'affiche brièvement pour vous informer que le fichier est protégé. Les fichiers sélectionnés sont désormais protégés. Dans certains cas (lorsque l'ajout d'une protection modifie l'extension du nom du fichier), le fichier d'origine dans l'Explorateur de fichiers est remplacé par un nouveau fichier associé à l'icône de verrou de protection de Rights Management. Exemple :

    ![Fichier protégé avec une icône de verrou pour l’application de partage RMS](../media/ADRMS_MSRMSApp_Pfile.png)

Si vous changez d’avis concernant les autorisations ou si vous devez les modifier ultérieurement, il vous suffit de reprotéger le fichier.

Si, par la suite, vous avez besoin d’ôter la protection d’un fichier, consultez [Supprimer la protection d’un fichier à l’aide de l’application de partage Rights Management](sharing-app-remove-protection.md).

## Exemples et autres instructions
Pour obtenir des exemples et des instructions concernant l’utilisation de l’application de partage Rights Management, voir les sections suivantes dans le Guide d’utilisation de l’application de partage Rights Management :

-   [Exemples d’utilisation de l’application de partage RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Que souhaitez-vous faire ?](sharing-app-user-guide.md#what-do-you-want-to-do)

## Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jul16_HO3-->


