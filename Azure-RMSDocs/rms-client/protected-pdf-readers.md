---
title: Lecteurs PDF protégés pour Microsoft Information Protection
description: Installer un lecteur pour les documents PDF étiquetés pour la classification et la protection
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: 755424c1f3c813ca517ae4afcbe1e4d7a134276f
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84250039"
---
# <a name="pdf-readers-that-support-microsoft-information-protection"></a>Lecteurs PDF prenant en charge Microsoft Information Protection

Si vous avez besoin d’ouvrir un document PDF protégé par Microsoft Information Protection, utilisez les liens et les informations ci-dessous.

Un document PDF protégé est susceptible de contenir des informations sensibles. Pour renforcer la sécurité, le document est chiffré de sorte que les personnes non autorisées ne puissent pas le lire, et que les personnes autorisées ne peuvent pas partager des écrans ou des captures d’écran qui affichent le document. 

Pour ouvrir ce document, vous avez besoin d’un lecteur (parfois appelé visionneuse) qui vérifie que vous avez reçu les autorisations nécessaires pour ouvrir le document, puis le déchiffrer pour vous.

## <a name="install-pdf-readers-for-your-device"></a>Installer des lecteurs PDF pour votre appareil

Sélectionnez l’appareil que vous utilisez pour installer un lecteur PDF qui peut ouvrir des documents PDF protégés. Tous ces lecteurs peuvent ouvrir des documents protégés qui adhèrent à la norme ISO pour le chiffrement PDF :

- **Ordinateurs**: [Windows](protected-pdf-readers-windows.md)  |  [MacOS](protected-pdf-readers-mac.md)

- **Appareils mobiles**: [Android](protected-pdf-readers-android.md)  |  [iOS](protected-pdf-readers-ios.md)

### <a name="support-for-previous-formats"></a>Prise en charge des formats précédents

Les lecteurs PDF dans le tableau suivant prennent en charge les documents PDF protégés qui ont une extension de nom de fichier. ppdf, ainsi que les anciens formats qui ont une extension de nom de fichier. pdf. 

À l’heure actuelle, Microsoft SharePoint utilise un format plus ancien pour les documents PDF dans les bibliothèques protégées par IRM.


|Système d'exploitation|Lecteurs pris en charge|
|----------------|-----------------------------------|
|Windows 10 et versions antérieures<br />via Windows 7 Service Pack 1|Visionneuse Azure Information Protection<br /><br />Gaaiho Doc<br /><br />Client PDF GigaTrust Desktop pour Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF|
|Android|Application Azure Information Protection<br /><br />Foxit MobilePDF avec RMS<br /><br />GigaTrust App pour Android|
|iOS|Application Azure Information Protection<br /><br />Foxit MobilePDF avec RMS<br /><br />TITUS Docs|

## <a name="using-adobe-acrobat-reader-with-the-adobe-plug-in"></a>Utilisation d’Adobe Acrobat Reader avec le plug-in Adobe

Une collaboration entre Microsoft et Adobe vous offre une expérience plus simple et plus cohérente pour les documents PDF qui ont été classés et éventuellement protégés. Cette collaboration assure la prise en charge de l’intégration native d’Adobe Acrobat aux solutions Microsoft Information Protection, par exemple [Azure Information Protection](../what-is-information-protection.md). 

Cette intégration native présente les avantages suivants :

- Vous pouvez afficher les documents PDF qui ont été protégés parce qu’ils contiennent des informations sensibles.

- Vous pouvez voir la valeur de classification de l’étiquette de votre organisation qui a été appliquée au document.

- Prise en charge de la norme ISO pour le chiffrement PDF.
    
    À moins que cette fonctionnalité ait été [désactivée par un administrateur](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), ce format de fichier PDF protégé est activé par défaut pour le client Azure information protection (Classic) et est toujours utilisé par le client d’étiquetage unifié Azure information protection.

Vous pouvez utiliser le plug-in Adobe avec [Windows](protected-pdf-readers-windows.md) et [MacOS](protected-pdf-readers-mac.md).

Pour plus d’informations, consultez les billets de blog suivants : 

- [Disponibilité générale de l’intégration d’Adobe Acrobat Reader avec Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [FAQ sur l’intégration d’Adobe Reader et de Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="next-steps"></a>Étapes suivantes

Utilisez les liens de cette page pour installer un lecteur PDF afin de pouvoir ouvrir des documents PDF protégés.

Si vous avez besoin d’aide sur le lecteur après son installation, suivez les instructions et la documentation qui l’accompagnent. Par exemple, pour la visionneuse de Azure Information Protection pour Windows, consultez le Guide de l' [utilisateur : afficher les fichiers protégés avec le client d’étiquetage unifié Azure information protection](clientv2-view-use-files.md).
