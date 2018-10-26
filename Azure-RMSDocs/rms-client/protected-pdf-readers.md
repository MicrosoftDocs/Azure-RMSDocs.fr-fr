---
title: Lecteurs PDF protégés pour Microsoft Information Protection
description: ''
keywords: ''
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/13/2018
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.openlocfilehash: ab3d141394a9a042a8a3e15e35d1daffab20ad98
ms.sourcegitcommit: 1e6394044d646278ae582c7713cac8ffb9bf4c1e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49170252"
---
# <a name="supported-pdf-readers-for-microsoft-information-protection"></a>Lecteurs PDF pris en charge pour Microsoft Information Protection

Utilisez les informations suivantes pour en savoir plus sur les documents PDF qui sont étiquetés pour la classification et la protection, et la façon d’afficher ces documents.

Une collaboration entre Microsoft et Adobe vous offre une expérience plus simple et cohérente pour les documents PDF qui ont été classifiés et éventuellement protégés. Cette collaboration assure la prise en charge de l’intégration native d’Adobe Acrobat aux solutions Microsoft Information Protection, par exemple [Azure Information Protection](../what-is-information-protection.md). 

Cette intégration native présente les avantages suivants :

- Vous pouvez afficher les documents PDF qui ont été protégés parce qu’ils contiennent des informations sensibles.

- Vous pouvez voir la valeur de classification de l’étiquette de votre organisation qui a été appliquée au document.

- Prise en charge de la norme ISO pour le chiffrement PDF.
    
    Ce format de fichier PDF protégé doit être [activé par un administrateur](client-admin-guide-customizations.md#protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption). Quand cette configuration est effectuée, l’extension de nom de fichier reste .pdf et ne passe pas au format .ppdf.

Pour plus d’informations, consultez le billet de blog suivant : [Starting October, use Adobe Acrobat Reader for PDFs protected by Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Starting-October-use-Adobe-Acrobat-Reader-for-PDFs-protected-by/ba-p/262738)

## <a name="supported-pdf-readers"></a>Lecteurs PDF pris en charge

Les lecteurs PDF suivants peuvent ouvrir des fichiers PDF protégés qui respectent la norme ISO pour le chiffrement PDF :

|Système d'exploitation|Lecteurs pris en charge et lien de téléchargement|
|----------------|-----------------------------------|
|Windows 10 et versions antérieures<br />via Windows 7 Service Pack 1|Adobe Acrobat Reader (recommandé) :<br />-  [Lire les conditions générales d’utilisation d’Adobe](https://www.adobe.com/legal/terms.html) <br />- [Télécharger la préversion](https://ardownload2.adobe.com/pub/adobe/reader/win/AcrobatDC/misc/MIP_Preview/1900820120/Adobe_MIP_Preview_1900820120.zip) <br /><br /> Visionneuse Azure Information Protection : [Télécharger](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader : [Télécharger](https://www.foxitsoftware.com/pdf-reader/)|
|Android|Application Azure Information Protection : [Télécharger](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|Application Azure Information Protection : [Télécharger](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>Prise en charge des formats précédents

Les lecteurs PDF du tableau suivant prennent en charge les documents PDF protégés avec l’extension de nom de fichier .ppdf et les formats plus anciens avec l’extension de nom de fichier .pdf.

Actuellement, SharePoint Online et SharePoint en local utilisent un format plus ancien pour les documents PDF dans les bibliothèques protégées par IRM.


|Système d'exploitation|Lecteurs pris en charge|
|----------------|-----------------------------------|
|Windows 10 et versions antérieures<br />via Windows 7 Service Pack 1|Visionneuse Azure Information Protection<br /><br />Gaaiho Doc<br /><br />Client PDF GigaTrust Desktop pour Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Application de partage RMS|
|Android|Application Azure Information Protection<br /><br />Foxit MobilePDF avec RMS<br /><br />GigaTrust App pour Android|
|iOS|Application Azure Information Protection<br /><br />Foxit MobilePDF avec RMS<br /><br />Docs TITUS|
