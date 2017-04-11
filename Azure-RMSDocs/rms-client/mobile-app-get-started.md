---
title: "Bien démarrer : application AIP pour iOS et Android"
description: 
keywords: "Guide pratique pour afficher des e-mails ou des fichiers avec l’application Azure Information Protection pour iOS et Android"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 96ab267f22abf31d39a77dcc5450b28a583096e8
ms.sourcegitcommit: 81b5c111627246a4094ef87da17d260f66ae985c
translationtype: HT
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>Bien démarrer avec l’application Microsoft Azure Information Protection pour iOS et Android

*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection*

La plupart des gens utilisent généralement l’application Azure Information Protection automatiquement quand ils ont besoin d’ouvrir un fichier ou un e-mail protégé. Toutefois, si vous êtes administrateur et que vous souhaitez tester l’application pour vos utilisateurs, ou simplement faire un essai avant d’en avoir besoin, vous pouvez utiliser les instructions suivantes.

Sur votre appareil mobile, vous devez accéder à l’un des fichiers que l’application prend en charge pour voir la visionneuse en action. Exemple :

- **Un fichier .rpmsg** : il s’agit d’un e-mail protégé par des droits qui s’affiche comme pièce jointe dans un e-mail lorsque votre application de messagerie sur votre appareil mobile ne prend pas en charge la protection des données Rights Management de manière native. 
    
    Utilisez un autre appareil pour vous envoyer un e-mail protégé par des droits auquel vous pouvez accéder à partir de votre appareil mobile. Par exemple, utilisez Outlook à partir d’un ordinateur Windows. Pour obtenir la liste des clients de messagerie prenant en charge la gestion des droits de manière native, consultez la colonne Adresse de messagerie dans [Applications prenant en charge la protection des données Azure Rights Management](../get-started/requirements-applications.md).

- **Un fichier PDF protégé par des droits** : à partir d’un ordinateur Windows, utilisez le client Azure Information Protection pour [protéger un fichier PDF](client-classify-protect.md), puis envoyez ce fichier PDF protégé par des droits par e-mail à votre adresse en tant que pièce jointe. Vous pouvez également télécharger un fichier PDF dans une bibliothèque protégée SharePoint, puis la partager en utilisant votre adresse e-mail.

- **Un fichier ptxt, .pjpg ou .ppng** : à partir d’un ordinateur Windows, utilisez le client Azure Information Protection pour protéger un fichier texte ou image, puis envoyez ce fichier protégé par e-mail à votre adresse en tant que pièce jointe. Pour obtenir la liste complète des types de fichiers que vous pouvez utiliser pour les tests, consultez le premier tableau de la section [Types de fichiers pris en charge pour la classification et la protection](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) du Guide d’administration du client Azure Information Protection. 

Pour afficher ces fichiers dans l’application de visionneuse Azure Information Protection, cliquez sur la pièce jointe ou le lien dans l’e-mail. Lorsque vous êtes invité à sélectionner une application avez laquelle les ouvrir, sélectionnez l’application **Visionneuse d’accès et de protection des informations**. Vous serez invité à vous connecter avec votre compte professionnel ou scolaire, ou invité à sélectionner un certificat. Une fois ces informations d’identification authentifiées, l’application Azure Information Protection affiche l’e-mail ou le fichier que vous voulez lire.

## <a name="next-steps"></a>Étapes suivantes

Si vous avez d’autres questions concernant cette application, vérifiez si elles sont traitées dans le [FAQ pour l’application Azure Information Protection pour iOS et Android](mobile-app-faq.md). 

Si vous avez d’autres questions, accédez à notre [site Yammer](https://www.yammer.com/AskIPTeam) ou [envoyez un e-mail à l’équipe Information Protection](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]