---
title: "Conditions d’utilisation | Azure RMS"
description: "Collection de définitions propres aux services Rights Management."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 5779cc10503ad7afe997e031a467021b513fc510


---

# Conditions d'utilisation

Collection de définitions propres aux services Rights Management.

**Algorithme déconseillé**  
Paramètre modal qui implémente un ancien schéma de protection de contenu, se référant en particulier au mode de chiffrement ECB (Electronic CookBook). Dans ce SDK, le paramètre vous permet de générer des licences compatibles avec la bibliothèque MSDRM utilisée par le Kit [AD Rights Management SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx).

Ce paramètre peut inciter l’application à protéger le contenu non conformément aux normes de vos clients pour la protection de contenu.

Ce paramètre empêche votre application de tirer parti des améliorations de chiffrement ajoutées à Microsoft Rights Management SDK 3.0 ou ultérieur.

**Format de fichier protégé de Microsoft**

Ce format, également appelé PFile, est le format de fichier par défaut pour AD RMS qui fait office de norme pour les applications RMS.

Le format PFile est transparent pour le développeur d’applications, car il est intégré dans la conception de Microsoft Rights Management SDK 4.2.

 

 






<!--HONumber=Jul16_HO3-->


