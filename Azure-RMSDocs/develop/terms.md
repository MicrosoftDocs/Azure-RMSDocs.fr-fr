---
title: "Terminologie de développeurs AIP | Microsoft Docs"
description: "Une collection de définitions pour les développeurs propres aux services Rights Management."
keywords: 
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c99a87deb6c333ed61e13c5d98f59d6623f75cbd
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
---
# <a name="terms"></a>Conditions d'utilisation

Une collection de définitions pour les développeurs propres à Azure Information Protection.

**Algorithme déprécié**  
Paramètre modal qui implémente un ancien schéma de protection de contenu, se référant en particulier au mode de chiffrement ECB (Electronic CodeBook). Dans ce SDK, le paramètre vous permet de générer des licences compatibles avec la bibliothèque MSDRM utilisée par le Kit [AD Rights Management SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx).

Ce paramètre peut inciter l’application à protéger le contenu non conformément aux normes de vos clients pour la protection de contenu.

Ce paramètre empêche votre application de tirer parti des améliorations de chiffrement ajoutées à Microsoft Rights Management SDK 3.0 ou ultérieur.

**Format de fichier protégé de Microsoft**

Ce format, également appelé PFile, est le format de fichier par défaut pour AD RMS qui fait office de norme pour les applications RMS.

Le format PFile est transparent pour le développeur d’applications, car il est intégré dans la conception de Microsoft Rights Management SDK 4.2.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]