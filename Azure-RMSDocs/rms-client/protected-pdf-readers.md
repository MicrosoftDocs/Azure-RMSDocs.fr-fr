---
title: Lecteurs PDF protégés pour Microsoft Information Protection
description: Installer un lecteur pour les documents PDF étiquetés pour la classification et la protection
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: 04325119b44c5bfaad025e96251bc6b032285cb6
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68792836"
---
# <a name="install-a-pdf-reader-that-supports-microsoft-information-protection"></a>Installer un lecteur PDF qui prend en charge Microsoft Information Protection

Si vous avez besoin d’ouvrir un document PDF protégé par Microsoft Information Protection, utilisez les liens et les informations ci-dessous.

## <a name="choose-your-pdf-reader"></a>Choisir votre lecteur PDF

Les lecteurs PDF suivants peuvent ouvrir des documents PDF protégés qui adhèrent à la norme ISO pour le chiffrement PDF:

|Système d’exploitation|Lecteurs pris en charge et lien de téléchargement|
|----------------|-----------------------------------|
|Windows 10 et versions antérieures<br />via Windows 7 Service Pack 1|Adobe Acrobat Reader (recommandé) :<br /> 1. Lisez les [conditions générales d’utilisation d’Adobe](https://www.adobe.com/legal/terms.html) <br /> 2. Installer Adobe Reader pour Windows à partir du [site Adobe](https://www.adobe.com/)<br /> 3. Installer le [plug-in Adobe](https://go.microsoft.com/fwlink/?linkid=2050049) pour Windows <br /> 4. Si vous y êtes invité, contactez votre administrateur pour [autoriser le plug-in](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396) <br /><br /> Visionneuse Azure Information Protection : [Télécharger](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader : [Télécharger](https://www.foxitsoftware.com/pdf-reader/)|
|Versions MacOS 10,12-10,14 |Adobe Acrobat Reader:<br /> 1. Lisez les [conditions générales d’utilisation d’Adobe](https://www.adobe.com/legal/terms.html) <br /> 2. Installer Adobe Reader pour Mac à partir du [site Adobe](https://www.adobe.com/)<br /> 3. Installer le [plug-in Adobe](https://go.microsoft.com/fwlink/?linkid=2050049) pour Mac <br /> 4. Si vous y êtes invité, contactez votre administrateur pour [autoriser le plug-in](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)|
|Android|Application Azure Information Protection : [Télécharger](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|Application Azure Information Protection : [Télécharger](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>Prise en charge des formats précédents

Les lecteurs PDF dans le tableau suivant prennent en charge les documents PDF protégés qui ont une extension de nom de fichier. ppdf, ainsi que les anciens formats qui ont une extension de nom de fichier. pdf.

Actuellement, SharePoint Online et SharePoint en local utilisent un format plus ancien pour les documents PDF dans les bibliothèques protégées par IRM.


|Système d'exploitation|Lecteurs pris en charge|
|----------------|-----------------------------------|
|Windows 10 et versions antérieures<br />via Windows 7 Service Pack 1|Visionneuse Azure Information Protection<br /><br />Gaaiho Doc<br /><br />Client PDF GigaTrust Desktop pour Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF<br /><br />Application de partage RMS|
|Android|Application Azure Information Protection<br /><br />Foxit MobilePDF avec RMS<br /><br />GigaTrust App pour Android|
|iOS|Application Azure Information Protection<br /><br />Foxit MobilePDF avec RMS<br /><br />Docs TITUS|

## <a name="using-adobe-acrobat-reader-with-the-adobe-plug-in"></a>Utilisation d’Adobe Acrobat Reader avec le plug-in Adobe

Une collaboration entre Microsoft et Adobe vous offre une expérience plus simple et plus cohérente pour les documents PDF qui ont été classés et éventuellement protégés. Cette collaboration assure la prise en charge de l’intégration native d’Adobe Acrobat aux solutions Microsoft Information Protection, par exemple [Azure Information Protection](../what-is-information-protection.md). 

Cette intégration native présente les avantages suivants :

- Vous pouvez afficher les documents PDF qui ont été protégés parce qu’ils contiennent des informations sensibles.

- Vous pouvez voir la valeur de classification de l’étiquette de votre organisation qui a été appliquée au document.

- Prise en charge de la norme ISO pour le chiffrement PDF.
    
    À moins que cette fonctionnalité ait été désactivée [par un administrateur](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), ce format de fichier PDF protégé est activé par défaut pour le client Azure information protection (Classic) et est toujours utilisé par le client d’étiquetage unifié Azure information protection.

Pour plus d’informations, consultez les billets de blog suivants: 

- [Disponibilité générale de l’intégration d’Adobe Acrobat Reader avec Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [FAQ sur l’intégration d’Adobe Reader et de Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)
