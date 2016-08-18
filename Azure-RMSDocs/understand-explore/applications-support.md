---
title: Comment les applications prennent en charge Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 16c2dbbce4234f41941bd3fd92d264df0ae685e2
ms.openlocfilehash: 15167c4e7dbe0fd401e198c80524b39e4ded250d


---

# Comment les applications prennent en charge Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Utilisez les informations suivantes pour mieux comprendre comment les applications (comme les applications Office Word, Excel, PowerPoint et Outlook) et les services (comme Exchange et SharePoint) les plus couramment utilisés par vos utilisateurs finaux peuvent utiliser Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] pour protéger les données de votre organisation. 
> [!NOTE]
> Pour vérifier les applications et les versions prises en charge par [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), consultez [Configuration requise pour Azure Rights Management](../get-started/requirements-azure-rms.md).

Dans certains cas, la protection des informations est automatiquement appliquée, conformément aux stratégies que vous configurez. Par exemple, c’est le cas avec les bibliothèques SharePoint, les fichiers classifiés et les règles de transport Exchange. Dans d’autres cas, les utilisateurs doivent appliquer eux-mêmes la protection des informations depuis les applications, soit en sélectionnant un modèle, soit en sélectionnant des options spécifiques. Par exemple, c’est le cas quand les utilisateurs partagent un fichier par messagerie électronique ou protègent un fichier en place en restreignant l’accès ou l’utilisation aux utilisateurs sélectionnés ou aux utilisateurs extérieurs à l’organisation.

Les modèles permettent aux utilisateurs (et administrateurs qui configurent des stratégies) d’appliquer facilement le niveau adéquat de protection et de restreindre l’accès aux personnes internes de l’organisation. Deux modèles par défaut sont livrés avec [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], mais vous voudrez probablement créer des modèles personnalisés pour réduire le temps passé par ces personnes à spécifier des options individuelles. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md).

Quand les utilisateurs doivent appliquer eux-mêmes la protection des informations, veillez à leur fournir des instructions et des conseils sur la manière de le faire et le moment auquel le faire. Ces instructions doivent être appropriées à l’application et aux versions qu’ils utilisent et à la manière dont ils les utilisent. Les conseils sur l’application de la protection des informations doivent refléter votre secteur d’activité. Pour plus d’informations, consultez [Aider les utilisateurs à protéger des fichiers en utilisant Azure Rights Management](../deploy-use/help-users.md).

Pour plus d’informations sur la configuration de ces applications pour Azure RMS, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

> [!TIP]
> Pour des exemples et des captures d’écran d’applications utilisant Azure RMS, consultez [Azure RMS en action : ce que voient les administrateurs et les utilisateurs](what-admins-users-see.md).

Les services de recherche peuvent s’intégrer à Rights Management de différentes manières. Exemple : 

- Exchange Online et Exchange Server utilisent l’indexation côté service pour que les messages électroniques de l’utilisateur protégés par RMS soient affichés automatiquement dans les résultats de la recherche. 

- SharePoint Online et SharePoint Server appliquent la protection RMS aux fichiers uniquement lors du téléchargement, ce qui signifie que l’indexation et les résultats de recherche sur SharePoint ne sont pas affectés par cette solution de protection de document. Toutefois, si vous avez un document que vous souhaitez stocker dans SharePoint et qui ne doit pas être retourné dans les résultats de recherche, RMS protège le fichier avant de le charger vers SharePoint.

- Windows Desktop Search utilise un index partagé entre différents utilisateurs de l’appareil. Ainsi, pour sécuriser les données dans les documents protégés, il n’indexe pas les fichiers protégés par RMS. Cela signifie que même si vos résultats de recherche n’incluent pas les fichiers que vous avez protégés, vous pouvez être sûr que vos fichiers contenant des données sensibles ne seront pas affichés dans les résultats de recherche pour d’autres utilisateurs susceptibles de se connecter à votre PC. 



## Étapes suivantes

Découvrez comment chacun des éléments suivants prend en charge Azure RMS :

-   [Application de partage RMS pour Windows et les plateformes mobiles](sharing-app-support.md)

-   [Applications et services Office](office-apps-services-support.md)

-   [Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)](file-server-support.md)

-   [Autres applications prenant en charge les API RMS](api-support.md)




<!--HONumber=Jul16_HO3-->


