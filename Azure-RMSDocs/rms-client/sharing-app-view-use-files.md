---
title: "Ouvrir des fichiers protégés par RMS avec l’application de partage RMS - AIP"
description: "Instructions à suivre pour afficher et utiliser un fichier protégé. Cette procédure nécessite l’installation de l’application de partage Rights Management (RMS)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 43f083ffaf8aefd9b79b2cb64a6408e565818b9b
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
ms.translationtype: HT
ms.contentlocale: fr-FR
---
# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Afficher et utiliser des fichiers qui ont été protégés par Rights Management

>*S’applique à : Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Quand [l’application de partage Rights Management (RMS) est installée sur votre ordinateur](install-sharing-app.md), vous pouvez afficher un fichier protégé simplement en double-cliquant dessus. Le fichier peut être une pièce jointe à un message électronique, ou un fichier apparaissant dans l'Explorateur de fichiers.

> [!NOTE]
> Pour que vous puissiez afficher le fichier protégé, le service Rights Management doit confirmer que vous y êtes autorisé. Pour ce faire, il vérifie vos nom d’utilisateur et mot de passe. Dans certains cas, cette opération peut être mise en cache de sorte que vous ne voyez pas d'invite vous demandant vos informations d'identification. Dans d'autres cas, vous êtes invité à fournir vos informations d'identification.
>
> Si votre organisation n’utilise pas Azure Information Protection ou AD RMS, vous pouvez demander un compte gratuit acceptant vos informations d’identification afin de pouvoir ouvrir des fichiers protégés à l’aide de RMS :
>
> -   Pour demander ce compte, cliquez sur le lien [RMS for Individuals](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Lorsque vous vous inscrivez, utilisez l'adresse de messagerie de votre organisation plutôt qu'une adresse personnelle. Si vous vous inscrivez parce que vous reçu une pièce protégée jointe à un message électronique, utilisez l'adresse de messagerie à laquelle ce message a été envoyé.
> -   Pour plus d’informations, consultez [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md).

## <a name="to-view-a-protected-file"></a>Pour afficher un fichier protégé
Dans l'Explorateur de fichiers ou dans le message électronique contenant la pièce jointe, double-cliquez sur le fichier protégé, puis entrez vos informations d'identification si vous y êtes invité.

Si vous voyez deux versions du fichier dont les extensions diffèrent, n'ouvrez celle dont l'extension est .ppdf uniquement si l'autre ne s'ouvre pas. Si vous ne pouvez pas non plus ouvrir la version .ppdf, installez l’[application de partage RMS](install-sharing-app.md), qui peut ouvrir des fichiers dont l’extension est .ppdf.

> [!NOTE]
> Pour plus d’informations, consultez [Qu’est-ce que le fichier .ppdf créé automatiquement ?](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)

La manière dont le fichier s'ouvre dépend de la manière dont il a été protégé, ce que vous pouvez déterminer en examinant l'extension de son nom. Dans chaque cas, l'ouverture du fichier peut être auditée et reste auditée tant qu'il est protégé. En outre, si le fichier a été envoyé en pièce jointe à un e-mail, il se peut que l'expéditeur soit informé par e-mail chaque fois que vous ouvrez le fichier.

- **L’extension du nom du fichier est* .pfile***

    Le fichier fait l'objet d'une protection générique.

    Quand vous ouvrez le fichier, une boîte de dialogue **Fichier protégé** de l’application de partage s’affiche. Elle vous indique l’utilisateur qui a protégé le fichier et vous informe que vous devez respecter les autorisations de copropriétaire. Pour lire le fichier, cliquez sur **Ouvrir** .

    ![Boîte de dialogue d’un fichier .pfile partagé par e-mail quand vous faites appel à l’application de partage RMS](../media/ADRMS_MSRMSApp_PfilePermission.png)

- **L’extension du nom du fichier est* .ppdf* ou le fichier est un fichier texte ou image protégé (par exemple, *.ptxt* ou *.pjpg*)**

    Le fichier fait l'objet d'une protection native en tant que copie en lecture seule.

    Le fichier s'ouvre dans la visionneuse installée en même temps que l'application de partage RMS. Ce fichier est en lecture seule, même si vous l'enregistrez dans un autre emplacement ou le renommez.

- **Autres extensions de nom de fichier**

    Le fichier fait l'objet d'une protection native.

    Le fichier s'ouvre dans l'application associée à l'extension d'origine de son nom, et une bannière de restriction s'affiche en haut du fichier. La bannière peut afficher les autorisations appliquées au fichier, ou un lien permettant de les afficher. Par exemple, il se peut que s'affiche ce qui suit, et que vous deviez cliquer sur **Les autorisations sont actuellement restreintes** pour afficher les autorisations appliquées au fichier et les personnes pouvant accéder à celui-ci :

    ![Bannière à accès restreint lorsque le fichier est protégé](../media/ADRMS_MSRMSApp_RestrictedAccess.png)



Pour obtenir la liste complète des extensions de nom de fichier prises en charge par les services Rights Management, consultez la section [Types de fichier pris en charge et extensions de nom de fichier](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) du [Guide de l’administrateur de l’application de partage Rights Management](sharing-app-admin-guide.md). Si votre extension de nom de fichier n’est pas répertoriée, faites une recherche sur le web pour déterminer si cette extension de nom de fichier est prise en charge par une autre application.

> [!NOTE]
> Si, après avoir confirmé que le fichier est bien protégé par Rights Management, il ne s’ouvre pas, téléchargez et utilisez l’[outil Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Suivez les instructions contenues dans l’outil pour rechercher la présence de problèmes éventuels sur votre ordinateur qui pourraient empêcher l’ouverture d’un document protégé.

## <a name="to-use-files-that-have-been-protected-for-example-edit-and-print-the-file"></a>Pour utiliser un fichier protégé (par exemple, l'éditer et l'imprimer)
Si, après avoir ouvert le fichier protégé, vous voulez le lire, mais aussi, par exemple, le modifier, le copier et l’imprimer :

- **L’extension du nom du fichier est* .pfile***

    Enregistrez le fichier ouvert en lui donnant une nouvelle extension de nom associée à l'application que vous souhaitez utiliser.

    Par exemple, si un fichier a été protégé sous le nom document.vsdx.pfile, affichez-le, puis, dans l'Explorateur de fichiers, enregistrez-le sous document.vsdx.

    Le nouveau fichier n'est plus protégé. Si vous souhaitez le protéger, vous devez le faire manuellement. Pour obtenir des instructions, consultez [Protéger un fichier sur un appareil (protéger sur place) à l’aide de l’application de partage Rights Management](sharing-app-protect-in-place.md).

- **L’extension du nom du fichier est* .ppdf* ou le fichier est un fichier texte ou image protégé (par exemple, *.ptxt* ou *.pjpg*)**

    Vous pouvez uniquement afficher le fichier et, même si vous le renommez ou le déplacez, sa protection subsiste.

- **Autres extensions de nom de fichier**

    Pour utiliser de tels fichiers, votre appareil doit disposer d’une application comprenant la protection Rights Management. Les applications de ce type sont qualifiées de « compatibles RMS ». Les applications Office 2016, Office 2013 et Office 2010 (telles que Word, Excel, PowerPoint et Outlook) sont des exemples d’applications compatibles avec Rights Management. Toutefois, des applications ne provenant pas de Microsoft, telles que celles publiées par d'autres éditeurs de logiciels ou vos propres applications métier, peuvent également être compatibles Rights Management.

    Les applications compatibles Rights Management savent comment ouvrir des fichiers protégés par d'autres applications compatibles Rights Management. Elles conservent également la protection appliquée au fichier, même si vous modifiez celui-ci ou l'enregistrez sous un autre nom ou dans un autre emplacement. Ces applications vous permettent d'utiliser le fichier conformément aux autorisations qui lui sont appliquées de sorte que, si vous disposez des autorisations nécessaires, vous l'utiliser. Par exemple, il se peut que vous puissiez modifier le fichier mais pas l'imprimer.


## <a name="examples-and-other-instructions"></a>Exemples et autres instructions
Pour obtenir des exemples et des instructions concernant l’utilisation de l’application de partage Rights Management, voir les sections suivantes dans le Guide d’utilisation de l’application de partage Rights Management :

-   [Exemples d’utilisation de l’application de partage RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Que voulez-vous faire ?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]