---
title: Terminologie de développeurs AIP | Microsoft Docs
description: Une collection de définitions pour les développeurs propres aux services Rights Management.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 87aa190a87426e61d919b8781444239c4ce5d3c7
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68790763"
---
# <a name="terms"></a>Conditions d'utilisation

Une collection de définitions pour les développeurs propres à Azure Information Protection.

**Algorithme déprécié**  
Paramètre modal qui implémente un ancien schéma de protection de contenu, se référant en particulier au mode de chiffrement ECB (Electronic CodeBook). Dans ce SDK, le paramètre vous permet de générer des licences compatibles avec la bibliothèque MSDRM utilisée par le Kit [AD Rights Management SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx).

Ce paramètre peut inciter l’application à protéger le contenu non conformément aux normes de vos clients pour la protection de contenu.

Ce paramètre empêche votre application de tirer parti des améliorations de chiffrement ajoutées au SDK Microsoft Rights Management 3.0 ou ultérieur.

**Format de fichier protégé de Microsoft**

Ce format, également appelé PFile, est le format de fichier par défaut pour AD RMS qui fait office de norme pour les applications RMS.

Le format PFile est transparent pour le développeur d’applications, car il est intégré dans la conception du SDK Microsoft Rights Management 4.2.

