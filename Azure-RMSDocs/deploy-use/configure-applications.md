---
title: "Configuration d’applications pour Azure Rights Management - AIP"
description: "Instructions pour les administrateurs relatives à la configuration d’applications et de services pour prendre en charge le service de protection Azure Rights Management d’Azure Information Protection. par exemple des applications Office telles que Word 2013 et Word 2010, et des services tels qu’Exchange Online (règles de transport, protection contre la perte de données, Ne pas transférer et chiffrement des messages) et SharePoint Online (bibliothèques protégées)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 8161315fcb3c3beb40b5273db799a5a3f37e4a7e
ms.lasthandoff: 02/24/2017


---

# <a name="configuring-applications-for-azure-rights-management"></a>Configuration d’applications pour Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

> [!NOTE]
> Ces informations sont destinées aux administrateurs informatiques et consultants qui ont déployé Azure Information Protection. Si vous recherchez des informations et une aide utilisateur sur l’utilisation des fonctionnalités de Rights Management pour une application spécifique ou sur l’ouverture d’un fichier protégé par des droits, utilisez l’aide et les conseils qui accompagnent votre application.
>
> Par exemple, pour les applications Office, cliquez sur l'icône d'aide, puis entrez les termes recherchés, comme **Rights Management** ou **IRM**. Pour le client Azure Information Protection pour Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](../rms-client/client-user-guide.md).

Après avoir déployé Azure Information Protection pour votre organisation, utilisez les informations suivantes pour configurer des applications, le client Azure Information Protection et des services. Par exemple, des applications Office telles que Word 2016, Word 2013 et Word 2010. Des services tels qu’Exchange Online (règles de transport, protection contre la perte de données, Ne pas transférer et chiffrement des messages) et SharePoint Online (bibliothèques protégées) également. Pour des informations sur la manière dont ces applications et services prennent en charge le service de protection des données d’Azure Information Protection, consultez [Comment les applications prennent en charge le service Azure Rights Management](../understand-explore/applications-support.md).

> [!IMPORTANT]
> Pour plus d’informations sur les versions prises en charge et les autres exigences, consultez [Configuration requise pour Azure Rights Management](../get-started/requirements-azure-rms.md).

-   [Office 365 : configuration pour les clients et services en ligne](configure-office365.md)

    -   [Exchange Online : configuration de la gestion des droits relatifs à l'information](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online et OneDrive Entreprise : configuration de la gestion des droits relatifs à l'information](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Applications Office : configuration pour les clients](configure-office-apps.md)

    -   [Office 2016 et Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Client Azure Information Protection : installation et configuration pour les clients](configure-sharing-app.md)

-   [Application de partage Rights Management : installation et configuration pour les clients](configure-sharing-app.md)


Pour configurer des serveurs locaux tels que SharePoint Server et Exchange Server, consultez [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

> [!TIP]
> Pour obtenir des exemples généraux et des captures d’écran d’applications configurées de manière à utiliser le service Azure Rights Management, consultez [Azure RMS en action : ce que voient les administrateurs et les utilisateurs](../understand-explore/what-admins-users-see.md).


Outre ces applications et services, il existe d’autres applications qui prennent en charge les API Rights Management. Cette catégorie inclut les applications métier développées en interne et les applications de fournisseurs de logiciels écrites avec le SDK Rights Management. Pour ces applications, suivez les instructions fournies avec l'application.

## <a name="next-steps"></a>Étapes suivantes
Une fois vos applications configurées pour prendre en charge le service Azure Rights Management, utilisez la [Feuille de route pour le déploiement d’Azure Information Protection](../plan-design/deployment-roadmap.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre Azure Information Protection à la disposition des utilisateurs et des administrateurs. Dans le cas contraire, les informations opérationnelles suivantes vous seront utiles :

- [Vérification du service Azure Rights Management](verify.md)

- [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](help-users.md)

- [Journalisation et analyse du service Azure Rights Management](log-analyze-usage.md)

- [Opérations pour votre clé de locataire Azure Information Protection](operations-tenant-key.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


