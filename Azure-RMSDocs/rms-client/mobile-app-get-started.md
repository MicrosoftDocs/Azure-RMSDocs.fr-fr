---
title: 'Bien démarrer : application AIP pour iOS et Android'
description: Afficher des e-mails ou des fichiers avec l’application Azure Information Protection pour iOS et Android
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 622786bc1192d6727ef748df970adeb53733f4f8
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298082"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>Bien démarrer avec l’application Microsoft Azure Information Protection pour iOS et Android

*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Cette page explique comment tester l’exécution des applications Azure Information Protection pour iOS ou Android.

La plupart des utilisateurs se servent généralement de l’application Azure Information Protection quand ils ont besoin d’ouvrir un fichier ou un e-mail protégé. Toutefois, si vous êtes un administrateur qui teste l’application pour vos utilisateurs, ou si vous souhaitez simplement l’essayer avant de l’avoir besoin, suivez les instructions ci-dessous pour afficher les fichiers protégés sur votre appareil.

> [!IMPORTANT]
> Avant de commencer, lisez les conditions requises et les instructions relatives à [l’application Azure information protection pour iOS ou Android ?](mobile-app-faq.md)
> 

## <a name="access-a-protected-file-from-your-device"></a>Accéder à un fichier protégé à partir de votre appareil

Pour tester l’application mobile AIP, assurez-vous que vous pouvez accéder à l’un des types de fichiers protégés suivants à partir de votre appareil :

|Type de fichier  |Instructions  |
|---------|---------|
|**Un fichier. rpmsg**     | Message électronique protégé par des droits. Si votre application de messagerie mobile ne prend pas en charge la protection des données Rights Management en mode natif, les messages électroniques protégés sont affichés sous forme de pièces jointes. </br></br>Utilisez un autre appareil, tel qu’Outlook à partir d’un ordinateur Windows, pour vous envoyer un e-mail protégé par des droits auquel vous pouvez accéder à partir de votre appareil mobile. </br></br>**Remarque :** Pour obtenir la liste des clients de messagerie qui prennent en charge Rights Management en mode natif, consultez les lignes de **courrier électronique** dans les [applications qui prennent en charge Azure Rights Management la protection des données](../requirements-applications.md). |
|**Un fichier PDF protégé par des droits**     | 1. à partir d’un ordinateur Windows, protégez un fichier PDF à l’aide du client du [client d’étiquetage](clientv2-classify-protect.md) [classique](client-classify-protect.md) ou unifié d’AIP. </br>2. envoyez-vous le fichier PDF protégé, ou téléchargez-le dans une bibliothèque protégée SharePoint et partagez-le avec votre propre adresse de messagerie.        |
|**A. PTXT ou. pjpg ou. PPNG**     | 1. à partir d’un ordinateur Windows, protégez un fichier texte ou image à l’aide du client [client d’étiquetage](clientv2-classify-protect.md) [classique](client-classify-protect.md) ou unifié d’AIP. </br></br>2. envoyez-vous le fichier protégé, ou téléchargez-le dans une bibliothèque protégée SharePoint et partagez-le avec votre propre adresse de messagerie. </br></br>**Remarque :** Pour plus d’informations, consultez [types de fichiers pris en charge pour la classification et la protection](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)   |
| | |

### <a name="open-the-protected-file-on-your-mobile"></a>Ouvrir le fichier protégé sur votre mobile

1. Appuyez sur la pièce jointe de courrier électronique ou sur le lien pour ouvrir votre contenu protégé.

1. Lorsque vous y êtes invité, sélectionnez l’application de **visionneuse AIP** pour afficher le contenu protégé.

1. Lorsque vous y êtes invité, connectez-vous avec votre compte professionnel ou scolaire ou sélectionnez un certificat.

Une fois authentifié, l’application de visionneuse AIP affiche l’e-mail ou le fichier pour vous.

> [!NOTE]
> Ouvrez toujours l’application AIP en ouvrant le contenu protégé. N’essayez pas de vous connecter à l’application tant que vous n’y êtes pas invité ou d’ouvrir un fichier protégé à partir de l’application de visionneuse AIP.
> 

## <a name="next-steps"></a>Étapes suivantes

Utilisez l’une des méthodes suivantes pour fournir des commentaires sur les applications mobiles AIP :

- Accéder aux **paramètres**  >  **Envoyer des commentaires**
- Publiez votre question sur notre [site Yammer](https://www.yammer.com/AskIPTeam)