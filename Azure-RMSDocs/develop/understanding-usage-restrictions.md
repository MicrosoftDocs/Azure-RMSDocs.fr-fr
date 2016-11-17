---
title: "Présentation des restrictions d’utilisation | Azure RMS"
description: "Toutes les applications prenant en charge RMS doivent appliquer des restrictions d’utilisation."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: cc383728d487cac45e59ef34ca43ba47c4db237b


---

# <a name="understanding-usage-restrictions"></a>Comprendre les restrictions d’utilisation

Toutes les applications prenant en charge RMS doivent appliquer des restrictions d’utilisation. Une restriction d’utilisation est une condition qui se produit quand un utilisateur tente d’effectuer une action (par exemple, imprimer d’un document), alors que la stratégie RMS pour ce document ne lui accorde pas l’autorisation ou le droit nécessaire pour mener à bien cette action (par exemple, le droit PRINT).

Il est possible d’interroger les autorisations dont dispose un utilisateur sur un document à l’aide de la fonction [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx).

## <a name="understanding-usage-restrictions"></a>Comprendre les restrictions d’utilisation

-   Se familiariser avec les droits RMS standard

    Pour connaître l’ensemble des droits RMS que peut appliquer votre application, consultez [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md).

    Notez que vous pouvez créer des droits définis par l’application qui sont propres à votre situation et qui vont au-delà des droits RMS standards.

-   Identifier les points de mise en œuvre de restriction d’utilisation

    Un *point de mise en œuvre de restriction d’utilisation* est un emplacement dans le flux de contrôle de votre application où vous devez mettre en œuvre une restriction d’utilisation. La rubrique [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md) fournit plusieurs exemples de points de mise en œuvre courants.

    Évaluez votre propre application pour déterminer les points de mise en œuvre de restriction d’utilisation qui s’appliquent.

    Votre application n’a peut-être pas besoin de tous les points de mise en œuvre décrits dans [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md). Par exemple, si votre application n’autorise pas les utilisateurs à imprimer du contenu, il est inutile de vérifier le droit **IPC\_GENERIC\_PRINT**.

-   Mettre à jour le code pour effectuer une vérification d’accès à chaque point de mise en œuvre

    Pour obtenir des conseils sur la mise en œuvre de droits spécifiques, consultez [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md).

## <a name="related-topics"></a>Rubriques connexes

* [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx)
* [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md)
 

 



<!--HONumber=Nov16_HO2-->


