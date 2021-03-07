---
title: Visionneuses PDF protégées pour Microsoft Information Protection
description: Découvrez comment ouvrir et afficher des PDF étiquetés pour la classification et la protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: c982293c4b6544e0bc093caef5a94596660bfcb5
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415379"
---
# <a name="which-pdf-readers-are-supported-for-protected-pdfs"></a>Quels sont les lecteurs PDF pris en charge pour les fichiers PDF protégés ?

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Cet article décrit les lecteurs PDF protégés pris en charge pour Azure Information Protection (AIP). Les lecteurs PDF protégés permettent aux utilisateurs d’ouvrir ces fichiers PDF chiffrés et d’afficher les informations sensibles qu’ils contiennent.

Le chiffrement de vos fichiers PDF avec AIP garantit que les personnes non autorisées ne peuvent pas lire le contenu du fichier. Lecteurs PDF protégés qui prennent en charge AIP Vérifiez que vous avez reçu les autorisations nécessaires pour ouvrir le document et déchiffrez également le contenu pour vous.

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

Cette norme est utilisée par défaut par le client AIP.

> [!NOTE]
> **Client classique uniquement**: Si vous avez le client classique AIP, il a peut-être été [désactivé par un administrateur](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).
> 

### <a name="viewing-protected-pdfs-in-adobe-acrobat-reader"></a>Affichage de fichiers PDF protégés dans Adobe Acrobat Reader

Adobe Acrobat Reader s’intègre aux solutions Microsoft Information Protection, telles que Azure Information Protection pour offrir aux utilisateurs une expérience simplifiée et cohérente pour les fichiers PDF classés et/ou protégés.

L’intégration d’Adobe Acrobat Reader avec Microsoft Information Protection est prise en charge pour [Windows](#installing-a-protected-pdf-reader-for-windows-or-mac) et [MacOS](#installing-a-protected-pdf-reader-for-windows-or-mac).

Pour plus d’informations, consultez les billets de blog suivants : 

- [Disponibilité générale de l’intégration d’Adobe Acrobat Reader avec Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [FAQ sur l’intégration d’Adobe Reader et de Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac"></a>Affichage de fichiers PDF protégés dans Microsoft Edge sur Windows ou Mac

Microsoft Edge offre une prise en charge intégrée de l’affichage des fichiers PDF classés et protégés. L’utilisation de Microsoft Edge garantit que les utilisateurs peuvent ouvrir des fichiers PDF protégés sans qu’il soit nécessaire d’installer ou de configurer des paramètres ou des logiciels supplémentaires.

Les versions prises en charge sont les suivantes :

- **Windows**: Windows 10 et versions antérieures via Windows 8. 
    
    Pour plus d’informations sur les versions antérieures, consultez [prise en charge des formats précédents](#support-for-previous-formats).

- **Mac**: macOS versions 10,12 et ultérieures 


**Instructions**: 

1. Vérifiez la [version de Microsoft Edge](https://support.microsoft.com/help/4027011/microsoft-edge-find-out-which-version-you-have) installée sur votre système. 
1. Si la version de Microsoft Edge est 83.0.478.37 ou supérieure, vous pouvez ouvrir des fichiers protégés directement dans le navigateur Edge. 

1. Pour ouvrir des fichiers PDF dans SharePoint, cliquez sur **ouvrir**  >  **ouvrir dans le navigateur**. 

    :::image type="content" source="../media/edge_open_browser.png" alt-text="Ouvrir un fichier PDF protégé à l’aide de Microsoft Edge à partir du navigateur à l’aide de l’option ouvrir dans le navigateur":::
 
## <a name="installing-a-protected-pdf-reader-for-windows-or-mac"></a>Installation d’un lecteur PDF protégé pour Windows ou Mac

Pour ouvrir un document PDF protégé sur votre ordinateur de bureau, nous vous recommandons d’installer le [plug-in Microsoft information protection (MIP) approprié pour Acrobat et Acrobat Reader](https://go.microsoft.com/fwlink/?linkid=2050049) pour votre système d’exploitation.

**Instructions**:

1. Si vous ne l’avez pas déjà fait, installez Adobe Reader à partir du [site Adobe](https://www.adobe.com/).

    Veillez à lire et à accepter les [conditions générales d’utilisation d’Adobe](https://www.adobe.com/legal/terms.html).

1. Installez le [plug-in MIP pour Acrobat et Acrobat Reader](https://go.microsoft.com/fwlink/?linkid=2050049) pour votre système d’exploitation.  

    Les versions prises en charge sont les suivantes :

    - **Windows**: Windows 10 et versions antérieures via Windows 8. 
    
        Pour plus d’informations sur les versions antérieures, consultez [prise en charge des formats précédents](#support-for-previous-formats).

    - **Mac**: macOS versions 10,12-10,14 

1. Si vous êtes invité à approuver l’administrateur, demandez à votre administrateur d’autoriser le plug-in.

    Par exemple :
    
    :::image type="content" source="../media/admin-approval-for-mip-in-adobe-reader.png" alt-text="Approbation d’administrateur requise pour installer le plug-in MIP pour Acrobat et Acrobat Reader":::
    
> [!NOTE]
> Pour plus d’informations, consultez l' [annonce Microsoft information protection et Adobe Release](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396).
> 

### <a name="alternative-protected-pdf-readers-for-windows"></a>Autres lecteurs PDF protégés pour Windows

Vous pouvez également utiliser l’un des lecteurs PDF suivants pour Windows qui adhèrent à la norme ISO pour le chiffrement PDF :

- [Visionneuse Azure Information Protection](https://go.microsoft.com/fwlink/?linkid=838993) 

- [Lecteur Foxit](https://www.foxitsoftware.com/pdf-reader/)

## <a name="installing-a-protected-pdf-reader-for-mobile-iosandroid"></a>Installation d’un lecteur PDF protégé pour mobile (iOS/Android)

Pour ouvrir un fichier PDF protégé sur votre appareil iOS ou Android, téléchargez et installez l’application pour votre système d’exploitation :

|Système d''exploitation  |Lien  |
|---------|---------|
|**iTunes**     | [![Installez à partir d’iTunes.](../media/small/ios-icon-small.png)](https://apps.apple.com/app/microsoft-rights-management/id689516635)        |
|**Google Play**     |[![Installez à partir de Google Play.](../media/small/android-icon-small.png)](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)         |
| | |

Pour plus d’informations, consultez [applications de visionneuse mobile pour Azure information protection (iOS et Android)](mobile-app-faq.md).

## <a name="support-for-previous-formats"></a>Prise en charge des formats précédents

Les lecteurs PDF suivants prennent en charge les fichiers PDF protégés avec l’extension **. ppdf** et les anciens formats avec une extension **. pdf** .

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
- [Applications de visionneuse mobile pour Azure Information Protection (iOS et Android)](mobile-app-faq.md)