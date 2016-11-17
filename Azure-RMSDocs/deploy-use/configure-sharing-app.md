---
title: Application de partage Rights Management&colon; Installation et configuration pour les clients | Azure Information Protection
description: "Informations destinées aux administrateurs sur le déploiement de l’application de partage Rights Management (RMS) sur les ordinateurs et appareils mobiles Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: f96641355da46eee85a828a6e5e417282883bac7


---

# <a name="rights-management-sharing-application-installation-and-configuration-for-clients"></a>Application de partage Rights Management : installation et configuration pour les clients

>*S’applique à : Azure Information Protection, Office 365*

L’application de partage Rights Management (RMS) est requise pour permettre aux ordinateurs client d’utiliser le service Azure Rights Management avec Office 2010, et est recommandée pour tous les ordinateurs et appareils mobiles prenant en charge le service Azure Rights Management d’Azure Information Protection. L'application de partage RMS s'intègre aux applications Office via l'installation d'un complément Office, afin de permettre aux utilisateurs de protéger facilement des fichiers et e-mails directement depuis le ruban. Elle offre également une protection générique pour les types de fichiers qui ne sont pas pris en charge de manière native par le service Azure Rights Management, et un site de suivi de documents permettant aux utilisateurs de suivre et de révoquer les fichiers qu’ils ont protégés.

## <a name="the-rms-sharing-application-for-windows-installation-and-configuration"></a>Application de partage RMS pour Windows : installation et configuration
Pour installer et configurer l’application de partage RMS pour Windows pour un déploiement d’entreprise, consultez le [guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Si vous souhaitez installer et tester rapidement l’application de partage RMS sur un ordinateur unique, consultez la rubrique [Téléchargement et installation de l’application de partage Rights Management](../rms-client/install-sharing-app.md) du [guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md).

## <a name="the-rms-sharing-application-for-mobile-platforms-installation-and-management"></a>Application de partage RMS pour plateformes mobiles : installation et gestion
Pour installer l'application de partage RMS pour plateformes mobiles, vous pouvez télécharger l'application correspondante grâce aux liens de la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). Aucune configuration n’est requise pour utiliser le service Azure Rights Management avec cette application.

> [!NOTE]
> L’application de partage RMS pour iOS et Android est maintenant remplacée par l’application Azure Information Protection.

**Si vous avez Microsoft Intune** : comme l’application Azure Information Protection comprend le SDK d’application Microsoft Intune, quand les appareils iOS et Android sont inscrits par Intune, vous pouvez déployer et gérer l’application Azure Information Protection pour ces appareils. Pour plus d’informations, consultez [Configurer et déployer des stratégies de gestion des applications mobiles dans la console Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) dans la documentation Intune. Pour l’étape 2, suivez les instructions pour publier une application gérée par une stratégie.






<!--HONumber=Nov16_HO2-->


