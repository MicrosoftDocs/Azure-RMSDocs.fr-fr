---
title: Afficher les fichiers protégés avec le client d’étiquetage unifié Azure Information Protection
description: Instructions pour afficher un fichier protégé qui vous oblige à installer la Azure Information Protection visionneuse d’étiquetage unifiée.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: bbe2a70714d65bff27ce7dc9131ea33fc0774454
ms.sourcegitcommit: 40693000ce86110e14ffce3b553e42149d6b7dc2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2019
ms.locfileid: "75326539"
---
# <a name="user-guide-view-protected-files-with-the-azure-information-protection-unified-labeling-client"></a>Guide de l’utilisateur : afficher les fichiers protégés avec le client d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Souvent, vous pouvez afficher un fichier protégé simplement en l’ouvrant. Par exemple, vous pouvez double-cliquer sur une pièce jointe à un e-mail ou sur un fichier dans l’Explorateur de fichiers, ou bien vous pouvez cliquer sur un lien vers un fichier.

Si les fichiers ne s’ouvrent pas immédiatement, la **visionneuse Azure Information Protection** pourra peut-être le faire. Cette visionneuse peut ouvrir des fichiers texte protégés, des fichiers image protégés, des fichiers PDF protégés et tous les fichiers ayant une extension de nom de fichier **.pfile**.

La visionneuse s’installe automatiquement dans le cadre de l’Azure Information Protection client d’étiquetage unifié, ou vous pouvez l’installer séparément. Vous pouvez installer à la fois ce client et la visionneuse à partir de la page [Microsoft Azure information protection](https://go.microsoft.com/fwlink/?LinkId=303970) du site Web Microsoft. Pour plus d’informations sur l’installation de ce client, consultez [Télécharger et installer le client d’étiquetage unifié Azure information protection](install-unifiedlabelingclient-app.md).

> [!NOTE]
> Bien que l’installation du client offre davantage de fonctionnalités, elle réclame des autorisations d’administrateur local, et un service correspondant pour votre organisation est requis pour pouvoir profiter de l’ensemble des fonctionnalités : Par exemple, Azure Information Protection.
> 
> Installez la visionneuse si vous avez reçu un document protégé par un utilisateur d’une autre organisation ou si vous n’avez pas d’autorisations d’administrateur local sur votre PC.

Pour être en mesure d’ouvrir un document protégé, l’application doit être « Compatible RMS ». Les applications Office et la visionneuse Azure Information Protection sont des exemples d’applications compatibles RMS. Pour obtenir une liste d’applications par type et les appareils pris en charge, consultez le tableau [applications compatibles RMS](../requirements-applications.md#rms-enlightened-applications). 

## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg en tant que pièce jointe de courrier électronique

Si vous voyez **message.rpmsg** en tant que pièce jointe dans un e-mail, il ne s’agit pas d’un document protégé mais d’un message électronique protégé qui s’affiche comme pièce jointe. Il n’est pas possible d’utiliser la visionneuse Azure Information Protection pour Windows pour afficher cet e-mail protégé sur un PC Windows. Vous avez plutôt besoin d’une application de messagerie pour Windows qui prend en charge la protection Rights Management, comme Office Outlook. Ou vous pouvez utiliser Outlook sur le web.

Toutefois, si vous avez un appareil iOS ou Android, vous pouvez utiliser l’application Azure Information Protection pour ouvrir ces messages électroniques protégés. Vous pouvez télécharger cette application pour ces appareils mobiles à partir de la page [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft.

## <a name="prompts-for-authentication"></a>Invites pour l’authentification

Pour que vous puissiez afficher le fichier protégé, le service Rights Management qui a été utilisé pour protéger le fichier doit confirmer que vous y êtes autorisé. Pour ce faire, il vérifie votre nom d’utilisateur et votre mot de passe. Dans certains cas, ces informations d’identification peuvent être mises en cache et donc vous ne voyez pas d’invite vous demandant de vous connecter. Dans d'autres cas, vous êtes invité à fournir vos informations d’identification.

Si votre organisation ne dispose pas d’un compte cloud dont vous pouvez vous servir (pour Office 365 ou Azure) et n’utilise pas une version locale équivalente (AD RMS), vous avez deux options :

- Si vous avez reçu un e-mail protégé, suivez les instructions pour vous connecter avec votre fournisseur d’identité sociale (comme Google pour un compte Gmail) ou demandez un code secret à usage unique.

- Vous pouvez demander un compte gratuit acceptant vos informations d’identification pour pouvoir ouvrir des documents protégés par Rights Management. Pour demander ce compte, cliquez sur le lien pour [RMS for individuals](https://go.microsoft.com/fwlink/?LinkId=309469) et utilisez votre adresse e-mail au sein de votre entreprise au lieu d’une adresse e-mail personnelle. 

## <a name="to-view-a-protected-file"></a>Pour afficher un fichier protégé

1. Ouvrez le fichier protégé (par exemple, en double-cliquant sur le fichier ou la pièce jointe, ou en cliquant sur le lien vers le fichier). Si vous êtes invité à sélectionner une application, sélectionnez **Visionneuse Azure Information Protection**. 

2. Si vous voyez une page de **connexion** ou d’**inscription** : cliquez sur **Se connecter** et entrez vos informations d’identification. Si le fichier protégé vous a été envoyé comme pièce jointe, veillez à spécifier la même adresse e-mail que celle utilisée pour vous envoyer le fichier.
    
    Si vous ne disposez pas d’un compte qui est accepté, consultez la section [Invites pour l’authentification](#prompts-for-authentication) de cette page.

3. Une version en lecture seule du fichier s’ouvre dans la **visionneuse de Azure information protection** ou dans l’application associée à l’extension de nom de fichier.

4. Si vous avez des fichiers protégés supplémentaires à ouvrir, vous pouvez y accéder directement depuis la visionneuse, en utilisant l’option **Ouvrir**. Votre fichier sélectionné remplace le fichier d’origine dans la visionneuse. 

> [!TIP]
> Si le fichier protégé ne s’ouvre pas alors que vous avez installé le client Azure Information Protection complet, essayez l’option **Réinitialiser les paramètres**. Pour accéder à cette option, à partir d’une application Office, sélectionnez le bouton **sensibilité** > **aide et commentaires** > **Réinitialiser les paramètres**. 
> 
> [Informations supplémentaires sur l’option Réinitialiser les paramètres](clientv2-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

