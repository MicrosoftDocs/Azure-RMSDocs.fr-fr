---
title: Configuration d’applications pour Azure Rights Management - AIP
description: Instructions pour les administrateurs relatives à la configuration d’applications et de services pour prendre en charge le service de protection Azure Rights Management d’Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1f8100e22f1608ebbd678ec5f97f77b4abd53ff0
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383650"
---
# <a name="configuring-applications-for-azure-rights-management"></a>Configuration d’applications pour Azure Rights Management

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> Ces informations sont destinées aux administrateurs informatiques et consultants qui ont déployé Azure Information Protection. Si vous recherchez des informations et une aide utilisateur sur l’utilisation des fonctionnalités de Rights Management pour une application spécifique ou sur l’ouverture d’un fichier protégé par des droits, utilisez l’aide et les conseils qui accompagnent votre application.
>
> Par exemple, pour les applications Office, cliquez sur l'icône d'aide, puis entrez les termes recherchés, comme **Rights Management** ou **IRM**. Pour le client Azure Information Protection pour Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](./rms-client/clientv2-user-guide.md).

Une fois que vous avez déployé Azure Information Protection pour votre organisation, utilisez les informations suivantes pour configurer des applications, le client Azure Information Protection et les services, tels que :

- **Applications Office**, telles que Word 2019, Word 2016 et Word 2013. 
- **Services**, tels qu’Exchange Online (règles de transport, protection contre la perte de données, ne pas transférer et chiffrement des messages) et Microsoft SharePoint (bibliothèques protégées). 

Pour des informations sur la manière dont ces applications et services prennent en charge le service de protection des données d’Azure Information Protection, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

> [!IMPORTANT]
> Pour plus d’informations sur les versions prises en charge et d’autres conditions requises, consultez [Configuration requise pour Azure information protection](requirements.md).

-   [Office 365 : configuration pour services en ligne](configure-office365.md)

    -   [Exchange Online : configuration de la gestion des droits relatifs à l’information](configure-office365.md#exchangeonline-irm-configuration)

    -   [SharePoint dans Microsoft 365 et OneDrive : configuration IRM](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)

- [Applications Office : configuration pour les clients](configure-office-apps.md)

    -   [Applications Office 365, Office 2019, Office 2016 et Office 2013](configure-office-apps.md#office365-apps-office-2019-office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office2010)

-   [Client Azure Information Protection : installation et configuration pour les clients](configure-client.md)

Pour configurer des serveurs locaux tels qu’Exchange Server et SharePoint Server, consultez [déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

Outre ces applications et services, il existe d’autres applications qui prennent en charge les API Rights Management. Cette catégorie inclut les applications métier développées en interne et les applications de fournisseurs de logiciels écrites avec le SDK Rights Management. Pour ces applications, suivez les instructions fournies avec l'application.

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez configuré vos applications pour prendre en charge le service Azure Rights Management, utilisez la feuille [de route pour le déploiement d’AIP pour la classification, l’étiquetage et la protection](deployment-roadmap-classify-label-protect.md) pour vérifier si d’autres étapes de configuration peuvent s’avérer nécessaires avant de déployer des Azure information protection pour les utilisateurs et les administrateurs. 

Dans le cas contraire, les informations opérationnelles suivantes vous seront utiles :

- [Vérification du service Azure Rights Management](verify.md)

- [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](help-users.md)

- [Journalisation et analyse du service Azure Rights Management](log-analyze-usage.md)

- [Opérations relatives à votre clé de locataire Azure Information Protection](operations-tenant-key.md)


