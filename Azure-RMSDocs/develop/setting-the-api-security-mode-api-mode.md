---
title: Procédure de définition du mode de sécurité de l’API | Azure RMS
description: Découvrez comment définir le mode de sécurité de l’API à l’aide de la fonction IpcSetGlobalProperty pour choisir le mode de sécurité dans lequel s’exécute votre application API de fichier.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 942192690e06422246fa0ed7a4fb2d1d3ccf6cd6
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563598"
---
# <a name="how-to-set-the-api-security-mode"></a>Comment : définir le mode de sécurité de l’API

Vous pouvez choisir le mode de sécurité qu’exécute votre application API de fichier à l’aide de la fonction [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

Pour initialiser votre application pour qu’elle s’exécute en *mode serveur*, appelez la fonction [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) et choisissez le mode de sécurité [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx). Par défaut, votre application s’exécute en *mode client*, ** \_ \_ \_ client en mode d’API IPC**.

Pour plus d’informations sur le *mode serveur*, consultez [Application types](application-types.md) (Types d’applications).

**Important**    Le mode de sécurité doit être défini avant l’appel de toute autre fonction de Rights Management Services SDK 2,1. Une fois que le mode de sécurité a été défini, il ne peut plus être modifié pour le processus en cours.

## <a name="related-topics"></a>Rubriques connexes

* [Types d’applications](application-types.md)
* [Valeurs de mode de l’API](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
