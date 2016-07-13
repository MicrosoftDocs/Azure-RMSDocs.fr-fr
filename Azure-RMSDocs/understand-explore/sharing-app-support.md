---
title: Application de partage RMS pour Windows et les plateformes mobiles | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 02f1cf60bdafe748f16d9defa1c8b0cc8a61efb0


---


# Application de partage RMS pour Windows et les plateformes mobiles

*S’applique à : Azure Rights Management, Office 365*

L’application de partage RMS est une application téléchargeable gratuitement qui est nécessaire pour prendre en charge Office 2010, mais également recommandée pour les ordinateurs Windows et Mac, ainsi que les appareils mobiles. L’un de ses avantages est qu’elle est capable d’appliquer une protection générique aux applications et fichiers qui ne prennent pas en charge [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] de manière native, ce qui signifie que tous les fichiers peuvent être protégés. Pour plus d’informations sur les différents niveaux de protection, voir la section [Niveaux de protection : natif et générique](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) du [Guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).

Lorsque les utilisateurs protègent leurs fichiers à l’aide de l’application de partage RMS, ils peuvent également suivre les documents protégés et, si nécessaire, révoquer l’accès à ceux-ci. Ils doivent pour cela utiliser le [site de suivi des documents](http://go.microsoft.com/fwlink/?LinkId=529562).

Pour les ordinateurs Windows, l’application de partage RMS s’intègre discrètement dans les applications que les utilisateurs utilisent déjà et ainsi les améliorent :

-   Un complément Office pour Word, Excel, PowerPoint et Outlook est installé. Il fournit aux utilisateurs un bouton **Partage protégé** sur le ruban, qui permet d’appeler une boîte de dialogue pratique de paramètres couramment utilisés pour protéger des fichiers à envoyer par e-mail. Ce bouton fournit également un moyen rapide d’accéder au site de suivi des documents.

-   Une nouvelle option par clic droit pour l’Explorateur de fichiers. Celle-ci fournit aux utilisateurs une option **Protéger sur place**, qui permet d’appeler une boîte de dialogue pratique de paramètres couramment utilisés pour protéger des fichiers stockés sur un disque.

-   Une visionneuse pour ouvrir des fichiers qui ont été protégés par [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Cette visionneuse est automatiquement appelée quand aucune autre application installée n’est capable d’ouvrir le fichier protégé.

-   Une configuration principale d’Office 2010 qui permet à Word, Excel, PowerPoint et Outlook inclus dans cette suite de fonctionner de manière transparente avec [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

Bien que l’application de partage RMS pour Windows puisse être téléchargée et installée pour un seul ordinateur via la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970), elle prend également en charge un déploiement d’entreprise avec une installation sans assistance et une configuration personnalisée. Pour plus d’informations, consultez les ressources suivantes :

-   [Guide de l’administrateur sur l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md)

L’application de partage RMS pour les appareils mobiles prend en charge les appareils mobiles les plus couramment utilisés, comme les iPad et iPhone, les appareils Android, Windows Phone et Windows RT. Les utilisateurs peuvent télécharger cette application auprès de la boutique adéquate. Des liens vers celle-ci sont également disponibles dans la [page Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970).

**Si vous disposez de Microsoft Intune** : Étant donné que l’application de partage RMS comprend le Kit de développement logiciel de l’application Microsoft Intune, vous pouvez utiliser les options suivantes :

-   Déployer et gérer l’application pour les appareils iOS et Android inscrits par Intune.

-   Gérer l’application pour les appareils Android non inscrits par Intune.


## Étapes suivantes
Pour voir comment d’autres applications et services prennent en charge Azure Rights Management, consultez [Comment les applications prennent en charge Azure Rights Management](applications-support.md).




<!--HONumber=Jun16_HO4-->


