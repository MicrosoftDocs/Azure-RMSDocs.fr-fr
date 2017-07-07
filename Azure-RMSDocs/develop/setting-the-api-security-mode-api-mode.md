---
title: "Procédure de définition du mode de sécurité de l’API | Azure RMS"
description: "Choisissez le mode de sécurité qu’exécute votre application API de fichier."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 5ad73cdb72957425ce71f77ba3d11ec457a4f72f
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-set-the-api-security-mode"></a>Comment : définir le mode de sécurité de l’API

Vous pouvez choisir le mode de sécurité qu’exécute votre application API de fichier à l’aide de la fonction [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

Pour initialiser votre application pour qu’elle s’exécute en *mode serveur*, appelez la fonction [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) et choisissez le mode de sécurité [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx). Par défaut, votre application s’exécute en *mode client*, **IPC\_API\_MODE\_CLIENT**.

Pour plus d’informations sur le *mode serveur*, consultez [Application types](application-types.md) (Types d’applications).

**Important**  Le mode de sécurité doit être défini avant d’appeler toute autre fonction Rights Management Services SDK 2.1. Une fois que le mode de sécurité a été défini, il ne peut plus être modifié pour le processus en cours.

## <a name="related-topics"></a>Rubriques connexes

* [Types d’applications](application-types.md)
* [Valeurs de mode de l’API](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]