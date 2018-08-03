---
title: Formats de fichier pris en charge | Azure RMS
description: La version actuelle de l’API de fichier prend en charge la protection native pour les fichiers Microsoft Office, PDF et la protection PFile pour tous les autres formats de fichier.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EC831494-7F2C-4C70-9063-B02CDDEA14EE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 5dc4cc7a54e7976339ad0def3f2a1d71c8204991
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39369922"
---
# <a name="supported-file-formats"></a>Formats de fichier pris en charge

L’API de fichier prend en charge les formats natif et Pfile.

## <a name="supported-file-formats"></a>Formats de fichier pris en charge

La version actuelle de l’API de fichier prend en charge la protection native pour les fichiers Microsoft Office, PDF (Portable Document Files) et la protection PFile pour tous les autres formats de fichier. Les fichiers PDF peuvent éventuellement avoir une protection PFile.

-   **Protection native**. Dans la protection native, le fichier est chiffré dans un format de fichier AD RMS basé sur son type MIME (extension de nom de fichier). Les fichiers qui sont protégés en mode natif à l’aide de l’API de fichier sont cohérents avec le format attendu par les applications activées pour AD RMS qui utilisent la protection native. Par exemple, Office 2013, Office 2010 et FoxIt PDF reader. La protection native est prise en charge uniquement sur les fichiers Office, les fichiers PDF et un nombre limité d’autres types de fichier. Pour plus d’informations sur les types de fichier sur lesquels la protection native est prise en charge, consultez [Configuration de l’API de fichier](file-api-configuration.md).
-   **Protection PFile**. Dans la protection PFile, les fichiers sont chiffrés à l’aide du format Fichier protégé par AD RMS (PFile). Le fichier est chiffré dans un fichier avec une extension .pfile. La protection PFile est prise en charge pour tous les formats de fichier, à l’exception des fichiers Office.

Les administrateurs peuvent définir des clés de Registre pour déterminer si et comment les fichiers doivent être protégés selon leur extension de nom de fichier. Pour plus d’informations sur la configuration de la protection des fichiers avec l’API de fichier, consultez [Configuration de l’API de fichier](file-api-configuration.md).

## <a name="related-topics"></a>Rubriques connexes

* [Notes pour les développeurs](developer-notes.md)
* [Configuration de l’API de fichier](file-api-configuration.md)
 