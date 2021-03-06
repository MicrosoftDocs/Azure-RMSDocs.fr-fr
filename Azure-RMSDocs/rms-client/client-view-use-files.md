---
title: Afficher les fichiers protégés avec la visionneuse cliente Azure Information Protection Classic
description: Instructions pour afficher et utiliser un fichier protégé qui vous oblige à installer la visionneuse cliente Azure Information Protection Classic.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 1/13/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 5a0bbc3160784259f3bf6799135b6cb82fb64693
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807040"
---
# <a name="user-guide-view-protected-files-with-the-azure-information-protection-classic-client-viewer"></a>Guide de l’utilisateur : afficher les fichiers protégés avec la visionneuse cliente Azure Information Protection Classic

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Concerne :** [Azure information protection client classique pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez le [Guide de l’utilisateur du client d’étiquetage unifié](clientv2-view-use-files.md). *

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Souvent, vous pouvez afficher un fichier protégé simplement en l’ouvrant. Par exemple, vous pouvez double-cliquer sur une pièce jointe à un e-mail ou sur un fichier dans l’Explorateur de fichiers, ou bien vous pouvez cliquer sur un lien vers un fichier.

Si les fichiers ne s’ouvrent pas immédiatement, la **visionneuse de Azure information protection** peut être en mesure de l’ouvrir. Cette visionneuse peut ouvrir des fichiers texte protégés, des fichiers image protégés, des fichiers PDF protégés et tous les fichiers ayant une extension de nom de fichier **.pfile**.

La visionneuse s’installe automatiquement dans le cadre du client Azure Information Protection, ou vous pouvez l’installer séparément. Vous pouvez installer le client et la visionneuse à partir de la page [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft. Pour plus d’informations sur l’installation du client, consultez [Télécharger et installer le client Azure Information Protection](install-client-app.md).

> [!NOTE]
> Bien que l’installation du client offre davantage de fonctionnalités, elle réclame des autorisations d’administrateur local, et un service correspondant pour votre organisation est requis pour pouvoir profiter de l’ensemble des fonctionnalités : par exemple, Azure Information Protection ou les services AD RMS (Active Directory Rights Management Services).
> 
> Installez la visionneuse si vous avez reçu un document protégé par un utilisateur d’une autre organisation ou si vous n’avez pas d’autorisations d’administrateur local sur votre PC.

Pour être en mesure d’ouvrir un document protégé, l’application doit être « Compatible RMS ». Les applications Office et la visionneuse Azure Information Protection sont des exemples d’applications compatibles RMS. Pour afficher la liste des applications par type et des appareils pris en charge, consultez les tableaux des applications compatibles avec [RMS](../requirements-applications.md) .
  
## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg en tant que pièce jointe de courrier électronique

Si vous voyez **message.rpmsg** en tant que pièce jointe dans un e-mail, il ne s’agit pas d’un document protégé mais d’un message électronique protégé qui s’affiche comme pièce jointe. Il n’est pas possible d’utiliser la visionneuse Azure Information Protection pour Windows pour afficher cet e-mail protégé sur un PC Windows. Vous avez plutôt besoin d’une application de messagerie pour Windows qui prend en charge la protection Rights Management, comme Office Outlook. Ou vous pouvez utiliser Outlook sur le web.

Toutefois, si vous avez un appareil iOS ou Android, vous pouvez utiliser l’application Azure Information Protection pour ouvrir ces messages électroniques protégés. Vous pouvez télécharger cette application pour ces appareils mobiles à partir de la page [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft.

## <a name="prompts-for-authentication"></a>Invites pour l’authentification

Pour que vous puissiez afficher le fichier protégé, le service Rights Management qui a été utilisé pour protéger le fichier doit confirmer que vous y êtes autorisé. Pour ce faire, il vérifie votre nom d’utilisateur et votre mot de passe. Dans certains cas, ces informations d’identification peuvent être mises en cache et donc vous ne voyez pas d’invite vous demandant de vous connecter. Dans d'autres cas, vous êtes invité à fournir vos informations d’identification.

Si votre organisation ne dispose pas d’un compte Cloud que vous pouvez utiliser (pour Microsoft 365 ou Azure) et qu’elle n’utilise pas une version locale équivalente (AD RMS), vous avez deux options :

- Si vous avez reçu un e-mail protégé, suivez les instructions pour vous connecter avec votre fournisseur d’identité sociale (comme Google pour un compte Gmail) ou demandez un code secret à usage unique.

- Vous pouvez demander un compte gratuit acceptant vos informations d’identification pour pouvoir ouvrir des documents protégés par Rights Management. Pour demander ce compte, cliquez sur le lien pour [RMS for individuals](https://go.microsoft.com/fwlink/?LinkId=309469) et utilisez votre adresse e-mail au sein de votre entreprise au lieu d’une adresse e-mail personnelle. 

## <a name="to-view-and-use-a-protected-document"></a>Pour afficher et utiliser un document protégé

1. Ouvrez le fichier protégé (par exemple, en double-cliquant sur le fichier ou la pièce jointe, ou en cliquant sur le lien vers le fichier). Si vous êtes invité à sélectionner une application, sélectionnez **Visionneuse Azure Information Protection**. 

2. Si vous voyez une page de **connexion** ou d’**inscription** : cliquez sur **Se connecter** et entrez vos informations d’identification. Si le fichier protégé vous a été envoyé comme pièce jointe, veillez à spécifier la même adresse e-mail que celle utilisée pour vous envoyer le fichier.
    
    Si vous ne disposez pas d’un compte qui est accepté, consultez la section [Invites pour l’authentification](#prompts-for-authentication) de cette page.

3. Une version en lecture seule du fichier s’ouvre dans **Azure Information Protection Viewer**. Si vous disposez des autorisations suffisantes, vous pouvez imprimer le fichier et le modifier. 

    Vous pouvez vérifier vos autorisations sur le fichier en cliquant sur **Autorisations**. Dans la boîte de dialogue **Autorisations**, vous pouvez également identifier le propriétaire du fichier à contacter si vous voulez lui demander une nouvelle version du fichier avec des autorisations supplémentaires.
    
    Pour plus d’informations sur les autorisations et les droits d’utilisation de chacune d’elle, consultez [Droits inclus dans les niveaux d’autorisation](../configure-usage-rights.md#rights-included-in-permissions-levels).

4. Pour modifier le fichier, cliquez sur **Enregistrer sous**, ce qui vous permet d’enregistrer le fichier protégé avec son extension de nom de fichier d’origine. Vous pouvez ensuite le modifier à l’aide de l’application associée à son type. À ce stade, l’étiquette et la protection du fichier sont supprimées.
    
    Notez qu’étant donné que la visionneuse est destinée aux fichiers protégés, le bouton **Enregistrer sous** est activé uniquement pour ces fichiers.
    
5. Une fois que vous avez terminé les modifications du fichier, dans l’Explorateur de fichiers, cliquez avec le bouton droit sur le fichier pour réappliquer l’étiquette. Cette action réapplique la protection.

6. Si vous avez des fichiers protégés supplémentaires à ouvrir, vous pouvez y accéder directement depuis la visionneuse, en utilisant l’option **Ouvrir**. Votre fichier sélectionné remplace le fichier d’origine dans la visionneuse. 

> [!TIP]
> Si le fichier protégé ne s’ouvre pas alors que vous avez installé le client Azure Information Protection complet, essayez l’option **Réinitialiser les paramètres**. Pour accéder à cette option, à partir d’une application Office, sélectionnez le bouton **Protéger** > **Aide et commentaires** > **Réinitialiser les paramètres**. 
> 
> [Informations supplémentaires sur l’option Réinitialiser les paramètres](client-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

