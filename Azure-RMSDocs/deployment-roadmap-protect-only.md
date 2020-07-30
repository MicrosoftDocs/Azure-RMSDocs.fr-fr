---
title: Feuille de route pour le déploiement de l’Azure Information Protection (AIP) pour la protection uniquement
description: Procédez comme suit pour préparer, implémenter et gérer Azure Information Protection (AIP) pour votre organisation, lorsque vous souhaitez implémenter la protection uniquement.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ecf9257a69a5046592cb52f810e171859df238a4
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298396"
---
# <a name="azure-information-protection-deployment-roadmap-for-protection-only"></a>Plan de déploiement Azure Information Protection pour la protection uniquement

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

> [!TIP]
> Vous pouvez également Rechercher l’un des articles suivants :
> - [Plan de déploiement AIP pour la classification, l’étiquetage et la protection](deployment-roadmap-classify-label-protect.md)
> - [Guides de procédures pour les scénarios courants utilisant Azure Information Protection](how-to-guides.md)
>- [Feuille de route Azure Information Protection Release](information-support.md#information-about-new-releases-and-updates)

Suivez les étapes ci-dessous comme recommandations pour vous aider à préparer, implémenter et gérer des Azure Information Protection pour votre organisation, lorsque vous souhaitez implémenter la protection des données uniquement.

Cette feuille de route est recommandée pour les clients disposant d’un abonnement qui ne prend pas en charge la classification et les étiquettes, mais prend en charge la protection sans étiquette. Le client standard AIP doit être installé. 

## <a name="deployment-process"></a>Processus de déploiement

Effectuez les étapes suivantes :

1. [Vérifiez que vous disposez d’un abonnement qui comprend le service de protection AIP](#confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service) [
1. [Préparer votre locataire à l’utilisation d’Azure Information Protection](#prepare-your-tenant-to-use-azure-information-protection)
1. [Installer le Azure Information Protection Classic et le client configurer des applications et des services pour Rights Management](#install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management)
1. [Utiliser et superviser vos solutions de protection des données](#use-and-monitor-your-data-protection-solutions)
1. [Administrer le service de protection pour votre compte de locataire selon les besoins](#administer-the-protection-service-for-your-tenant-account-as-needed)

## <a name="confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service"></a>Confirmer que vous disposez d’un abonnement qui comprend le service de protection AIP

Vérifiez que votre organisation dispose d’un abonnement qui inclut les fonctionnalités que vous attendez. Vous pouvez utiliser les informations d’abonnement et la liste des fonctionnalités de la page de [tarification de Azure information protection](https://azure.microsoft.com/pricing/details/information-protection) .

Attribuez une licence de cet abonnement à chaque utilisateur de votre organisation qui protégera les documents et les e-mails.

> [!IMPORTANT]
> N’attribuez pas manuellement des licences utilisateur à partir de l’abonnement gratuit RMS for individuals et n’utilisez pas cette licence pour administrer le service Azure Rights Management dans votre organisation. 
>
> Ces licences apparaissent sous la forme **Rights Management Adhoc** dans le Centre d’administration Microsoft 365 et **RIGHTSMANAGEMENT_ADHOC** quand vous exécutez l’applet de commande PowerShell Azure AD [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). 
>
> Pour plus d’informations sur la façon dont l’abonnement RMS for individuals est automatiquement accordé et attribué aux utilisateurs, consultez [RMS for individuals et Protection des informations Azure](./rms-for-individuals.md).

## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>Préparer votre locataire à l’utilisation d’Azure Information Protection

Avant de commencer à utiliser le service de protection d’Azure Information Protection, effectuez la préparation suivante :

1. **Configurez vos comptes et groupes d’utilisateurs pour AIP.**

    Vérifiez que votre locataire Office 365 contient les comptes et groupes d’utilisateurs qu’Azure Information Protection utilisera pour authentifier et autoriser les utilisateurs de votre organisation. Si nécessaire, créez ces comptes et groupes, ou synchronisez-les à partir de votre annuaire local. 

    Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

1. **Décidez comment vous souhaitez gérer votre clé de locataire.**

    Déterminez si vous voulez que Microsoft gère votre clé de locataire (option par défaut) ou si vous voulez la générer et la gérer vous-même (option BYOK, Bring Your Own Key). Pour renforcer la sécurité, implémentez la protection « conserver votre propre clé » (HYOK). 

    Pour plus d’informations, consultez [Planification et implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

1. **Installez PowerShell pour AIP**.

    Installez le module PowerShell pour AIPService sur au moins un ordinateur qui a accès à Internet. Vous pouvez effectuer cette étape maintenant ou ultérieurement. 

    Pour plus d’informations, consultez [installation du module PowerShell AIPService](./install-powershell.md).

1. **AD RMS uniquement : migrez vos données vers le Cloud**.

    Si vous utilisez actuellement AD RMS : effectuez une migration pour déplacer les clés, modèles et URL dans le cloud. 

    Pour plus d’informations, consultez [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

1. **Activez la protection**.

    Vérifiez que le service de protection est activé pour pouvoir commencer à protéger des documents et des e-mails. Si vous effectuez un déploiement en plusieurs phases, configurez des contrôles d’intégration d’utilisateur pour limiter la capacité des utilisateurs à appliquer la protection. 

    Pour plus d’informations, consultez [Activation du service de protection à partir d’Azure Information Protection](./activate-service.md).

1. **Configurer des fonctionnalités facultatives si nécessaire**.

    Envisagez de configurer l’une ou l’autre des fonctionnalités suivantes, à l’heure actuelle ou une version ultérieure.
    
    |Caractéristique  |Description  |
    |---------|---------|
    |**Modèles personnalisés pour les paramètres de protection**     |  Si les modèles par défaut ne sont pas suffisants pour votre organisation, configurez des modèles personnalisés. </br>Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](./configure-policy-templates.md).       |
    |**Journalisation de l’utilisation**     | Configurez la journalisation de l’utilisation pour surveiller la manière dont votre organisation utilise le service de protection. </br>Pour plus d’informations, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](./log-analyze-usage.md).        |
    | | |

## <a name="install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management"></a>Installer le Azure Information Protection Classic et le client configurer des applications et des services pour Rights Management

Effectuez les étapes suivantes :

1. **Déployer le client Azure Information Protection Classic**
    
    Installez le client Classic pour que les utilisateurs prennent en charge Office 2010, afin de protéger les fichiers autres que les documents Office et les e-mails, ainsi que de suivre les documents protégés et de fournir une formation utilisateur pour ce client. 

    Pour plus d’informations, consultez [Client Azure Information Protection pour Windows](./rms-client/aip-client.md).

2. **Configurer des applications et des services Office**
    
    Configurez les applications et services Office pour les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans SharePoint ou Exchange Online. 

    Pour plus d’informations, consultez [configuration d’applications pour Azure Rights Management](./configure-applications.md).

3. **Configurez la fonctionnalité de super utilisateur pour la récupération de données.**
    
    Si vous avez des services informatiques, tels que des solutions de protection contre la perte de données (DLP), des passerelles de chiffrement de contenu (CEG) et d’autres logiciels anti-programme malveillant, qui sont chargés d’inspecter les fichiers qu’Azure Information Protection doit protéger, configurez les comptes de service en tant que super utilisateurs pour Azure Rights Management. 

    Pour plus d’informations, consultez [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](./configure-super-users.md).

4. **Protéger les fichiers existants en bloc** 
    
    Vous pouvez utiliser les applets de commande PowerShell pour protéger en bloc plusieurs types de fichiers ou annuler cette protection en bloc. 

    Pour plus d’informations, consultez [utilisation de PowerShell avec le client Azure information protection](./rms-client/client-admin-guide-powershell.md) du Guide de l’administrateur.
    
    Pour les fichiers sur les serveurs de fichiers Windows, vous pouvez utiliser ces applets de commande avec un script et l’infrastructure de classification des fichiers de Windows Server. Pour plus d’informations, consultez [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](./rms-client/configure-fci.md).

5. **Déployez le connecteur pour les serveurs locaux.**
    
    Si vous voulez utiliser des services locaux avec le service de protection, installez et configurez le connecteur Microsoft Rights Management. 

    Pour plus d’informations, consultez [déploiement du connecteur Azure Rights Management](./deploy-rms-connector.md).

## <a name="use-and-monitor-your-data-protection-solutions"></a>Utiliser et superviser vos solutions de protection des données

Vous êtes maintenant prêt à protéger vos données et à consigner la manière dont votre entreprise utilise le service de protection. 

Pour plus d’informations, consultez :

- [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](./help-users.md)
- [Journalisation et analyse de l’utilisation de la protection à partir de Azure Information Protection](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>Administrer le service de protection pour votre compte de locataire selon les besoins

Quand vous commencez à utiliser le service de protection, PowerShell peut s’avérer utile pour automatiser les changements administratifs ou générer des scripts sur ces changements. PowerShell peut également être nécessaire pour certaines configurations avancées. 

Pour plus d’informations, consultez [administration de la protection à partir de Azure information protection à l’aide de PowerShell](./administer-powershell.md).

## <a name="next-steps"></a>Étapes suivantes

Lorsque vous déployez Azure Information Protection, il peut s’avérer utile de consulter les [questions fréquemment posées](faqs.md), ainsi que la page [informations et support](information-support.md) pour obtenir des ressources supplémentaires.