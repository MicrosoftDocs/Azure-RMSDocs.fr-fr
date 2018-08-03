---
title: Terminologie de développeurs AIP | Microsoft Docs
description: Une collection de définitions pour les développeurs propres aux services Rights Management.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: a0b63f08041c7cf57dd079136bd55a95b1659fd3
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39375366"
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

