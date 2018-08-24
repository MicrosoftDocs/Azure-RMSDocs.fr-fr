---
title: Client Azure Information Protection &colon; installation et configuration
description: Informations destinées aux administrateurs sur le déploiement du client Azure Information Protection sur les ordinateurs et appareils mobiles Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 206ebd5ddfae1644609a343cb3e6d7805342aad0
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42803258"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Client Azure Information Protection : installation et configuration pour les clients

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les ordinateurs qui exécutent Office 2010 exigent que le client Azure Information Protection (ou l’application de partage Rights Management) s’authentifie auprès du service Azure Rights Management et le service Azure Information Protection. Ce client est également recommandé pour tous les ordinateurs Windows et les appareils iOS et Android qui prennent en charge le service Azure Rights Management et Azure Information Protection. 

Le client Azure Information Protection s’intègre aux applications Office grâce à l’installation d’un complément Office, afin de permettre aux utilisateurs d’étiqueter et de protéger facilement des documents et des e-mails directement depuis le ruban Office. Ce client offre également un étiquetage et une protection pour les types de fichiers qui ne sont pas pris en charge de manière native par le service Azure Rights Management, une visionneuse de fichiers protégés et un site de suivi de documents permettant aux utilisateurs de suivre et de révoquer les fichiers qu’ils ont protégés.

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Le client Azure Information Protection pour Windows : installation et configuration
Pour une installation et une configuration du client en entreprise pour Windows, consultez le [Guide de l’administrateur Azure Information Protection](./rms-client/client-admin-guide.md).

> [!TIP]
> Si vous souhaitez installer et tester rapidement le client Azure Information Protection pour un seul ordinateur, consultez [Télécharger et installer le client Azure Information Protection](./rms-client/install-client-app.md) à partir du [Guide de l’utilisateur du client Azure Information Protection](./rms-client/client-user-guide.md).

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>Le client Azure Information Protection pour iOS et Android : installation et gestion
Pour installer le client Azure Information Protection pour ces plateformes mobiles populaires, vous pouvez télécharger l’application correspondante à l’aide des liens de la [page Microsoft Azure Information Protection](http://go.microsoft.com/fwlink/?LinkId=303970). Aucune action de configuration n'est requise.

> [!NOTE]
> Pour les ordinateurs Mac et Windows Phone, les liens de cette page téléchargent des applications de partage RMS pour appareils mobiles. Actuellement, ces appareils ne prennent pas en charge le client Azure Information Protection client.

**Si vous avez Microsoft Intune** : comme l’application Azure Information Protection comprend le SDK d’application Microsoft Intune, quand les appareils iOS et Android sont inscrits par Intune, vous pouvez déployer et gérer la visionneuse Azure Information Protection pour ces appareils. Pour plus d’informations, consultez [Configurer et déployer des stratégies de gestion des applications mobiles dans la console Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) dans la documentation Intune. Pour l’étape 2, suivez les instructions pour publier une application gérée par une stratégie.



