---
title: Lecteurs PDF protégés pour Microsoft Information Protection
description: Installer un lecteur pour les documents PDF étiquetés pour la classification et la protection
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: dd8a895c0fb6fb94311d7e028265bf9bbdbfe668
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927706"
---
# <a name="which-pdf-readers-are-supported-for-protected-pdfs"></a>Quels sont les lecteurs PDF pris en charge pour les fichiers PDF protégés ?

Les lecteurs PDF des fichiers PDF classifiés et/ou protégés vous permettent d’ouvrir des fichiers PDF chiffrés qui contiennent des informations sensibles.

Le chiffrement de vos fichiers PDF avec [Azure information protection (AIP)](../what-is-information-protection.md) garantit que les personnes non autorisées ne peuvent pas lire le contenu du fichier, et que même les personnes autorisées ne peuvent pas partager des écrans ou des captures d’écran qui affichent le contenu.

Lecteurs PDF protégés qui prennent en charge Azure Information Protection Vérifiez que vous disposez des autorisations nécessaires pour ouvrir le document et déchiffrez également le contenu pour vous.

Par exemple, l’illustration suivante montre un document chiffré ouvert dans Adobe Acrobat Reader. La barre située en haut indique que le document est protégé par une solution Microsoft Information Protection.

:::image type="content" source="../media/protected-pdf-in-adobe-reader.png" alt-text="PDF protégé ouvrir dans Adobe Acrobat Reader":::

Pour obtenir des instructions, consultez les sections suivantes :

- [Affichage de fichiers PDF protégés dans Microsoft Edge sur Windows ou Mac](#viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac)

- [Installation d’un lecteur PDF protégé pour Windows ou Mac](#installing-a-protected-pdf-reader-for-windows-or-mac)

- [Installation d’un lecteur PDF protégé pour mobile (iOS/Android)](#installing-a-protected-pdf-reader-for-mobile-iosandroid)

> [!TIP]
> Si votre document ne s’ouvre pas après l’installation d’un lecteur recommandé, il est possible que le document soit protégé dans un format plus ancien. 
>
> Dans ce cas, essayez l’un des lecteurs listés comme étant pris en charge pour les formats précédents. Pour plus d’informations, consultez [prise en charge des formats précédents](#support-for-previous-formats).
> 
### <a name="iso-standards-for-pdf-encryption"></a>Normes ISO pour le chiffrement PDF

Les lecteurs PDF référencés sur cette page peuvent tous des documents protégés ouverts qui adhèrent à la norme ISO pour le chiffrement PDF. 

Cette norme est utilisée par défaut par les clients d’étiquetage classique et unifiés, sauf si elle a été [désactivée par un administrateur](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).

### <a name="viewing-protected-pdfs-in-adobe-acrobat-reader"></a>Affichage de fichiers PDF protégés dans Adobe Acrobat Reader

Adobe Acrobat Reader s’intègre aux solutions Microsoft Information Protection, telles que [Azure information protection](../what-is-information-protection.md) pour offrir aux utilisateurs une expérience simplifiée et cohérente pour les fichiers PDF classés et/ou protégés.

L’intégration d’Adobe Acrobat Reader avec Microsoft Information Protection est prise en charge pour [Windows](protected-pdf-readers-windows.md) et [MacOS](protected-pdf-readers-mac.md).

Pour plus d’informations, consultez les billets de blog suivants : 

- [Disponibilité générale de l’intégration d’Adobe Acrobat Reader avec Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [FAQ sur l’intégration d’Adobe Reader et de Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac"></a>Affichage de fichiers PDF protégés dans Microsoft Edge sur Windows ou Mac

Microsoft Edge offre une prise en charge native de l’affichage des fichiers PDF qui sont classifiés et protégés. L’utilisation de Microsoft Edge garantit que les utilisateurs peuvent ouvrir des fichiers PDF protégés sans qu’il soit nécessaire d’installer ou de configurer des paramètres ou des logiciels supplémentaires.

Les versions prises en charge sont les suivantes :

- **Windows :** Windows 10 et versions antérieures via Windows 8. 
    
    Pour plus d’informations sur les versions antérieures, consultez [prise en charge des formats précédents](#support-for-previous-formats).

- **Mac :** macOS versions 10,12 et ultérieures 



<!--
With Microsoft Edge, when a user encounters a locally saved protected PDF file, they can view the file directly in the browser. If the file is available on SharePoint, the user only needs to click **Open** > **Open in browser** from Microsoft Edge, to view the file. 
-->

**Ample** 

1. Vérifiez la [version de Microsoft Edge](https://support.microsoft.com/help/4027011/microsoft-edge-find-out-which-version-you-have) installée sur votre système. 
1. Si la version de Microsoft Edge est 83.0.478.37 ou supérieure, vous pouvez ouvrir des fichiers protégés directement dans le navigateur Edge. 

1. Pour ouvrir des fichiers PDF dans SharePoint, cliquez sur **ouvrir**  >  **ouvrir dans le navigateur**. 

    :::image type="content" source="../media/edge_open_browser.png" alt-text="Ouvrir un fichier PDF protégé à l’aide de Microsoft Edge à partir du navigateur à l’aide de l’option ouvrir dans le navigateur":::
 
## <a name="installing-a-protected-pdf-reader-for-windows-or-mac"></a>Installation d’un lecteur PDF protégé pour Windows ou Mac

Pour ouvrir un document PDF protégé sur votre ordinateur de bureau, nous vous recommandons d’installer le [plug-in Microsoft information protection (MIP) approprié pour Acrobat et Acrobat Reader](https://go.microsoft.com/fwlink/?linkid=2050049) pour votre système d’exploitation.

**Ample**

1. Si vous ne l’avez pas déjà fait, installez Adobe Reader à partir du [site Adobe](https://www.adobe.com/).

    Veillez à lire et à accepter les [conditions générales d’utilisation d’Adobe](https://www.adobe.com/legal/terms.html).

1. Installez le [plug-in MIP pour Acrobat et Acrobat Reader](https://go.microsoft.com/fwlink/?linkid=2050049) pour votre système d’exploitation.  

    Télécharger : [ ![Télécharger](../media/download.png "Télécharger le plug-in MIP pour Acrobat et Acrobat Reader")](https://go.microsoft.com/fwlink/?linkid=2050049)

    Les versions prises en charge sont les suivantes :

    - **Windows :** Windows 10 et versions antérieures via Windows 8. 
    
        Pour plus d’informations sur les versions antérieures, consultez [prise en charge des formats précédents](#support-for-previous-formats).

    - **Mac :** macOS versions 10,12-10,14 

1. Si vous êtes invité à approuver l’administrateur, demandez à votre administrateur d’autoriser le plug-in.

    Par exemple :
    
    :::image type="content" source="../media/admin-approval-for-mip-in-adobe-reader.png" alt-text="Approbation d’administrateur requise pour installer le plug-in MIP pour Acrobat et Acrobat Reader":::
    
> [!NOTE]
> Pour plus d’informations, consultez l' [annonce Microsoft information protection et Adobe Release](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396).
> 

### <a name="alternative-protected-pdf-readers-for-windows"></a>Autres lecteurs PDF protégés pour Windows

Vous pouvez également utiliser l’un des lecteurs PDF suivants pour Windows qui adhèrent à la norme ISO pour le chiffrement PDF :

- Téléchargement de la visionneuse Azure Information Protection [ ![Download](../media/download.png "Télécharger la visionneuse AIP")](https://go.microsoft.com/fwlink/?linkid=838993) 

- Téléchargement de Foxit Reader [ ![Download](../media/download.png "Télécharger Foxit Reader Viewer")](https://www.foxitsoftware.com/pdf-reader/)

## <a name="installing-a-protected-pdf-reader-for-mobile-iosandroid"></a>Installation d’un lecteur PDF protégé pour mobile (iOS/Android)

Pour ouvrir un fichier PDF protégé sur votre appareil iOS ou Android, téléchargez et installez l’application pour votre système d’exploitation :

- Azure Information Protection l’application pour le [ ![Téléchargement](../media/download.png "Application Azure Information Protection pour iOS") d’iOS  ](https://go.microsoft.com/fwlink/?LinkId=325338)

- Azure Information Protection l’application pour le [ ![Téléchargement](../media/download.png "Application Azure Information Protection pour Android") Android](https://go.microsoft.com/fwlink/?LinkId=325340)

Pour plus d’informations, consultez [qu’est-ce que l’application Azure information protection pour iOS ou Android ?](mobile-app-faq.md).

## <a name="support-for-previous-formats"></a>Prise en charge des formats précédents

Les lecteurs PDF suivants prennent en charge les fichiers PDF protégés avec l’extension **. ppdf** , ainsi que les anciens formats avec une extension **. pdf** .

Si vous ne parvenez pas à ouvrir votre fichier PDF protégé à l’aide du lecteur recommandé, le document peut être protégé dans un format antérieur. Par exemple, Microsoft SharePoint utilise actuellement un format plus ancien pour les documents PDF dans les bibliothèques protégées par IRM.

- **Windows 10/versions antérieures via Windows 7 Service Pack 1**

    - [Visionneuse Azure Information Protection](https://go.microsoft.com/fwlink/?linkid=838993)
    - Gaaiho Doc
    - Client PDF GigaTrust Desktop pour Adobe
    - Foxit Reader
    - Nitro PDF Reader
    - Nuance Power PDF
    - Chrome de bord

- **Android**:

    - [Application Azure Information Protection](mobile-app-faq.md)
    - Foxit MobilePDF avec RMS
    - GigaTrust App pour Android

- **iOS**:

    - [Application Azure Information Protection](mobile-app-faq.md)
    - Foxit MobilePDF avec RMS
    - TITUS Docs

- **MacOS Catalina**: Edge chrome

## <a name="next-steps"></a>Étapes suivantes

Si vous avez besoin d’aide supplémentaire après l’installation de, suivez les instructions et la documentation de chaque lecteur. Par exemple, consultez les articles suivants :

- [Guide de l’utilisateur : afficher les fichiers protégés avec le client d’étiquetage unifié Azure Information Protection](clientv2-view-use-files.md)
- [Qu’est-ce que l’application Azure Information Protection pour iOS ou Android ?](mobile-app-faq.md)