---
title: "Application de partage RMS pour Windows et les plateformes mobiles - AIP"
description: "Découvrez comment l’application de partage RMS prend en charge Azure RMS. L’application de partage RMS est une application téléchargeable gratuitement qui est nécessaire pour prendre en charge Office 2010, mais également recommandée pour les ordinateurs Windows et Mac, ainsi que les appareils mobiles."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3c96d8718f42dcedebba03354c149bb2b9667d66
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="rms-sharing-application-for-windows-and-mobile-platforms"></a>Application de partage RMS pour Windows et les plateformes mobiles

>*S’applique à : Azure Information Protection, Office 365*

> [!IMPORTANT]
> **Notification de fin de prise en charge** : l’application de partage Rights Management pour Windows est remplacée par le [client Azure Information Protection](../rms-client/aip-client.md). La prise en charge de cette application plus ancienne cessera le 31 janvier 2018. 
 
L’application de partage RMS est une application téléchargeable gratuitement prenant en charge Office 2010, qui était recommandée pour les ordinateurs Windows, ainsi que les appareils mobiles. Elle reste recommandée pour les ordinateurs Mac et les appareils Windows Phone. L’un de ses avantages est qu’elle est capable d’appliquer une protection générique aux applications et fichiers qui ne prennent pas en charge le service Azure Rights Management de manière native, ce qui signifie que tous les fichiers peuvent être protégés. Pour plus d’informations sur les différents niveaux de protection, voir la section [Niveaux de protection : natif et générique](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection--native-and-generic) du [Guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).

Lorsque les utilisateurs protègent leurs fichiers à l’aide de l’application de partage RMS, ils peuvent également suivre les documents protégés et, si nécessaire, révoquer l’accès à ceux-ci. Ils doivent pour cela utiliser le [site de suivi des documents](http://go.microsoft.com/fwlink/?LinkId=529562).

Pour les ordinateurs Windows, l’application de partage RMS s’intègre discrètement dans les applications que les utilisateurs utilisent déjà et ainsi les améliorent :

-   Un complément Office pour Word, Excel, PowerPoint et Outlook est installé. Il fournit aux utilisateurs un bouton **Partage protégé** sur le ruban, qui permet d’appeler une boîte de dialogue pratique de paramètres couramment utilisés pour protéger des fichiers à envoyer par e-mail. Ce bouton fournit également un moyen rapide d’accéder au site de suivi des documents.

-   Une nouvelle option par clic droit pour l’Explorateur de fichiers. Celle-ci fournit aux utilisateurs une option **Protéger sur place**, qui permet d’appeler une boîte de dialogue pratique de paramètres couramment utilisés pour protéger des fichiers stockés sur un disque.

-   Une visionneuse pour ouvrir les fichiers qui ont été protégés par le service Azure Rights Management. Cette visionneuse est automatiquement appelée quand aucune autre application installée n’est capable d’ouvrir le fichier protégé.

-   Une configuration principale d’Office 2010 qui permet à Word, Excel, PowerPoint et Outlook inclus dans cette suite de fonctionner de manière transparente avec le service Azure Rights Management.

Bien que l’application de partage RMS pour Windows puisse être téléchargée et installée pour un seul ordinateur via la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970), elle prend également en charge un déploiement d’entreprise avec une installation sans assistance et une configuration personnalisée. Pour plus d'informations, consultez les ressources suivantes :

-   [Guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md)

L’application de partage RMS pour les appareils mobiles prend en charge les appareils mobiles les plus couramment utilisés, comme les iPad et iPhone, les appareils Android, Windows Phone et Windows RT. Les utilisateurs peuvent télécharger cette application auprès de la boutique adéquate. Des liens vers celle-ci sont également disponibles dans la [page Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970).

**Si vous disposez de Microsoft Intune** : Étant donné que l’application de partage RMS comprend le Kit de développement logiciel de l’application Microsoft Intune, vous pouvez utiliser les options suivantes :

-   Déployer et gérer l’application pour les appareils iOS et Android inscrits par Intune.

-   Gérer l’application pour les appareils Android non inscrits par Intune.


## <a name="next-steps"></a>Étapes suivantes
Pour voir comment d’autres applications et services prennent en charge le service Azure Rights Management d’Azure Information Protection, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
