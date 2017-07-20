---
title: "Afficher et utiliser des documents protégés à l’aide du client AIP"
description: "Instructions pour afficher et utiliser un document protégé qui vous oblige à installer le client Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d8fd80d6ff97118cd37dd62e293768b145c98595
ms.sourcegitcommit: 1c3ebf4ad64b55db4fec3ad007fca71ab7d38c02
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2017
---
# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Afficher et utiliser des fichiers qui ont été protégés par Rights Management

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

Souvent, vous pouvez afficher un document protégé simplement en l’ouvrant. Par exemple, vous pouvez double-cliquer sur une pièce jointe à un e-mail ou sur un fichier dans l’Explorateur de fichiers, ou bien vous pouvez cliquer sur un lien vers un fichier.

Si les fichiers ne s’ouvrent pas immédiatement, la **visionneuse Azure Information Protection** pourrait être en mesure de les ouvrir. Cette visionneuse peut ouvrir des fichiers texte protégés, des fichiers image protégés, des fichiers PDF protégés et tous les fichiers ayant une extension de nom de fichier **.pfile**.

La visionneuse s’installe automatiquement dans le cadre du client Azure Information Protection, ou vous pouvez l’installer séparément. Vous pouvez installer le client et la visionneuse à partir de la page [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft. Pour plus d’informations sur l’installation du client, consultez [Télécharger et installer le client Azure Information Protection](install-client-app.md).

> [!NOTE]
> Bien que l’installation du client fournisse davantage de fonctionnalités, elle requiert des autorisations de l’administrateur local et le fonctionnement intégral requiert un service correspondant à votre organisation :
> 
> - Azure Information Protection
> 
> - Gestion des droits Azure
> 
> - Active Directory Rights Management Services 
> 
> Installez la visionneuse si vous avez reçu un document protégé par un utilisateur d’une autre organisation ou si vous n’avez pas d’autorisations d’administrateur local sur votre PC.

Pour être en mesure d’ouvrir un document protégé, l’application doit être « Compatible RMS ». Les applications Office et la visionneuse Azure Information Protection sont des exemples d’applications compatibles RMS. Pour obtenir une liste d’applications par type et les appareils pris en charge, consultez le tableau [applications compatibles RMS](../get-started/requirements-applications.md#rms-enlightened-applications).  
## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg en tant que pièce jointe de courrier électronique

Si vous voyez **message.rpmsg** en tant que pièce jointe dans un e-mail, il ne s’agit pas d’un document protégé mais d’un message électronique protégé qui s’affiche comme pièce jointe. Vous ne pouvez pas utiliser la visionneuse Azure Information Protection pour Windows pour afficher ce message électronique protégé sur votre PC Windows. Vous devez à la place disposer d’une application de messagerie pour Windows qui prend en charge la protection Rights Management, comme Office Outlook. Ou vous pouvez utiliser Outlook sur le web.

Toutefois, si vous avez un appareil iOS ou Android, vous pouvez utiliser l’application Azure Information Protection pour ouvrir ces messages électroniques protégés. Vous pouvez télécharger cette application pour ces appareils mobiles à partir de la page [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft.

## <a name="prompts-for-authentication"></a>Invites pour l’authentification

Pour que vous puissiez afficher le fichier protégé, le service Rights Management qui a été utilisé pour protéger le fichier doit confirmer que vous y êtes autorisé. Pour ce faire, il vérifie vos nom d’utilisateur et mot de passe. Dans certains cas, cette opération peut être mise en cache de sorte que vous ne voyez pas d'invite vous demandant vos informations d'identification. Dans d'autres cas, vous êtes invité à fournir vos informations d'identification.

Si votre organisation ne dispose pas d’un compte cloud que vous pouvez utiliser (pour Office 365 ou Azure) et qu’elle n’utilise pas de version locale équivalente (AD RMS), vous pouvez obtenir un compte gratuit qui accepte vos informations d’identification afin de pouvoir ouvrir des fichiers protégés par Rights Management :

-   Pour demander ce compte, cliquez sur le lien [RMS for Individuals](http://go.microsoft.com/fwlink/?LinkId=309469).
    
    Lorsque vous vous inscrivez, utilisez l'adresse de messagerie de votre organisation plutôt qu'une adresse personnelle. Si vous vous inscrivez parce que vous reçu une pièce protégée jointe à un message électronique, utilisez l'adresse de messagerie à laquelle ce message a été envoyé.
    
-   Pour plus d’informations, consultez [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md).

## <a name="to-view-and-use-a-protected-document"></a>Pour afficher et utiliser un document protégé

1. Ouvrez le fichier protégé (par exemple, en double-cliquant sur le fichier ou la pièce jointe, ou en cliquant sur le lien vers le fichier). Si vous êtes invité à sélectionner une application, sélectionnez **Visionneuse Azure Information Protection**. 

2. Si vous voyez une page de **connexion** ou d’**inscription** : cliquez sur **Se connecter** et entrez vos informations d’identification. Si le fichier protégé vous a été envoyé comme pièce jointe, veillez à spécifier la même adresse e-mail que celle utilisée pour vous envoyer le fichier.
    
    Si vous ne disposez pas d’un compte qui est accepté, consultez la section [Invites pour l’authentification](#prompts-for-authentication) de cette page. Inscrivez-vous pour obtenir un compte gratuit et revenez à ces instructions.

3. Une version en lecture seule du fichier s’ouvre dans **Azure Information Protection Viewer**. Si vous disposez des autorisations suffisantes, vous pouvez imprimer le fichier et le modifier. 

    Vous pouvez vérifier vos autorisations sur le fichier en cliquant sur **Autorisations**. Dans la boîte de dialogue **Autorisations**, vous pouvez également identifier le propriétaire du fichier à contacter si vous voulez lui demander une nouvelle version du fichier avec des autorisations supplémentaires.
    
    Pour plus d’informations sur les autorisations et les droits d’utilisation de chacune d’elle, consultez [Droits inclus dans les niveaux d’autorisation](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels).

4. Pour modifier le fichier, cliquez sur **Enregistrer sous**, ce qui vous permet d’enregistrer le fichier sans protection avec son extension de nom de fichier d’origine. Vous pouvez ensuite le modifier à l’aide de l’application associée à son type.

5. Si vous avez des fichiers protégés supplémentaires à ouvrir, vous pouvez y accéder directement depuis la visionneuse, en utilisant l’option **Ouvrir**. Votre fichier sélectionné remplace le fichier d’origine dans la visionneuse. 

> [!TIP]
> Si le fichier protégé ne s’ouvre pas, utilisez l’option **Aide et commentaires** d’Azure Information Protection, puis sélectionnez **Exécuter les diagnostics**. Une fois les tests terminés, vous pouvez réinitialiser le client, ce qui peut résoudre votre problème.


## <a name="other-instructions"></a>Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]