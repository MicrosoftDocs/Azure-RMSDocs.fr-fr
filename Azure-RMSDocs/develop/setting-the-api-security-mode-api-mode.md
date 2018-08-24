---
title: Procédure de définition du mode de sécurité de l’API | Azure RMS
description: Choisissez le mode de sécurité qu’exécute votre application API de fichier.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c6e7d29ac65e9f8494e6aaba8d5e3e2564bd3305
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42808410"
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
