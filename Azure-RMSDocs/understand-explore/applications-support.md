---
title: "Mode de prise en charge des applications par Azure Rights Management - AIP"
description: "Découvrez comment les applications (comme Office Word, Excel, PowerPoint et Outlook) et les services (comme Exchange et SharePoint) les plus couramment utilisés par vos utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les documents et e-mails de votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: db9f67c5baeea678bf288f4f10237ff4517d905b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>Comment les applications prennent en charge le service Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Utilisez les informations suivantes pour comprendre comment les applications (comme Office Word, Excel, PowerPoint et Outlook) et les services (comme Exchange et SharePoint) les plus couramment utilisés par vos utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les documents et e-mails de votre organisation. 
> [!NOTE]
> Pour vérifier les applications et les versions prises en charge par le service Azure Rights Management, consultez [Applications prenant en charge la protection des données Azure Rights Management](../get-started/requirements-applications.md).

Dans certains cas, le service Azure Rights Management applique automatiquement la protection, en fonction des stratégies configurées par les administrateurs. C’est le cas, par exemple, avec les bibliothèques SharePoint et les règles de transport Exchange. Dans d’autres cas, les utilisateurs finaux doivent eux-mêmes appliquer la protection des informations à partir de leurs applications, par exemple, en sélectionnant une étiquette de classification configurée pour appliquer un modèle, en sélectionnant directement un modèle, ou en sélectionnant des options spécifiques. La protection appliquée par les utilisateurs est standard lorsqu’ils décident de protéger un fichier à partager et de restreindre l’accès ou l’utilisation aux utilisateurs sélectionnés ou à des utilisateurs en dehors de l’organisation.

Les modèles permettent aux utilisateurs (et administrateurs qui configurent des stratégies) d’appliquer facilement le niveau adéquat de protection et de restreindre l’accès aux personnes internes de l’organisation. Deux modèles par défaut sont livrés avec le service Azure Rights Management, mais vous voudrez probablement créer des modèles personnalisés pour réduire le temps passé par ces personnes à spécifier des options individuelles. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md).

Quand les utilisateurs doivent appliquer eux-mêmes la protection des informations, veillez à leur fournir des instructions et des conseils sur la manière de le faire et le moment auquel le faire. Ces instructions doivent être appropriées à l’application et aux versions qu’ils utilisent et à la manière dont ils les utilisent. Les conseils sur l’application de la protection des informations doivent refléter votre secteur d’activité. Pour plus d’informations, consultez [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](../deploy-use/help-users.md).

Pour plus d’informations sur la configuration de ces applications pour le service Azure Rights Management d’Azure Information Protection, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

Les services de recherche peuvent s’intégrer à Rights Management de différentes manières. Exemple : 

- Exchange Online et Exchange Server utilisent l’indexation côté service pour que les messages électroniques de l’utilisateur protégés par RMS soient affichés automatiquement dans les résultats de la recherche. 

- SharePoint Online et SharePoint Server appliquent la protection Rights Management aux fichiers uniquement pendant le téléchargement, ce qui signifie que l’indexation et les résultats de recherche sur SharePoint ne sont pas affectés par cette solution de protection de document. Toutefois, si vous avez un document que vous souhaitez stocker dans SharePoint et qui ne doit pas être retourné dans les résultats de recherche, RMS protège le fichier avant de le charger vers SharePoint.

- Windows Desktop Search utilise un index partagé entre différents utilisateurs de l’appareil. Ainsi, pour sécuriser les données dans les documents protégés, il n’indexe pas les fichiers protégés par RMS. Cela signifie que même si vos résultats de recherche n’incluent pas les fichiers que vous avez protégés, vous pouvez être sûr que vos fichiers contenant des données sensibles ne seront pas affichés dans les résultats de recherche pour d’autres utilisateurs susceptibles de se connecter à votre PC. 



## <a name="next-steps"></a>Étapes suivantes

Découvrez comment chacun des éléments suivants prend en charge le service Azure Rights Management :

-   [Application de partage RMS pour Windows et les plateformes mobiles](sharing-app-support.md)

-   [Applications et services Office](office-apps-services-support.md)

-   [Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)](file-server-support.md)

-   [Autres applications prenant en charge les API RMS](api-support.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
