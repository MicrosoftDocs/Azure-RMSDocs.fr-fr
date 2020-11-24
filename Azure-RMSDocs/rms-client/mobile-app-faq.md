---
title: Azure Information Protection des applications mobiles pour iOS & Android
description: Découvrez les principes de base des applications mobiles Azure Information Protection (AIP) pour les appareils iOS et Android
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/24/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 17f1efc5c5e0c01f33e638d1ef674a81b17494f8
ms.sourcegitcommit: 5b7235f7bb77cc88716f15dda0aa0d832e0f7063
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734962"
---
# <a name="what-is-the-azure-information-protection-app-for-ios-or-android"></a>Qu’est-ce que l’application Azure Information Protection pour iOS ou Android ?

*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

L’application mobile Azure Information Protection (AIP) pour iOS et Android est une application de visionneuse qui vous permet d’afficher des messages électroniques, des fichiers PDF, des images et des fichiers texte protégés, et qui sont utiles si vos applications normales pour ces types de fichiers ne prennent pas en charge la protection. 

Par exemple, si des e-mails protégés s’affichent dans votre application mobile de messagerie standard en tant que pièces jointes, vous souhaiterez peut-être utiliser l’application mobile AIP pour afficher cet e-mail.

Pour plus d’informations, consultez [Applications prenant en charge la protection des données Azure Rights Management](../requirements-applications.md).

> [!NOTE]
> Les applications mobiles AIP sont *uniquement des visionneuses* et ne vous permettent pas de créer de nouveaux courriers électroniques ou de répondre à des courriers électroniques, ni de créer ou de modifier des fichiers protégés. Les applications mobiles AIP ne peuvent pas non plus ouvrir des pièces jointes à des e-mails ou des fichiers PDF protégés.
> 

## <a name="download-and-install-the-aip-app-for-your-device"></a>Télécharger et installer l’application AIP pour votre appareil

Téléchargez et installez les applications mobiles AIP à partir de l’un des emplacements suivants :

**iTunes**

:::image type="content" source="../media/develop/ios-icon.png" alt-text="iTunes" link="https://apps.apple.com/app/microsoft-rights-management/id689516635" border="false":::

**Google Play**

:::image type="content" source="../media/develop/android-icon.png" alt-text="Google Play" link="https://play.google.com/store/apps/details?id=com.microsoft.ipviewer" border="false":::

**Page de téléchargement AIP**

:::image type="content" source="../media/aip-icon.png" alt-text="Page de téléchargement de Azure Information Protection" border="false":::

Sélectionnez les icônes [iOS](https://apps.apple.com/app/microsoft-rights-management/id689516635) ou [Android](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer) dans la section **périphériques mobiles** .

**Votre portail d’entreprise**

Si votre appareil mobile est géré par Microsoft Intune, vous pouvez télécharger les applications mobiles AIP à partir du portail d’entreprise. 

Pour plus d’informations, contactez votre administrateur système.

## <a name="ios-view-protected-files-on-your-device"></a>iOS : afficher les fichiers protégés sur votre appareil

Une fois que vous avez [installé l’application mobile AIP](#download-and-install-the-aip-app-for-your-device), ouvrez un fichier ou un e-mail protégé. 

1. Si vous êtes invité à sélectionner une application pour ouvrir le fichier, appuyez sur le bouton partager pour partager le fichier à la place.

    Sélectionnez **partager le fichier via...** , puis sélectionnez **copier dans la visionneuse AIP.**

    Par exemple :

    :::image type="content" source="../media/ios-share-to-aip-viewer.png" alt-text="Partager avec la visionneuse AIP dans iOS" border="false":::

1. Connectez-vous ou sélectionnez un certificat comme invité.

    Une fois que vous avez été authentifié, l’e-mail ou le fichier s’ouvre dans la visionneuse AIP.
 
## <a name="android-view-protected-files-on-your-device"></a>Android : afficher les fichiers protégés sur votre appareil

Une fois que vous avez [installé l’application mobile AIP](#download-and-install-the-aip-app-for-your-device), ouvrez un fichier ou un e-mail protégé. 

1. Lorsque vous êtes invité à sélectionner une application, sélectionnez la visionneuse AIP :

    :::image type="content" source="../media/select-aip-viewer.png" alt-text="Sélectionner l’application mobile de la visionneuse AIP":::

1. Connectez-vous ou sélectionnez un certificat comme invité.

    Une fois que vous avez été authentifié, l’e-mail ou le fichier s’ouvre dans la visionneuse AIP.

## <a name="aip-mobile-app-requirements"></a>Configuration requise pour l’application mobile AIP

Les applications mobiles AIP pour iOS et Android prennent en charge les types de fichiers et les environnements suivants :

|Condition requise  |Description  |
|---------|---------|
|**Versions du système d'exploitation prises en charge**     | Les OSs mobiles minimum incluent : </br>-iOS 11  </br>-Android 6,0 </br></br>**Remarque :** Les applications mobiles AIP ne sont pas prises en charge sur les processeurs Intel.  |
|**Informations d’identification de connexion prises en charge**     | Connectez-vous aux applications mobiles AIP avec l’un des éléments suivants : </br></br>**Informations d’identification professionnelles ou scolaires.** Essayez de vous connecter avec vos informations d’identification professionnelles ou scolaires. Si vous avez des questions, contactez votre administrateur pour savoir si votre organisation a AD RMS localement avec l’extension d’appareil mobile, ou utilise Azure Information Protection. </br></br>**Compte Microsoft**. Si votre adresse de messagerie personnelle a été utilisée pour protéger le fichier, connectez-vous à l’aide d’un [compte Microsoft](https://signup.live.com). Si vous devez demander un compte Microsoft, vous pouvez utiliser votre propre adresse de messagerie Hotmail, Gmail ou toute autre adresse de messagerie. </br></br>**Remarque :** Toutes les applications ne sont pas en mesure d’ouvrir du contenu protégé avec une compte Microsoft. Pour plus d’informations, consultez [scénarios pris en charge pour l’ouverture de documents protégés](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).|
|**Types de fichiers pris en charge**     | Les types de fichiers pris en charge incluent les messages électroniques protégés, les fichiers PDF, les images et les fichiers texte. </br></br>Par exemple, ces fichiers incluent les extensions suivantes : **rpmsg,** **. pdf,** **. ppdf,** **. pjpg,** **. pjpeg,** **. ptiff,** **.** PPNG,. PTXT **,** **. pXML** </br></br>Pour obtenir la liste complète des types de fichiers pris en charge, consultez [le Guide de l’administrateur du client AIP](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection).|
| | |

## <a name="admins-testing-the-aip-mobile-apps"></a>Administrateurs : test des applications mobiles AIP

La plupart des utilisateurs utilisent généralement l’application mobile AIP pour ouvrir un fichier ou un e-mail protégé qui ne peut pas être ouvert à l’aide de leurs applications mobiles ordinaires.

Si vous êtes un administrateur système qui souhaite tester les applications mobiles AIP pour votre organisation ou si vous souhaitez simplement l’essayer par vous-même, suivez les instructions ci-dessous pour vous guider tout au long du processus.

1. Assurez-vous que vous avez accès à un type de fichier pris en charge par l’application mobile AIP à partir de votre appareil. 

    Par exemple, envoyez-vous l’un des fichiers protégés par des droits suivants :

    |Type de fichier  |Instructions  |
    |---------|---------|
    |**Adresse de messagerie (. rpmsg)**     | Utilisez un autre appareil, tel qu’Outlook à partir d’un ordinateur Windows, pour vous envoyer un e-mail protégé par des droits auquel vous pouvez accéder à partir de votre appareil mobile.  |
    |**PDF**     | 1. à partir d’un ordinateur Windows, protégez un fichier PDF à l’aide du client d’étiquetage [classique](client-classify-protect.md) ou [unifié](clientv2-classify-protect.md) d’AIP. </br>2. envoyez-vous le fichier PDF protégé, ou téléchargez-le dans une bibliothèque protégée SharePoint et partagez-le avec votre propre adresse de messagerie.        |
    |**Image (. PTXT,. pjpg ou. PPNG)**     | 1. à partir d’un ordinateur Windows, protégez un fichier texte ou image à l’aide du client d’étiquetage [classique](client-classify-protect.md) ou [unifié](clientv2-classify-protect.md) d’AIP. </br></br>2. envoyez-vous le fichier protégé, ou téléchargez-le dans une bibliothèque protégée SharePoint et partagez-le avec votre propre adresse de messagerie.   |
| | |

1. Ouvrez le fichier protégé sur votre appareil mobile à l’aide de la pièce jointe ou du lien de courrier électronique que vous avez envoyé à vous-même.

    Par exemple, les e-mails protégés apparaissent dans votre application mobile de messagerie standard en tant que pièces jointes. 

1. Lorsque vous êtes invité à sélectionner une application pour ouvrir l’e-mail ou le fichier protégé, sélectionnez l’application de **visionneuse AIP** .

1. Connectez-vous ou sélectionnez un certificat, lorsque vous y êtes invité. 

    Une fois authentifié, l’application de visionneuse AIP affiche l’e-mail ou le fichier pour vous.

> [!NOTE]
> Ouvrez toujours l’application AIP en ouvrant le contenu protégé. N’essayez pas de vous connecter à l’application tant que vous n’y êtes pas invité ou d’ouvrir un fichier protégé à partir de l’application de visionneuse AIP.
> 

## <a name="next-steps"></a>Étapes suivantes

Utilisez l’une des méthodes suivantes pour fournir des commentaires sur les applications mobiles AIP :

- Accéder aux **paramètres**  >  **Envoyer des commentaires**
- Publiez votre question sur notre [site Yammer](https://www.yammer.com/AskIPTeam)
