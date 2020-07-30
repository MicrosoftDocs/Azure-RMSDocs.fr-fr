---
title: Déployer Azure Information Protection (AIP) pour la classification, l’étiquetage et la protection
description: Procédez comme suit pour préparer, implémenter et gérer Azure Information Protection (AIP) pour votre organisation, lorsque vous souhaitez classifier, étiqueter et protéger vos données.
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
ms.openlocfilehash: f4039b1c74ae8b341c5afb13a02a743267f00930
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298401"
---
# <a name="aip-deployment-roadmap-for-classification-labeling-and-protection"></a>Plan de déploiement AIP pour la classification, l’étiquetage et la protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Suivez les étapes ci-dessous comme recommandations pour vous aider à préparer, implémenter et gérer des Azure Information Protection pour votre organisation, lorsque vous souhaitez classifier, étiqueter et protéger vos données.

Cette feuille de route est recommandée pour tous les clients disposant d’un abonnement. Les fonctionnalités supplémentaires incluent la découverte des informations sensibles et l’étiquetage des documents et des e-mails pour la classification. 

Les étiquettes peuvent également appliquer une protection, ce qui simplifie cette étape pour vos utilisateurs. 

Cette feuille de route est prise en charge pour les étiquettes AIP créées avec le client classique et les étiquettes de sensibilité qui utilisent la [plateforme d’étiquetage unifiée](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

> [!TIP]
> Vous pouvez également Rechercher l’un des articles suivants :
> - [Feuille de route AIP pour la protection des données uniquement](deployment-roadmap-protect-only.md)
> - [Guides de procédures pour les scénarios courants utilisant Azure Information Protection](how-to-guides.md)
>- [Feuille de route Azure Information Protection Release](information-support.md#information-about-new-releases-and-updates)

## <a name="deployment-process"></a>Processus de déploiement

Effectuez les étapes suivantes :

1. [Vérifier votre abonnement et attribuer des licences utilisateur](#confirm-your-subscription-and-assign-user-licenses)
1. [Préparer votre locataire à l’utilisation d’Azure Information Protection](#prepare-your-tenant-to-use-azure-information-protection)
1. [Configurer et déployer la classification et l’étiquetage](#configure-and-deploy-classification-and-labeling)
1. [Préparer la protection des données](#prepare-for-data-protection)
1. [Configurer des étiquettes et des paramètres, des applications et des services pour la protection des données](#configure-labels-and-settings-applications-and-services-for-data-protection)
1. [Utiliser et superviser vos solutions de protection des données](#use-and-monitor-your-data-protection-solutions)
1. [Administrer le service de protection pour votre compte de locataire selon les besoins](#administer-the-protection-service-for-your-tenant-account-as-needed)

> [!TIP]
> Vous utilisez déjà la fonctionnalité de protection d’Azure Information Protection ? Vous pouvez ignorer la plupart de ces étapes et vous concentrer sur les étapes [3](#configure-and-deploy-classification-and-labeling) et [5,1](#configure-labels-and-settings-applications-and-services-for-data-protection).

## <a name="confirm-your-subscription-and-assign-user-licenses"></a>Vérifier votre abonnement et attribuer des licences utilisateur

Vérifiez que votre organisation dispose d’un abonnement qui inclut les fonctionnalités que vous attendez. Vous trouverez ces détails sur la page de [tarification Azure information protection](https://azure.microsoft.com/pricing/details/information-protection) .

Ensuite, attribuez des licences à partir de cet abonnement à chaque utilisateur de votre organisation susceptible de classifier, d’étiqueter et de protéger des documents et des e-mails.

> [!IMPORTANT]
> N’attribuez pas manuellement des licences utilisateur de l’abonnement RMS for Individuals gratuit et n’utilisez pas cette licence pour administrer le service Azure Rights Management pour votre organisation. 
>
> Ces licences apparaissent sous la forme **Rights Management Adhoc** dans le Centre d’administration Microsoft 365 et **RIGHTSMANAGEMENT_ADHOC** quand vous exécutez l’applet de commande PowerShell Azure AD [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). 
>
> Pour plus d’informations, consultez [RMS for Individuals et Azure information protection](./rms-for-individuals.md).
> 
## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>Préparer votre locataire à l’utilisation d’Azure Information Protection

Avant de commencer à utiliser Azure Information Protection, assurez-vous que vous disposez de comptes d’utilisateur et de groupes dans Office 365 ou Azure Active Directory que AIP peut utiliser pour authentifier et autoriser vos utilisateurs.

Si nécessaire, créez ces comptes et groupes, ou synchronisez-les à partir de votre annuaire local. 

Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

## <a name="configure-and-deploy-classification-and-labeling"></a>Configurer et déployer la classification et l’étiquetage

Déterminez si vous allez utiliser le client d’étiquetage standard AIP ou AIP ou si vous avez besoin de ces deux clients.

1. **Déterminez le client que vous souhaitez utiliser.**

    Déterminez le client dont vous aurez besoin à ce stade pour connaître le portail de gestion à utiliser lors de la configuration des étiquettes et des paramètres de stratégie.

    Pour plus d’informations, consultez [choisir le client Azure information protection à utiliser](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

1. **Analyser vos fichiers (facultatif mais recommandé).**

    [Déployez et exécutez le scanneur AIP](deploy-aip-scanner.md) pour découvrir les informations sensibles dont vous disposez dans vos magasins de données locaux. Les informations trouvées par le scanneur peuvent vous aider dans votre taxonomie de classification ainsi que fournir de précieuses informations sur les étiquettes dont vous avez besoin et les fichiers à protéger.

    Le mode de détection de l’analyseur ne nécessite aucune configuration d’étiquette ni taxonomie, et est donc adapté à cette phase préliminaire de votre déploiement. Vous pouvez également utiliser cette configuration d’analyseur en parallèle avec les étapes de déploiement suivantes, jusqu’à ce que vous configuriez l’étiquetage automatique ou recommandé.

1. **Personnaliser la stratégie AIP par défaut**.

    Si vous n’avez pas encore de stratégie de classification, utilisez la [stratégie de Azure information protection par défaut](./configure-policy-default.md) comme base pour déterminer les étiquettes dont vous aurez besoin pour vos données. Personnalisez ces étiquettes si nécessaire pour répondre à vos besoins.

    Par exemple, vous souhaiterez peut-être reconfigurer vos étiquettes avec les informations suivantes :

    - Assurez-vous que vos étiquettes prennent en charge vos décisions de classification.
    - Configurer des stratégies pour l’étiquetage manuel par les utilisateurs
    - Écrivez un guide de l’utilisateur pour expliquer quelle étiquette doit être appliquée dans chaque scénario.
    - Si votre stratégie par défaut a été créée avec des étiquettes qui appliquent automatiquement la protection, vous souhaiterez peut-être supprimer temporairement les paramètres de protection ou désactiver l’étiquette pendant que vous testez vos paramètres. 

    Pour plus d’informations sur la configuration des étiquettes et des paramètres de stratégie, consultez :

    - **Client classique :** [configuration](./configure-policy.md) de la stratégie de Azure information protection
    - **Client d’étiquetage unifié :** [en savoir plus sur les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)
    
1. **Déployer votre client**

    Une fois que vous avez configuré une stratégie, déployez le Azure Information Protection client d’étiquetage classique et/ou unifié pour vos utilisateurs. Fournissez une formation utilisateur et des instructions spécifiques pour sélectionner les étiquettes. 

    Pour plus d'informations, consultez les pages suivantes :

    - **Client classique**: [Guide](./rms-client/client-admin-guide.md) de l’administrateur
    - **Client d’étiquetage unifié**: [Guide](./rms-client/clientv2-admin-guide.md) de l’administrateur

1. **Introduire des configurations plus avancées**

    Attendez que vos utilisateurs soient plus à l’aise avec les étiquettes de leurs documents et e-mails. Lorsque vous êtes prêt, introduisez des configurations avancées, telles que :

    - Application d’étiquettes par défaut
    - Demander à l’utilisateur la justification s’il choisit une étiquette avec un niveau de classification inférieur ou supprimer une étiquette
    - Obligation de faire en sorte que tous les documents et e-mails aient une étiquette
    - Personnalisation des en-têtes, des pieds de page ou des filigranes
    - Étiquetage automatique et recommandé

    Pour plus d'informations, consultez les pages suivantes :

    - **Client classique**: [Guide de l’administrateur : configurations personnalisées](rms-client/client-admin-guide-customizations.md)
    - **Client d’étiquetage unifié**: [Guide d’administration : configurations personnalisées](rms-client/clientv2-admin-guide-customizations.md)
     
    > [!TIP]
    > Si vous avez configuré des étiquettes pour l’étiquetage automatique, exécutez à nouveau le [moteur de Azure information protection](deploy-aip-scanner-manage.md) sur vos banques de données locales en mode détection et en fonction de votre stratégie. 
    > 
    > L’exécution du scanneur en mode détection vous indique les étiquettes qui seront appliquées aux fichiers, ce qui vous permet d’affiner la configuration de votre étiquette et de vous préparer à la classification et à la protection des fichiers en bloc. 
    > 

## <a name="prepare-for-data-protection"></a>Préparer la protection des données

Introduisez la protection des données pour vos données les plus sensibles une fois que les utilisateurs sont habitués à étiqueter les documents et les e-mails.

Pour préparer la protection des données, procédez comme suit :

1. **Déterminez comment vous souhaitez gérer votre clé de locataire**.

    Déterminez si vous voulez que Microsoft gère votre clé de locataire (option par défaut) ou si vous voulez la générer et la gérer vous-même (option BYOK, Bring Your Own Key). 

    > [!NOTE]
    > En fonction de votre client, des options supplémentaires pour la « conservation de votre propre clé (HYOK) » ou le chiffrement à clé double sont disponibles pour renforcer la sécurité. .
    >
 
    Pour plus d’informations, consultez [planification et implémentation de votre clé de locataire Azure information protection](plan-implement-tenant-key.md)

1. **Installez PowerShell pour AIP**.

    Installez le module PowerShell pour AIPService sur au moins un ordinateur qui a accès à Internet. Vous pouvez effectuer cette étape maintenant ou ultérieurement. 

    Pour plus d’informations, consultez [installation du module PowerShell AIPService](./install-powershell.md).

1. **AD RMS uniquement**: migrez vos clés, vos modèles et vos URL vers le Cloud.

    Si vous utilisez actuellement AD RMS, effectuez une migration pour déplacer les clés, les modèles et les URL vers le Cloud. 
    
    Pour plus d’informations, consultez [Migration d’AD RMS vers Information Protection](migrate-from-ad-rms-to-azure-rms.md).

1. **Activez la protection**.

    Vérifiez que le service de protection est activé pour pouvoir commencer à protéger des documents et des e-mails. Si vous effectuez un déploiement en plusieurs phases, configurez des contrôles d’intégration d’utilisateur pour limiter la capacité des utilisateurs à appliquer la protection. 

    Pour plus d’informations, consultez [Activation du service de protection à partir d’Azure Information Protection](./activate-service.md).

1. **Envisagez la journalisation de l’utilisation (facultatif)**.

    Envisagez l’utilisation de la journalisation pour surveiller la manière dont votre organisation utilise le service de protection. Vous pouvez effectuer cette étape maintenant ou ultérieurement. 

    Pour plus d’informations, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](./log-analyze-usage.md).

## <a name="configure-labels-and-settings-applications-and-services-for-data-protection"></a>Configurer des étiquettes et des paramètres, des applications et des services pour la protection des données

Effectuez les étapes suivantes :

1. **Mettre à jour vos étiquettes pour appliquer la protection**
    
    Utilisez l’un des guides suivants, en fonction de votre client :

    - Classique : [Comment configurer une étiquette pour la protection de Rights Management](./configure-policy-protection.md)
    - Étiquetage unifié : [restreindre l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)
    
    > [!IMPORTANT]
    > Les utilisateurs peuvent appliquer des étiquettes dans Outlook qui appliquent Rights Management protection même si Exchange n’est pas configuré pour la gestion des droits relatifs à l’information (IRM). 
    > 
    > Cependant, tant qu’Exchange n’est pas configuré pour IRM ou pour le [chiffrement de messages Office 365 avec de nouvelles fonctionnalités](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), votre organisation ne peut pas bénéficier des fonctionnalités complètes de la protection Azure Rights Management avec Exchange. Cette configuration supplémentaire est incluse dans la liste suivante (l’étape 2 pour Exchange Online et l’étape 5 pour Exchange sur site). 
    > 

1. **Configurer des applications et des services Office**
    
    Configurez les applications et services Office pour les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans Microsoft SharePoint ou Exchange Online. 

    Pour plus d’informations, consultez [configuration d’applications pour Azure Rights Management](configure-applications.md).

1. **Configurez la fonctionnalité de super utilisateur pour la récupération de données.**
    
    Si vous avez des services informatiques, tels que des solutions de protection contre la perte de données (DLP), des passerelles de chiffrement de contenu (CEG) et d’autres logiciels anti-programme malveillant, qui sont chargés d’inspecter les fichiers qu’Azure Information Protection doit protéger, configurez les comptes de service en tant que super utilisateurs pour Azure Rights Management. 

    Pour plus d’informations, consultez [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](./configure-super-users.md).

1. **Classifier et protéger les fichiers existants en bloc**
    
    Pour vos banques de données locales, exécutez maintenant le [scanneur Azure Information Protection](deploy-aip-scanner.md) en mode de mise en conformité afin que les fichiers soient automatiquement étiquetés.
    
    Pour les fichiers sur PC, utilisez les applets de commande PowerShell pour classifier et protéger des fichiers. Pour plus d’informations, consultez les guides suivants, en fonction de votre client :
    
    - **Client classique :** [utilisation de PowerShell avec le client Azure information protection](./rms-client/client-admin-guide-powershell.md)
    - **Client d’étiquetage unifié :** [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md)

    Pour les banques de données basées sur le cloud, utilisez [Azure Cloud App Security](https://docs.microsoft.com/cloud-app-security). 

    > [!TIP]
    > La classification et la protection des fichiers existants en bloc ne sont pas l’un des principaux cas d’utilisation de Cloud App Security. les [solutions de contournement documentées](https://docs.microsoft.com/cloud-app-security/azip-integration#enable-azure-information-protection) peuvent vous aider à obtenir la classification et la protection de vos fichiers.

6. **Déployez le connecteur pour les bibliothèques protégées par IRM sur SharePoint Server et les e-mails protégés par IRM pour Exchange sur site**
    
    Si vous avez SharePoint et Exchange sur site, et souhaitez utiliser leurs fonctionnalités de gestion des droits relatifs à l’information (IRM), installez et configurez le connecteur Rights Management. 

    Pour plus d’informations, consultez [déploiement du connecteur Azure Rights Management](./deploy-rms-connector.md).

## <a name="use-and-monitor-your-data-protection-solutions"></a>Utiliser et superviser vos solutions de protection des données

Vous êtes maintenant prêt à surveiller la manière dont votre organisation utilise les étiquettes que vous avez configurées et à confirmer que vous protégez les informations sensibles. 

Pour plus d'informations, consultez les pages suivantes :

- [Rapports centraux pour Azure information protection](reports-aip.md) actuellement en version préliminaire
- [Journalisation de l’utilisation locale avec l’analyseur d’événements Windows](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client) pour le client Azure information protection Classic
- [Journalisation et analyse de l’utilisation de la protection à partir de Azure Information Protection](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>Administrer le service de protection pour votre compte de locataire selon les besoins

Quand vous commencez à utiliser le service de protection, PowerShell peut s’avérer utile pour automatiser les changements administratifs ou générer des scripts sur ces changements. PowerShell peut également être nécessaire pour certaines configurations avancées. 

Pour plus d’informations, consultez [administration de la protection à partir de Azure information protection à l’aide de PowerShell](./administer-powershell.md).

## <a name="next-steps"></a>Étapes suivantes

Lorsque vous déployez Azure Information Protection, il peut s’avérer utile de consulter les [questions fréquemment posées](faqs.md), ainsi que la page [informations et support](information-support.md) pour obtenir des ressources supplémentaires.