---
title: "Comment déterminer si des utilisateurs se sont inscrits à RMS for Individuals | Azure RMS"
description: "En tant qu’administrateur, utilisez une ou plusieurs des méthodes décrites dans cet article pour déterminer si vos utilisateurs se sont inscrits à RMS for Individuals."
author: cabailey
manager: mbaldwin
ms.date: 09/01/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79d098e47cdfe608bc62ed385a5c8236fb7c6d3c
ms.openlocfilehash: 6a8a6ac7aae7c8e370af47e1d39a9f69acc1e12c


---


# Détermination des utilisateurs inscrits à RMS for Individuals

>*S’applique à : Azure Rights Management*

En tant qu'administrateur, vous souhaitez sûrement savoir si vos utilisateurs se sont inscrits à RMS for individuals. Pour ce faire, utilisez une ou plusieurs des méthodes suivantes :

-   Demandez aux utilisateurs comment ils protègent les fichiers hautement confidentiels, en particulier lorsqu'ils collaborent avec des personnes extérieures à l'organisation.

-   Si vous avez un abonnement Azure pour votre organisation, utilisez l’applet de commande [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) pour voir si **RIGHTSMANAGEMENT_ADHOC** est retourné comme l’un des abonnements. Si c'est le cas, il s'agit de l'abonnement RMS for individuals qui a été accordé à l'organisation, avec un pool d'unités actives disponibles dont les utilisateurs peuvent se servir pour le processus d'inscription libre-service.

-   Utilisez une solution de gestion de système, telle que System Center Configuration Manager, pour dresser l'inventaire des logiciels installés et utilisés. L'application de partage Rights Management s'exécute à l'aide du programme **ipviewer.exe** et vous pouvez [télécharger et installer l'application](http://go.microsoft.com/fwlink/?LinkId=303970) gratuitement pour identifier d'autres caractéristiques de cette application que vous utilisez ensuite pour l'inventaire logiciel.

-   Recherchez les extensions de nom de fichier créées par l'application de partage Rights Management. Les extensions de nom de fichier .pfile et .ppdf sont des exemples évidents, mais d'autres fichiers changent d'extension de nom quand ils font l'objet d'une protection native de Rights Management. Pour plus d’informations, consultez la section [Types de fichiers pris en charge et extensions de nom de fichier](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) du [Guide de l’administrateur de l’application de partage Rights Management](http://technet.microsoft.com/library/dn339003.aspx).




<!--HONumber=Sep16_HO1-->


