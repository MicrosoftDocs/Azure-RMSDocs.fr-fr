---
# required metadata

title: Application de partage Rights Management &colon; installation et configuration pour les clients | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Application de partage Rights Management : installation et configuration pour les clients

*S’applique à : Azure Rights Management, Office 365*

L'application de partage Rights Management (RMS) est requise pour permettre aux ordinateurs client d'utiliser Azure RMS avec Office 2010, et est recommandée pour tous les ordinateurs et appareils mobiles prenant en charge Azure RMS. L'application de partage RMS s'intègre aux applications Office via l'installation d'un complément Office, afin de permettre aux utilisateurs de protéger facilement des fichiers et e-mails directement depuis le ruban. Elle offre également une protection générique pour les types de fichiers qui ne sont pas pris en charge de manière native par Azure RMS, et un site de suivi de documents permettant aux utilisateurs de suivre et de révoquer les fichiers qu'ils ont protégés.

## Application de partage RMS pour Windows : installation et configuration
Pour installer et configurer l’application de partage RMS pour Windows pour un déploiement d’entreprise, consultez le [guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Si vous souhaitez installer et tester rapidement l’application de partage RMS sur un ordinateur unique, consultez la rubrique [Téléchargement et installation de l’application de partage Rights Management](../rms-client/install-sharing-app.md) du [guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md).

## Application de partage RMS pour plateformes mobiles : Installation et gestion
Pour installer l'application de partage RMS pour plateformes mobiles, vous pouvez télécharger l'application correspondante grâce aux liens de la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). Aucune configuration n'est requise pour l'utilisation d'Azure RMS avec cette application.

**Si vous disposez de Microsoft Intune** : étant donné que l’application de partage RMS comprend le Kit de développement logiciel de l’application Microsoft Intune, vous avez les options suivantes :

-   Pour les appareils qui sont inscrits par Intune, vous pouvez déployer et gérer l’application de partage RMS pour des appareils qui exécutent iOS et Android. Pour plus d’informations, consultez [Configurer et déployer des stratégies de gestion des applications mobiles dans la console Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) dans la documentation Intune. Pour l’étape 2, suivez les instructions pour publier une application gérée par une stratégie.

-   Pour les appareils qui ne sont pas inscrits par Intune, vous pouvez gérer l’application de partage RMS pour des appareils qui exécutent Android. Pour plus d’informations, consultez [Créer et déployer des stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune).



<!--HONumber=Apr16_HO4-->


