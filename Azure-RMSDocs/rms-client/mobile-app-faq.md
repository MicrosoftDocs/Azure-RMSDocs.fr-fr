---
title: Applications de visionneuse mobile pour Azure Information Protection (iOS et Android)-AIP
description: Découvrez comment afficher des fichiers protégés sur vos appareils iOS et Android à l’aide des applications de visionneuse d’Azure Information Protection (AIP).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/22/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 1f0e3de4a8548761cd58cc69216a7e80fe0128e5
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415340"
---
# <a name="mobile-viewer-apps-for-azure-information-protection-on-ios-and-android"></a>Applications de visionneuse mobile pour Azure Information Protection sur iOS et Android

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Les applications mobiles Azure Information Protection (AIP) vous permettent d’afficher des e-mails, des fichiers PDF, des images et des fichiers texte protégés quand vous ne pouvez pas les ouvrir avec vos applications standard pour ces types de fichiers. Par exemple, si des e-mails protégés s’affichent dans votre application mobile de messagerie standard en tant que pièces jointes, vous souhaiterez peut-être utiliser l’application mobile AIP pour afficher cet e-mail.

**Les étiquettes de protection et de sensibilité sont prises en charge dans les versions d’Office Mobile**. Si vous avez installé des applications Office Mobile sur votre appareil, nous vous recommandons d’utiliser les applications Office pour afficher les fichiers protégés. Pour plus d’informations, consultez [fonctionnalités d’étiquette de sensibilité dans Word, Excel et PowerPoint](/microsoft-365/compliance/sensitivity-labels-office-apps#sensitivity-label-capabilities-in-word-excel-and-powerpoint).

**Si vous ouvrez votre fichier sur un ordinateur de bureau**, utilisez la [version de bureau de la visionneuse AIP](clientv2-view-use-files.md). 

> [!NOTE]
> Les applications mobiles AIP sont *uniquement des visionneuses* et ne vous permettent pas de créer de nouveaux courriers électroniques ou de répondre à des courriers électroniques, ni de créer ou de modifier des fichiers protégés. Les applications mobiles AIP ne peuvent pas non plus ouvrir des pièces jointes à des e-mails ou des fichiers PDF protégés.
> 

## <a name="aip-mobile-viewer-app-requirements"></a>Configuration requise pour l’application de visionneuse mobile AIP

Les applications de visionneuse mobile AIP pour iOS et Android prennent en charge les types de fichiers et les environnements suivants :

|Condition requise  |Description  |
|---------|---------|
|**Versions du système d'exploitation prises en charge**     | Les OSs mobiles minimum incluent : </br>-iOS 11  </br>-Android 6,0 </br></br>**Remarque**: les applications de visionneuse mobile AIP ne sont pas prises en charge sur les processeurs Intel.  |
|**Informations d’identification de connexion prises en charge**     | Connectez-vous aux applications de visionneuse mobile AIP avec l’un des éléments suivants : </br></br>**Informations d’identification professionnelles ou scolaires.** Essayez de vous connecter avec vos informations d’identification professionnelles ou scolaires. Si vous avez des questions, contactez votre administrateur pour savoir si votre organisation a AD RMS localement avec l’extension d’appareil mobile, ou utilise Azure Information Protection. </br></br>**Compte Microsoft.** Si votre adresse de messagerie personnelle a été utilisée pour protéger le fichier, connectez-vous à l’aide d’un [compte Microsoft](https://signup.live.com). Si vous devez demander un compte Microsoft, vous pouvez utiliser votre propre adresse de messagerie Hotmail, Gmail ou toute autre adresse de messagerie. </br></br>**Remarque**: toutes les applications ne sont pas en mesure d’ouvrir du contenu protégé avec une compte Microsoft. Pour plus d’informations, consultez [scénarios pris en charge pour l’ouverture de documents protégés](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).|
|**Types de fichiers pris en charge**     | Les types de fichiers pris en charge incluent les messages électroniques protégés, les fichiers PDF, les images et les fichiers texte. </br></br>Par exemple, ces fichiers incluent les extensions suivantes : **rpmsg**, **. pdf**, **. ppdf**,. **pjpg**, **. pjpeg**, **. ptiff**, **.** PPNG, **. PTXT**, **. pXML** </br></br>Pour obtenir la liste complète des types de fichiers pris en charge, consultez [le Guide de l’administrateur du client AIP](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection).|
| | |

## <a name="download-and-install-the-aip-app-for-your-device"></a>Télécharger et installer l’application AIP pour votre appareil

Si vous ne disposez pas d' [applications Office](/microsoft-365/compliance/sensitivity-labels-office-apps#sensitivity-label-capabilities-in-word-excel-and-powerpoint) que vous pouvez utiliser pour ouvrir vos fichiers protégés, téléchargez et installez les applications de visionneuse mobile AIP.

Téléchargez et installez les applications de la visionneuse mobile à partir des emplacements suivants :

|Emplacement  |Détails/lien  |
|---------|---------|
|**iTunes**     | [![Installez à partir d’iTunes.](../media/small/ios-icon-small.png)](https://apps.apple.com/app/microsoft-rights-management/id689516635)        |
|**Google Play**     |[![Installez à partir de Google Play.](../media/small/android-icon-small.png)](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)         |
|**Votre portail d’entreprise**     |  Si votre appareil mobile est géré par Microsoft Intune, vous pourrez peut-être télécharger les applications de visionneuse mobile AIP à partir du portail d’entreprise. <br><br>Pour plus d’informations, contactez votre administrateur système.        |
|     |         |

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


## <a name="admins-testing-the-aip-mobile-viewer-apps"></a>Administrateurs : test des applications de visionneuse mobile AIP

La plupart des utilisateurs utilisent généralement l’application mobile AIP pour ouvrir un fichier ou un e-mail protégé qui ne peut pas être ouvert à l’aide de leurs applications mobiles ordinaires.

Si vous êtes un administrateur système qui souhaite tester les applications de visionneuse mobile AIP pour votre organisation ou si vous souhaitez simplement essayer par vous-même, suivez les instructions ci-dessous pour vous guider tout au long du processus.

1. Assurez-vous que vous avez accès à un type de fichier pris en charge par l’application mobile AIP à partir de votre appareil. 

    Par exemple, envoyez-vous l’un des fichiers protégés par des droits suivants :

    |Type de fichier  |Instructions  |
    |---------|---------|
    |**Adresse de messagerie (. rpmsg)**     | Utilisez un autre appareil, tel qu’Outlook à partir d’un ordinateur Windows, pour vous envoyer un e-mail protégé par des droits auquel vous pouvez accéder à partir de votre appareil mobile.  |
    |**PDF**     | 1. à partir d’un ordinateur Windows, [Protégez un fichier PDF](clientv2-classify-protect.md) à l’aide du client AIP. </br>2. envoyez-vous le fichier PDF protégé, ou téléchargez-le dans une bibliothèque protégée SharePoint et partagez-le avec votre propre adresse de messagerie.        |
    |**Image (. PTXT,. pjpg ou. PPNG)**     | 1. à partir d’un ordinateur Windows, [Protégez un fichier texte ou image](clientv2-classify-protect.md) à l’aide du client AIP. </br></br>2. envoyez-vous le fichier protégé, ou téléchargez-le dans une bibliothèque protégée SharePoint et partagez-le avec votre propre adresse de messagerie.   |
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

Utilisez l’une des méthodes suivantes pour fournir des commentaires sur les applications de visionneuse mobile AIP :

- Accéder aux **paramètres**  >  **Envoyer des commentaires**
- Publiez votre question sur notre [site Yammer](https://www.yammer.com/AskIPTeam)

Pour plus d’informations sur les fonctionnalités de protection prises en charge dans vos applications, consultez [applications prenant en charge Azure Rights Management la protection des données](../requirements-applications.md).
