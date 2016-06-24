---
# required metadata

title: Feuille de route pour le déploiement d’Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Feuille de route pour le déploiement d’Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Procédez comme suit pour préparer, implémenter et gérer Azure Rights Management (Azure RMS) pour votre organisation.

Toutefois, si vous souhaitez uniquement tester rapidement Azure RMS pour vous-même, au lieu de le déployer dans un environnement de production, consultez [Didacticiel de démarrage rapide pour Azure Rights Management](../get-started/quick-start-tutorial.md).

Pour obtenir une liste de scénarios spécifiques et les étapes de configuration et la documentation utilisateur final associés, consultez le [Guide de déploiement rapide pour Azure Rights Management](../get-started/rapid-deployment-guide.md).

> [!IMPORTANT]
> Avant de suivre les étapes ci-dessous, prenez le temps de consulter [Conditions requises pour Azure Rights Management](../get-started/requirements-azure-rms.md).

## Étape 1 : vérifier que vous disposez d'un abonnement incluant Azure Rights Management
Il existe plusieurs types d’abonnements incluant [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Consultez [Abonnements au cloud prenant en charge Azure RMS](../get-started/requirements-subscriptions.md) et vérifiez que votre abonnement inclut les fonctionnalités que vous souhaitez utiliser au sein de votre organisation en vous reportant au tableau figurant dans [Comparaison des offres de Rights Management Services (RMS)](https://technet.microsoft.com/dn858608). Vous devez attribuer une licence de cet abonnement à chaque utilisateur de votre organisation qui va protéger les fichiers et les e-mails avec Azure RMS.

## Étape 2 : préparer votre compte de locataire à l'utilisation de la Gestion des droits
Avant de commencer à utiliser [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], effectuez la préparation suivante :

1.  Assurez-vous que votre client Azure ou Office 365 contient les comptes et groupes d'utilisateurs qu'Azure RMS utilisera pour authentifier les utilisateurs de votre organisation. Si nécessaire, créez ces comptes et groupes, ou synchroniser-les à partir de votre répertoire local. Pour plus d’informations, consultez [Préparation pour Azure Rights Management](prepare.md).

2.  Déterminez si vous voulez que Microsoft gère votre clé de locataire (option par défaut) ou si vous voulez la générer et la gérer vous-même (option BYOK, Bring Your Own Key). Notez que vous ne pouvez pas actuellement utiliser l'option BYOK si vous utilisez Exchange Online. Pour plus d’informations, consultez [Planification et implémentation de la clé de locataire Azure Rights Management](plan-implement-tenant-key.md).

3.  Installez le module Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] sur au moins un ordinateur doté d’un accès à Internet. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

4.  Si vous utilisez actuellement des services Rights Management locaux : effectuez une migration pour déplacer les clés, modèles et URL dans le cloud. Pour plus d’informations, consultez [Migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).

5.  Activez la Gestion des droits pour pouvoir commencer à utiliser le service. Si un déploiement échelonné est nécessaire, configurez les contrôles d'intégration pour restreindre l'utilisation à des utilisateurs spécifiques. Pour plus d’informations, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

Configurez éventuellement les éléments suivants :

-   Des modèles personnalisés si les modèles de stratégie de droits par défaut ne suffisent pas à votre organisation. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   La journalisation de l'utilisation pour pouvoir surveiller l'usage que fait votre organisation de la Gestion des droits. Vous pouvez effectuer cette étape maintenant ou ultérieurement. Pour plus d’informations, consultez [Journalisation et analyse de l’utilisation d’Azure Rights Management](../deploy-use/log-analyze-usage.md).

## Étape 3 : configurer vos applications et services pour Rights Management
La configuration de vos applications et services peut inclure l’installation de l’application de partage Rights Management et l’activation de la prise en charge des fonctionnalités de Gestion des droits relatifs à l’information (IRM) dans SharePoint Online ou Exchange Online. Pour plus d’informations, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

Si vous avez des services informatiques, tels que des solutions de protection contre la perte de données (DLP), des passerelles de chiffrement de contenu (CEG) et d’autres logiciels anti-programme malveillant, qui sont chargés d’inspecter les fichiers qu’Azure RMS doit protéger, configurez les comptes de service en tant que super utilisateurs pour Azure RMS. Pour plus d’informations, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

Pour pouvoir protéger ou ôter la protection en bloc de tous les types de fichiers, installez l’outil de protection RMS, qui utilise le module PowerShell de protection RMS. Pour plus d’informations, consultez [Applets de commande de Protection RMS](https://msdn.microsoft.com/library/mt433195.aspx).

Si vous voulez utiliser des services locaux avec Azure Rights Management, installez et configurez le connecteur Microsoft Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Étape 4 : Publier et utiliser du contenu protégé par des droits
Vous êtes maintenant prêt à publier et à consommer du contenu protégé, ainsi qu'à journaliser la manière dont votre entreprise utilise Rights Management. Pour plus d’informations, consultez [Aider les utilisateurs à protéger des fichiers en utilisant Azure Rights Management](../deploy-use/help-users.md) et [Journalisation et analyse de l’utilisation d’Azure Rights Management](../deploy-use/log-analyze-usage.md).

Si vous êtes intéressé par la protection automatique des fichiers à l’aide de l’infrastructure de classification des fichiers sur un serveur de fichiers Windows, consultez [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](../rms-client/configure-fci.md).

## Étape 5 : administrer la Gestion des droits pour votre compte de locataire selon les besoins
Quand vous commencez à utiliser [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], le module [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour Windows PowerShell peut s’avérer utile pour automatiser les changements administratifs ou générer des scripts sur ces changements. Pour plus d’informations, consultez [Administration d’Azure Rights Management à l’aide de Windows PowerShell](../deploy-use/administer-powershell.md).




<!--HONumber=May16_HO2-->


