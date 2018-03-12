---
title: "Feuille de route pour le déploiement d’Azure Information Protection"
description: "Utilisez ces étapes pour préparer, implémenter et gérer Azure Information Protection pour votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/05/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ebfdb466be6dde9b0f1e48865c2af5d61cb038d1
ms.sourcegitcommit: dd53f3dc2ea2456ab512e3a541d251924018444e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
# <a name="azure-information-protection-deployment-roadmap"></a>Feuille de route pour le déploiement d’Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Utilisez les étapes suivantes comme des recommandations visant à faciliter la préparation, l’implémentation et la gestion d’Azure Information Protection pour votre organisation.

Toutefois, si vous souhaitez uniquement tester rapidement Azure Information Protection pour vous-même, au lieu de le déployer dans un environnement de production, consultez [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

> [!IMPORTANT]
> Avant de suivre les étapes ci-dessous, prenez le temps de consulter [Conditions requises pour Azure Information Protection](../get-started/requirements-azure-rms.md).

Choisissez la feuille de route de déploiement qui s’applique à votre organisation et qui correspond aux [fonctionnalités de l’abonnement](https://azure.microsoft.com/pricing/details/information-protection/) dont vous avez besoin :

- [Utiliser la classification, l’étiquetage et la protection](#deployment-roadmap-for-classification-labeling-and-protection)

- [Utiliser la protection des données uniquement](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>Feuille de route de déploiement pour la classification, l’étiquetage et la protection

> [!NOTE]
> Vous utilisez déjà la fonctionnalité de protection d’Azure Information Protection ? Vous pouvez ignorer la plupart de ces étapes et vous concentrer sur les étapes 3 et 5.1.

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>Étape 1 : Vérifier votre abonnement et attribuer des licences utilisateur
Examinez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) pour vérifier que votre organisation dispose d’un abonnement incluant les fonctionnalités attendues. Ensuite, attribuez une licence à partir de cet abonnement à chaque utilisateur de votre organisation susceptible de classifier, d’étiqueter et de protéger des documents et des e-mails.

Remarque : N’attribuez pas manuellement de licences utilisateur à partir de l’abonnement gratuit RMS for individuals et n’utilisez pas cette licence pour administrer le service Azure Rights Management dans votre organisation. Ces licences apparaissent sous la forme **Rights Management Adhoc** dans le centre d’administration Office 365 et **RIGHTSMANAGEMENT_ADHOC** quand vous exécutez l’applet de commande PowerShell Azure AD [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Pour plus d’informations sur la façon dont l’abonnement RMS for individuals est automatiquement accordé et attribué aux utilisateurs, consultez [RMS for individuals et Protection des informations Azure](../understand-explore/rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Étape 2 : Préparer votre locataire à l’utilisation d’Azure Information Protection
Avant de commencer à utiliser Azure Information Protection, effectuez la préparation suivante :

- Vérifiez que vous avez dans Office 365 ou Azure Active Directory des comptes et des groupes d’utilisateurs dont se servira Azure Information Protection pour authentifier et autoriser les utilisateurs de votre organisation. Si nécessaire, créez ces comptes et groupes, ou synchroniser-les à partir de votre répertoire local. Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>Étape 3 : Configurer et déployer la classification et l’étiquetage

Si vous ne disposez pas d’une stratégie de classification, passez en revue la [stratégie Azure Information Protection par défaut](../deploy-use/configure-policy-default.md) et appuyez-vous sur celle-ci pour déterminer les étiquettes de classement à attribuer à vos données d’entreprise. Vous pouvez les personnaliser en fonction des besoins de votre entreprise. 

Reconfigurez les étiquettes Azure Information Protection par défaut pour apporter toute modification nécessaire à la prise en charge de vos décisions de classification. Configurez la stratégie d’étiquetage manuel par les utilisateurs et écrivez un guide de l’utilisateur qui explique quelle étiquette appliquer et à quel moment. Si votre stratégie par défaut a été créée avec des étiquettes qui appliquent automatiquement la protection, supprimez les paramètres de protection ou désactivez l’étiquette. Pour plus d’informations sur la façon de configurer la stratégie Azure Information Protection, consultez [Configuration de la stratégie Azure Information Protection](../deploy-use/configure-policy.md).

Ensuite, déployez le client Azure Information Protection pour les utilisateurs, sans oublier de les former et de leur indiquer quand les étiquettes doivent être sélectionnées. Pour plus d’informations sur l’installation et la prise en charge du client, consultez le [Guide de l’administrateur du client Azure Information Protection](../rms-client/client-admin-guide.md).

Après un certain temps, quand les utilisateurs sont à l’aise avec l’étiquetage de leurs documents et e-mails, introduisez des configurations plus avancées. Celles-ci peuvent être les suivantes :

- Appliquer une étiquette par défaut

- Inviter les utilisateurs à fournir une justification s’ils choisissent une étiquette avec un faible niveau de classification

- Imposer que tous les documents et e-mails aient une étiquette

- Personnaliser les en-têtes, pieds de page ou filigranes

- Définir les conditions de prise en charge des recommandations et de l’étiquetage automatique

À ce stade, ne sélectionnez pas l’option qui permet de protéger les documents et les e-mails.

### <a name="step-4-prepare-for-data-protection"></a>Étape 4 : Préparer la protection des données

Quand les utilisateurs sont à l’aise avec l’étiquetage des documents et des e-mails, vous pouvez introduire la protection des données pour vos données les plus sensibles. Cette étape nécessite la préparation suivante :

1. Déterminez si vous voulez que Microsoft gère votre clé de locataire (option par défaut) ou si vous voulez la générer et la gérer vous-même (option BYOK, Bring Your Own Key). Pour plus d’informations, consultez [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Planification et implémentation de la clé de locataire Azure Information Protection).

2. Installez le module PowerShell pour AADRM sur au moins un ordinateur ayant accès à Internet. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, voir [Installation du module PowerShell AADMR](../deploy-use/install-powershell.md).

3. Si vous utilisez actuellement AD RMS : effectuez une migration pour déplacer les clés, modèles et URL dans le cloud. Pour plus d’informations, consultez [Migration d’AD RMS vers Information Protection](migrate-from-ad-rms-to-azure-rms.md).

4. Vérifiez que le service de protection est activé pour pouvoir commencer à protéger des documents et des e-mails. Si un déploiement échelonné est nécessaire, configurez les contrôles d'intégration pour restreindre l'utilisation à des utilisateurs spécifiques. Pour plus d’informations, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

Configurez éventuellement les éléments suivants :

-   Des modèles personnalisés pour des paramètres de protection si les modèles par défaut ne suffisent pas à votre organisation. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](../deploy-use/configure-policy-templates.md).

-   La journalisation de l’utilisation pour pouvoir surveiller l’usage que fait votre organisation du service de protection. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md).

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-data-protection"></a>Étape 5 : Configurer vos applications, services et stratégie Azure Information Protection pour la protection des données

1. Mettez à jour votre stratégie Azure Information Protection pour appliquer la protection des données.
    
    Modifiez votre stratégie Azure Information Protection pour qu’une ou plusieurs étiquettes appliquent la protection. Pour en savoir plus, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](../deploy-use/configure-policy-protection.md).
    
    Notez que les utilisateurs peuvent appliquer des étiquettes dans Outlook qui appliquent la protection Rights Management, même si Exchange n’est pas configuré pour la gestion des droits relatifs à l'information (IRM). Cependant, tant qu’Exchange n’est pas configuré pour IRM ou pour le [chiffrement de messages Office 365 avec de nouvelles fonctionnalités](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), votre organisation ne peut pas bénéficier des fonctionnalités complètes de la protection Azure Rights Management avec Exchange. Cette configuration supplémentaire est incluse dans la liste suivante (l’étape 2 pour Exchange Online et l’étape 5 pour Exchange sur site). 

2. Configurer des applications et des services Office
    
    Configurez des applications et services Office pour les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans SharePoint Online ou Exchange Online. Pour plus d’informations, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

3. Configurez la fonctionnalité de super utilisateur pour la récupération de données.
    
    Si vous avez des services informatiques, tels que des solutions de protection contre la perte de données (DLP), des passerelles de chiffrement de contenu (CEG) et d’autres logiciels anti-programme malveillant, qui sont chargés d’inspecter les fichiers qu’Azure Information Protection doit protéger, configurez les comptes de service en tant que super utilisateurs pour Azure Rights Management. Pour plus d’informations, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

4. Classifier et protéger les fichiers en bloc en fonction des besoins
    
    Les applets de commande PowerShell qui vous permettent de classifier et de protéger les fichiers, ainsi que d’annuler la classification et la protection, sont automatiquement installées avec le client Azure Information Protection. Pour plus d’informations, consultez [Utilisation de PowerShell avec le client Azure Information Protection](..\rms-client\client-admin-guide-powershell.md) dans le Guide de l’administrateur.

6. Déployez le connecteur pour les serveurs locaux.
    
    Si vous voulez utiliser des services locaux avec le service de protection, installez et configurez le connecteur Microsoft Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>Étape 6 : Utiliser et surveiller vos solutions de protection des données
Vous êtes maintenant prêt à protéger vos données, ainsi qu’à journaliser la manière dont votre entreprise utilise les étiquettes que vous avez configurées et la protection de données. Pour plus d’informations sur la prise en charge de cette phase de déploiement, consultez les éléments suivants :

- [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](../deploy-use/help-users.md)

-  [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md)

- [Fichiers du client et journalisation de l’utilisation](../rms-client/client-admin-guide-files-and-logging.md)

Si vous êtes intéressé par la protection automatique des fichiers à l’aide de l’infrastructure de classification des fichiers sur un serveur de fichiers Windows, consultez [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](../rms-client/configure-fci.md).

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Étape 7 : Administrer le service de protection pour votre compte de locataire selon les besoins
Quand vous commencez à utiliser le service de protection, PowerShell peut s’avérer utile pour automatiser les changements administratifs ou générer des scripts sur ces changements. Pour plus d’informations, consultez [Administration du service Azure Rights Management à l’aide de Windows PowerShell](../deploy-use/administer-powershell.md).


## <a name="deployment-roadmap-for-data-protection-only"></a>Feuille de route de déploiement pour la protection des données uniquement

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>Étape 1 : Vérifier que vous disposez d’un abonnement qui inclut le service de protection d’Azure Information Protection
Examinez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) pour vérifier que votre organisation dispose d’un abonnement incluant les fonctionnalités attendues. Ensuite, attribuez une licence à partir de cet abonnement à chaque utilisateur de votre organisation susceptible de protéger des documents et des e-mails.

Remarque : N’attribuez pas manuellement de licences utilisateur à partir de l’abonnement gratuit RMS for individuals et n’utilisez pas cette licence pour administrer le service Azure Rights Management dans votre organisation. Ces licences apparaissent sous la forme **Rights Management Adhoc** dans le centre d’administration Office 365 et **RIGHTSMANAGEMENT_ADHOC** quand vous exécutez l’applet de commande PowerShell Azure AD [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Pour plus d’informations sur la façon dont l’abonnement RMS for individuals est automatiquement accordé et attribué aux utilisateurs, consultez [RMS for individuals et Protection des informations Azure](../understand-explore/rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Étape 2 : Préparer votre locataire à l’utilisation d’Azure Information Protection
Avant de commencer à utiliser le service de protection d’Azure Information Protection, effectuez la préparation suivante :

1.  Vérifiez que votre locataire Office 365 contient les comptes et groupes d’utilisateurs qu’Azure Information Protection utilisera pour authentifier et autoriser les utilisateurs de votre organisation. Si nécessaire, créez ces comptes et groupes, ou synchroniser-les à partir de votre répertoire local. Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

2. Déterminez si vous voulez que Microsoft gère votre clé de locataire (option par défaut) ou si vous voulez la générer et la gérer vous-même (option BYOK, Bring Your Own Key). Pour plus d’informations, consultez [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Planification et implémentation de la clé de locataire Azure Information Protection).

3. Installez le module PowerShell pour AADRM sur au moins un ordinateur ayant accès à Internet. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, voir [Installation du module PowerShell AADMR](../deploy-use/install-powershell.md).

4. Si vous utilisez actuellement AD RMS : effectuez une migration pour déplacer les clés, modèles et URL dans le cloud. Pour plus d’informations, consultez [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

5. Vérifiez que le service de protection est activé pour pouvoir commencer à protéger des documents et des e-mails. Si un déploiement échelonné est nécessaire, configurez les contrôles d'intégration pour restreindre l'utilisation à des utilisateurs spécifiques. Pour plus d’informations, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

Configurez éventuellement les éléments suivants :

-   Des modèles personnalisés pour des paramètres de protection si les modèles par défaut ne suffisent pas à votre organisation. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](../deploy-use/configure-policy-templates.md).

- La journalisation de l’utilisation pour pouvoir surveiller l’usage que fait votre organisation du service de protection. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md).

### <a name="step-3-install-the-client-and-configure-applications-and-services-for-rights-management"></a>Étape 3 : Installer le client et configurer les applications et services pour Rights Management

1. Déployer le client Azure Information Protection
    
    Installez Azure Information Protection pour les utilisateurs, pour prendre en charge Office 2010, protéger les fichiers autres que les documents Office et les e-mails, et suivre des documents protégés. Formez les utilisateurs à ce client. Pour plus d’informations, consultez [Client Azure Information Protection pour Windows](../rms-client/aip-client.md).

2. Configurer des applications et des services Office
    
    Configurez des applications et services Office pour les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans SharePoint Online ou Exchange Online. Pour plus d’informations, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

3. Configurez la fonctionnalité de super utilisateur pour la récupération de données.
    
    Si vous avez des services informatiques, tels que des solutions de protection contre la perte de données (DLP), des passerelles de chiffrement de contenu (CEG) et d’autres logiciels anti-programme malveillant, qui sont chargés d’inspecter les fichiers qu’Azure Information Protection doit protéger, configurez les comptes de service en tant que super utilisateurs pour Azure Rights Management. Pour plus d’informations, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

4. Protéger les fichiers en bloc en fonction des besoins 
    
    Les applets de commande PowerShell qui vous permettent de protéger ou d’annuler la protection en bloc pour plusieurs types de fichiers sont installés automatiquement avec le client Azure Information Protection. Pour plus d’informations, consultez [Utilisation de PowerShell avec le client Azure Information Protection](..\rms-client\client-admin-guide-powershell.md) dans le Guide de l’administrateur.

5. Déployez le connecteur pour les serveurs locaux.
    
    Si vous voulez utiliser des services locaux avec le service de protection, installez et configurez le connecteur Microsoft Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).


### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Étape 4 : Utiliser et surveiller vos solutions de protection des données
Vous êtes maintenant prêt à protéger vos données, ainsi qu’à journaliser la manière dont votre entreprise utilise le service de protection. Pour plus d’informations sur la prise en charge de cette phase de déploiement, consultez [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](../deploy-use/help-users.md) et [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md).

Si vous êtes intéressé par la protection automatique des fichiers à l’aide de l’infrastructure de classification des fichiers sur un serveur de fichiers Windows, consultez [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](../rms-client/configure-fci.md).

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Étape 5 : Administrer le service de protection pour votre compte de locataire selon les besoins
Quand vous commencez à utiliser le service de protection, PowerShell peut s’avérer utile pour automatiser les changements administratifs ou générer des scripts sur ces changements. Pour plus d’informations, consultez [Administration du service Azure Rights Management à l’aide de Windows PowerShell](../deploy-use/administer-powershell.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
