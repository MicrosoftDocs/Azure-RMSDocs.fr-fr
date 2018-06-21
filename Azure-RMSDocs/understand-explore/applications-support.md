---
title: Prise en charge d’Azure Rights Management par les applications à partir d’AIP
description: Découvrez comment les applications (comme Office Word, Excel, PowerPoint et Outlook) et les services (comme Exchange et SharePoint) les plus couramment utilisés par vos utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les documents et e-mails de votre organisation.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: af3d103908aff785d48f70cc1cf89a7b9d17643e
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
ms.locfileid: "30207816"
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>Comment les applications prennent en charge le service Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations suivantes pour comprendre comment les applications et les services les plus couramment utilisés par vos utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les documents et les e-mails de votre organisation. Ces applications incluent Word, Excel, PowerPoint et Outlook. Les services incluent Exchange et SharePoint.

> [!NOTE]
> Pour vérifier les applications et les versions prises en charge par le service Azure Rights Management, consultez [Applications prenant en charge la protection des données Azure Rights Management](../get-started/requirements-applications.md).

Dans certains cas, le service Azure Rights Management applique automatiquement la protection, en fonction des stratégies configurées par les administrateurs. C’est le cas, par exemple, avec les bibliothèques SharePoint et les règles de transport Exchange. Dans d’autres cas, les utilisateurs finaux doivent appliquer eux-mêmes la protection à partir de leurs applications. Par exemple, les utilisateurs sélectionnent une étiquette de classification qui est configurée pour appliquer la protection, ou ils sélectionnent un modèle ou des options spécifiques. La protection appliquée par les utilisateurs est classique quand ils décident de protéger un fichier à partager, et quand ils limitent également l’accès ou l’utilisation à des utilisateurs sélectionnés ou à des utilisateurs en dehors de l’organisation.

Les modèles permettent aux utilisateurs (et administrateurs qui configurent des stratégies) d’appliquer facilement le niveau adéquat de protection et de restreindre l’accès aux personnes internes de l’organisation. Deux modèles par défaut sont livrés avec le service Azure Rights Management, mais vous voudrez probablement créer des modèles personnalisés pour réduire le temps passé par les utilisateurs et les administrateurs à spécifier des options individuelles. Pour plus d’informations sur les modèles, consultez [Configuration et gestion des modèles pour Azure Information Protection](../deploy-use/configure-policy-templates.md).

Pour les cas où les utilisateurs doivent appliquer eux-mêmes la protection, veillez à leur fournir des instructions et des conseils sur la façon et le moment de le faire. Fournissez des instructions spécifiques pour l’application et les versions qu’ils utilisent et la façon dont ils les utilisent. Fournissez également des conseils sur le moment et la façon dont les utilisateurs doivent appliquer la protection qui convient à votre entreprise. Pour plus d’informations, consultez [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](../deploy-use/help-users.md).

Pour plus d’informations sur la configuration de ces applications pour le service Azure Rights Management d’Azure Information Protection, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

Les services de recherche peuvent s’intégrer à Rights Management de différentes manières. Par exemple : 

- Exchange Online et Exchange Server utilisent l’indexation côté service pour que les e-mails protégés de l’utilisateur soient affichés automatiquement dans les résultats de la recherche. 

- SharePoint Online et SharePoint Server appliquent la protection Rights Management aux fichiers seulement lors du téléchargement. Cette implémentation signifie que les résultats de l’indexation et de la recherche sur SharePoint ne sont pas affectés par cette solution de protection des documents. Cependant, si vous avez un document que vous voulez stocker dans SharePoint et que ce document ne doit pas être retourné dans les résultats de la recherche, protégez le document avant de le charger dans SharePoint.

- Windows Desktop Search utilise un index partagé entre différents utilisateurs de l’appareil. Ainsi, pour sécuriser les données dans les documents protégés, il n’indexe pas les fichiers protégés. Cela signifie que même si vos résultats de recherche n’incluent pas les fichiers que vous avez protégés, vous pouvez être sûr que vos fichiers contenant des données sensibles ne seront pas affichés dans les résultats de recherche pour d’autres utilisateurs susceptibles de se connecter à votre PC. 

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment chacun des services ou applications suivants prend en charge le service Azure Rights Management :

-   [Application de partage RMS pour Windows et les plateformes mobiles](sharing-app-support.md)

-   [Applications et services Office](office-apps-services-support.md)

-   [Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)](file-server-support.md)

-   [Autres applications prenant en charge les API RMS](api-support.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
