---
title: Configuration d’applications pour Azure Rights Management - AIP
description: Instructions pour les administrateurs relatives à la configuration d’applications et de services pour prendre en charge le service de protection Azure Rights Management d’Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 753ef710b4a4058e9792203e549b27cae83f8a12
ms.sourcegitcommit: 2af2297319265c1f91aa76eb227c6f4d316df42a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348797"
---
# <a name="configuring-applications-for-azure-rights-management"></a>Configuration d’applications pour Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> Ces informations sont destinées aux administrateurs informatiques et consultants qui ont déployé Azure Information Protection. Si vous recherchez des informations et une aide utilisateur sur l’utilisation des fonctionnalités de Rights Management pour une application spécifique ou sur l’ouverture d’un fichier protégé par des droits, utilisez l’aide et les conseils qui accompagnent votre application.
>
> Par exemple, pour les applications Office, cliquez sur l'icône d'aide, puis entrez les termes recherchés, comme **Rights Management** ou **IRM**. Pour le client Azure Information Protection pour Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](./rms-client/client-user-guide.md).

Après avoir déployé Azure Information Protection pour votre organisation, utilisez les informations suivantes pour configurer des applications, le client Azure Information Protection et des services. Par exemple, les applications de Office comme Word 2019, Word 2016 et Word 2013. Des services tels qu’Exchange Online (règles de transport, protection contre la perte de données, Ne pas transférer et chiffrement des messages) et SharePoint Online (bibliothèques protégées) également. Pour des informations sur la manière dont ces applications et services prennent en charge le service de protection des données d’Azure Information Protection, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

> [!IMPORTANT]
> Pour plus d’informations sur les versions prises en charge et les autres exigences, consultez [Configuration requise pour Azure Rights Management](requirements.md).

-   [Office 365 : Configuration des services en ligne](configure-office365.md)

    -   [Exchange Online : Configuration de la Gestion des droits relatifs à l’information](configure-office365.md#exchangeonline-irm-configuration)

    -   [SharePoint Online et OneDrive Entreprise : Configuration de la Gestion des droits relatifs à l’information](configure-office365.md#sharepointonline-and-onedrive-for-business-irm-configuration)

- [Applications Office : Configuration pour les clients](configure-office-apps.md)

    -   [Applications Office 365, Office 2019, Office 2016 et Office 2013](configure-office-apps.md#office365-apps-office-2019-office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office2010)

-   [Client Azure Information Protection : Installation et configuration pour les clients](configure-client.md)

Pour configurer des serveurs locaux tels que SharePoint Server et Exchange Server, consultez [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

Outre ces applications et services, il existe d’autres applications qui prennent en charge les API Rights Management. Cette catégorie inclut les applications métier développées en interne et les applications de fournisseurs de logiciels écrites avec le SDK Rights Management. Pour ces applications, suivez les instructions fournies avec l'application.

## <a name="next-steps"></a>Étapes suivantes
Une fois vos applications configurées pour prendre en charge le service Azure Rights Management, utilisez la [Feuille de route pour le déploiement d’Azure Information Protection](deployment-roadmap.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre Azure Information Protection à la disposition des utilisateurs et des administrateurs. Dans le cas contraire, les informations opérationnelles suivantes vous seront utiles :

- [Vérification du service Azure Rights Management](verify.md)

- [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](help-users.md)

- [Journalisation et analyse du service Azure Rights Management](log-analyze-usage.md)

- [Opérations pour votre clé de locataire Azure Information Protection](operations-tenant-key.md)


