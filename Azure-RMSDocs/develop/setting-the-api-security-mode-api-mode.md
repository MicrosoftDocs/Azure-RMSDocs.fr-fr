---
# required metadata

title: Procédure de définition du mode de sécurité de l’API | Azure RMS
description: Choisissez le mode de sécurité qu’exécute votre application API de fichier.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Comment : définir le mode de sécurité de l’API

Vous pouvez choisir le mode de sécurité qu’exécute votre application API de fichier à l’aide de la fonction [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

Pour initialiser votre application pour qu’elle s’exécute en *mode serveur*, appelez la fonction [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) et choisissez le mode de sécurité [**IPC\_API\_MODE\_SERVER**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER). Par défaut, votre application s’exécute en *mode client*, **IPC\_API\_MODE\_CLIENT**.

Pour plus d’informations sur le *mode serveur*, consultez [Application types](application-types.md) (Types d’applications).

**Important**  Le mode de sécurité doit être défini avant d’appeler toute autre fonction Rights Management Services SDK 2.1. Une fois que le mode de sécurité a été défini, il ne peut plus être modifié pour le processus en cours.

## Rubriques connexes

* [Application types (Types d’applications)](application-types.md)
* [**API mode values (Valeurs de mode de l’API)**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 


<!--HONumber=Jun16_HO2-->


