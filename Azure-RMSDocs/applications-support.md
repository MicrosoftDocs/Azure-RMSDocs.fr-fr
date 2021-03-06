---
title: Prise en charge d’Azure Rights Management par les applications à partir d’AIP
description: Découvrez comment les applications les plus couramment utilisées (telles que les applications Office) et les services (tels qu’Exchange et SharePoint) peuvent utiliser le service Azure Rights Management de Azure Information Protection pour protéger les documents et e-mails de votre organisation.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5ee04997191002a9b20b97c52573834483eb8813
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383990"
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>Comment les applications prennent en charge le service Azure Rights Management

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). *

Utilisez les informations suivantes pour vous aider à comprendre comment les applications et services les plus couramment utilisés par les utilisateurs finaux peuvent utiliser le service Azure Rights Management de Azure Information Protection pour protéger les documents et e-mails de votre organisation. Ces applications incluent Word, Excel, PowerPoint et Outlook. Les services incluent Exchange et Microsoft SharePoint.

> [!NOTE]
> Pour vérifier les applications et les versions prises en charge par le service Azure Rights Management, consultez [Applications prenant en charge la protection des données Azure Rights Management](./requirements-applications.md).

Dans certains cas, le service Azure Rights Management applique automatiquement la protection, en fonction des stratégies configurées par les administrateurs. C’est le cas, par exemple, avec les bibliothèques SharePoint et les règles de transport Exchange. Dans d’autres cas, les utilisateurs finaux doivent appliquer eux-mêmes la protection à partir de leurs applications. Par exemple, les utilisateurs sélectionnent une étiquette de classification qui est configurée pour appliquer la protection, ou ils sélectionnent un modèle ou des options spécifiques. La protection appliquée par les utilisateurs est classique quand ils décident de protéger un fichier à partager, et quand ils limitent également l’accès ou l’utilisation à des utilisateurs sélectionnés ou à des utilisateurs en dehors de l’organisation.

Les modèles permettent aux utilisateurs (et administrateurs qui configurent des stratégies) d’appliquer facilement le niveau adéquat de protection et de restreindre l’accès aux personnes internes de l’organisation. Deux modèles par défaut sont livrés avec le service Azure Rights Management, mais vous voudrez probablement créer des modèles personnalisés pour réduire le temps passé par les utilisateurs et les administrateurs à spécifier des options individuelles. Pour plus d’informations sur les modèles, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).

Pour les cas où les utilisateurs doivent appliquer eux-mêmes la protection, veillez à leur fournir des instructions et des conseils sur la façon et le moment de le faire. Fournissez des instructions spécifiques pour l’application et les versions qu’ils utilisent et la façon dont ils les utilisent. Fournissez également des conseils sur le moment et la façon dont les utilisateurs doivent appliquer la protection qui convient à votre entreprise. Pour plus d’informations, consultez [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](help-users.md).

Pour plus d’informations sur la configuration de ces applications pour le service Azure Rights Management d’Azure Information Protection, consultez [Configuration d’applications pour Azure Rights Management](configure-applications.md).

Les services de recherche peuvent s’intégrer à Rights Management de différentes manières. Par exemple : 

- Exchange Online et Exchange Server utilisent l’indexation côté service pour que les e-mails protégés de l’utilisateur soient affichés automatiquement dans les résultats de la recherche. 

- SharePoint dans Microsoft 365 et SharePoint Server appliquent la protection Rights Management aux fichiers uniquement au téléchargement. Cette implémentation signifie que les résultats de l’indexation et de la recherche sur SharePoint ne sont pas affectés par cette solution de protection des documents. Cependant, si vous avez un document que vous voulez stocker dans SharePoint et que ce document ne doit pas être retourné dans les résultats de la recherche, protégez le document avant de le charger dans SharePoint.

- Windows Desktop Search utilise un index partagé entre différents utilisateurs de l’appareil. Ainsi, pour sécuriser les données dans les documents protégés, il n’indexe pas les fichiers protégés. Cela signifie que même si vos résultats de recherche n’incluent pas les fichiers que vous avez protégés, vous pouvez être sûr que vos fichiers qui contiennent des données sensibles ne sont pas affichés dans les résultats de recherche pour les autres utilisateurs qui peuvent se connecter à votre ordinateur ou se connecter à votre PC. 

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment chacun des services et applications suivants prend en charge le service Azure Rights Management :

-   [Applications et services Office](office-apps-services-support.md)

-   [Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)](file-server-support.md)

-   [Autres applications prenant en charge les API RMS](api-support.md)

