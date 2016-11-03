---
title: "Procédure de définition du mode de sécurité de l’API | Azure RMS"
description: "Choisissez le mode de sécurité qu’exécute votre application API de fichier."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 77e2dfe7f2afb1e70de658850f83f86e9224aea6
ms.openlocfilehash: 9235fa1c194162689b854493ea31e76c08c40ce7


---

# Comment : définir le mode de sécurité de l’API

Vous pouvez choisir le mode de sécurité qu’exécute votre application API de fichier à l’aide de la fonction [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

Pour initialiser votre application pour qu’elle s’exécute en *mode serveur*, appelez la fonction [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) et choisissez le mode de sécurité [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx). Par défaut, votre application s’exécute en *mode client*, **IPC\_API\_MODE\_CLIENT**.

Pour plus d’informations sur le *mode serveur*, consultez [Application types](application-types.md) (Types d’applications).

**Important**  Le mode de sécurité doit être défini avant d’appeler toute autre fonction Rights Management Services SDK 2.1. Une fois que le mode de sécurité a été défini, il ne peut plus être modifié pour le processus en cours.

## Rubriques connexes

* [Application types (Types d’applications)](application-types.md)
* [API mode values (Valeurs de mode de l’API)](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
 

 



<!--HONumber=Oct16_HO3-->


