---
title: "Présentation des restrictions d’utilisation | Azure RMS"
description: "Toutes les applications prenant en charge RMS doivent appliquer des restrictions d’utilisation."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: df210bd7aff33fda41a278e6aed1108574fe68eb


---

# Comprendre les restrictions d’utilisation

Toutes les applications prenant en charge RMS doivent appliquer des restrictions d’utilisation. Une restriction d’utilisation est une condition qui se produit quand un utilisateur tente d’effectuer une action (par exemple, imprimer d’un document), alors que la stratégie RMS pour ce document ne lui accorde pas l’autorisation ou le droit nécessaire pour mener à bien cette action (par exemple, le droit PRINT).

Il est possible d’interroger les autorisations dont dispose un utilisateur sur un document à l’aide de la fonction [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck).

## Comprendre les restrictions d’utilisation

-   Se familiariser avec les droits RMS standard

    Pour connaître l’ensemble des droits RMS que peut appliquer votre application, consultez [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md).

    Notez que vous pouvez créer des droits définis par l’application qui sont propres à votre situation et qui vont au-delà des droits RMS standards.

-   Identifier les points de mise en œuvre de restriction d’utilisation

    Un *point de mise en œuvre de restriction d’utilisation* est un emplacement dans le flux de contrôle de votre application où vous devez mettre en œuvre une restriction d’utilisation. La rubrique [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md) fournit plusieurs exemples de points de mise en œuvre courants.

    Évaluez votre propre application pour déterminer les points de mise en œuvre de restriction d’utilisation qui s’appliquent.

    Votre application n’a peut-être pas besoin de tous les points de mise en œuvre décrits dans [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md). Par exemple, si votre application n’autorise pas les utilisateurs à imprimer du contenu, il est inutile de vérifier le droit **IPC\_GENERIC\_PRINT**.

-   Mettre à jour le code pour effectuer une vérification d’accès à chaque point de mise en œuvre

    Pour obtenir des conseils sur la mise en œuvre de droits spécifiques, consultez [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md).

## Rubriques connexes

* [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck)
* [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md)
 

 



<!--HONumber=Aug16_HO4-->


