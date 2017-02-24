---
title: "Comment déterminer si des utilisateurs se sont inscrits à RMS for Individuals | Azure Information Protection"
description: "En tant qu&quot;administrateur, vous souhaitez sûrement savoir si vos utilisateurs se sont inscrits à RMS for individuals. Vous pouvez utiliser l’une des méthodes décrites dans cet article ou une combinaison de ces méthodes."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ffed64826982756072456be18cced0226b6bb6cc
ms.openlocfilehash: 5dae8412277be37cd3ff8cfe76c71a8109277146


---


# <a name="how-to-find-out-if-your-users-have-signed-up-for-rms-for-individuals"></a>Détermination des utilisateurs inscrits à RMS for Individuals

>*S’applique à : Azure Information Protection*

En tant qu'administrateur, vous souhaitez sûrement savoir si vos utilisateurs se sont inscrits à RMS for individuals. Pour ce faire, utilisez une ou plusieurs des méthodes suivantes :

-   Demandez aux utilisateurs comment ils protègent les fichiers hautement confidentiels, en particulier lorsqu'ils collaborent avec des personnes extérieures à l'organisation.

-   Si vous avez un abonnement Azure pour votre organisation, utilisez l’applet de commande [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) pour voir si la licence **RIGHTSMANAGEMENT_ADHOC** est affectée à des utilisateurs. La licence est issue de l’abonnement RMS for individuals qui a été accordé à l’organisation, avec un pool d’unités actives disponibles dont les utilisateurs peuvent se servir pour le processus d’inscription libre-service.

-   Utilisez une solution de gestion de système, telle que System Center Configuration Manager, pour dresser l'inventaire des logiciels installés et utilisés. Par exemple, recherchez **MSIP. App.exe**, qui est utilisé par le client Azure Information Protection, et **ipviewer.exe** pour l’application de partage Rights Management. Vous pouvez télécharger et installer ce client et cette application gratuitement pour identifier d’autres caractéristiques que vous utiliserez ensuite pour l’inventaire logiciel.

-   Recherchez les extensions de nom de fichier créées par le client Azure Information Protection et l’application de partage Rights Management. Les extensions de nom de fichier .pfile et .ppdf sont les exemples les plus évidents, mais d’autres fichiers changent d’extension de nom de fichier quand ils sont protégés nativement par le service Rights Management. Pour plus d’informations, consultez la section [Types de fichiers pris en charge pour la protection](../rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) dans le guide de l’administrateur du client Azure Information Protection.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


