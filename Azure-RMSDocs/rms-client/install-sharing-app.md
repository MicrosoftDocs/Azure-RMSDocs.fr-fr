---
title: "Télécharger et installer l’application de partage RMS - AIP"
description: "Instructions d’installation interactive de l’application de partage RMS pour Windows dans le but de partager des documents avec d’autres utilisateurs en toute sécurité."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 9c954f750c6f49d3db1bf6383efa2805f291682c
ms.lasthandoff: 02/24/2017


---

# <a name="download-and-install-the-rights-management-sharing-application"></a>Télécharger et installer l'application de partage Rights Management

>*S’applique à : Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Pour installer l’application de partage RMS, vous ne devez pas nécessairement être administrateur local. Toutefois, si vous ne l’êtes pas et utilisez Office 2010, il existe quelques limitations. Pour plus d’informations, consultez la section [Si vous n’êtes pas administrateur local et utilisez Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) dans cette page.

## <a name="to-download-and-install-the-rights-management-sharing-application"></a>Pour télécharger et installer l’application de partage Rights Management

1.  Accédez à la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft.

2.  Dans la section **Ordinateurs**, cliquez sur l’icône de l’**application RMS pour Windows** et enregistrez le fichier **Setup.exe** pour installer l’application de partage Microsoft Rights Management.

3.  Double-cliquez sur le fichier Setup.exe qui a été téléchargé. Si vous êtes invité à continuer, cliquez sur **Oui**.

4.  Dans la page **Installer Microsoft RMS**, cliquez sur **Suivant**, puis attendez que l’installation se termine.

    > [!NOTE]
    > L’application de partage RMS nécessite au minimum la version Microsoft .NET Framework 4.0. Le programme d’installation vérifie si elle est installée et, si ce n’est pas le cas, un message comportant un lien pour son installation s’affiche.

5.  Une fois l’installation terminée, cliquez sur **Redémarrer** pour redémarrer votre ordinateur et terminer l’installation. Vous pouvez également cliquer sur **Fermer** et redémarrer l’ordinateur ultérieurement pour terminer l’installation.

Vous pouvez à présent protéger vos fichiers et lire des fichiers protégés par d’autres personnes.

## <a name="if-you-are-not-a-local-administrator-and-use-office-2010"></a>Si vous n’êtes pas administrateur local et utilisez Office 2010
Si vous vous connectez à votre ordinateur sans disposer de droits d’administration locale, et que le programme d’installation détecte qu’Office 2010 est installé, un message d’avertissement s’affiche, indiquant que certains scénarios ne fonctionnent pas avec cette configuration. Ces scénarios sont les suivants :

-   Si votre organisation utilise le service Azure Rights Management d’Azure Information Protection plutôt que sur une version locale de Rights Management :

    -   Les fonctionnalités de Gestion des droits relatifs à l’Information (IRM) d’Office ne sont pas disponibles. Par exemple, l’option **Ne pas transférer** pour les e-mails, et les **restrictions d’accès** que vous pouvez définir par le biais des autorisations dans le menu **Fichier** de Word et Excel. Vous pouvez utiliser l’option Protégé contre le partage accessible dans le ruban, et les options de clic droit de l’Explorateur de fichiers.

-   Si votre organisation utilise une version locale de Rights Management plutôt que le service Azure Rights Management d’Azure Information Protection :

    -   Vous ne pouvez pas lire un document protégé qui vous est envoyé par un membre d’une autre organisation utilisant le service Azure Rights Management.

Si vous n’êtes pas administrateur local et utilisez Office 365 ou Office 2013, vous ne voyez pas ce message et ces scénarios sont pris en charge.

Vous pouvez continuer l’installation avec ces limitations connues. Vous pouvez aussi l’arrêter, puis soit la relancer avec l’option **Exécuter en tant qu’administrateur** lors de l’exécution du fichier Setup.exe à l’étape 3, soit demander à un administrateur de l’installer pour vous. Les administrateurs peuvent [créer un script d’installation](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application) qui s’exécute automatiquement.

## <a name="examples-and-other-instructions"></a>Exemples et autres instructions
Pour obtenir des exemples et des instructions concernant l’utilisation de l’application de partage Rights Management, voir les sections suivantes dans le Guide d’utilisation de l’application de partage Rights Management :

-   [Exemples d’utilisation de l’application de partage RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Que voulez-vous faire ?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

