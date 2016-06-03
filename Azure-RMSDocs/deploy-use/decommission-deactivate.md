---
# required metadata

title: Désaffectation et désactivation d’Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Désaffectation et désactivation d’Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Vous pouvez toujours contrôler si votre organisation protège le contenu à l’aide d’[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) et, si vous décidez de ne plus utiliser cette solution de protection des informations, vous êtes certain de toujours avoir accès au contenu précédemment protégé. Si vous n'avez pas besoin d'un accès permanent à un contenu précédemment protégé, vous pouvez simplement désactiver le service et laisser votre abonnement Azure Rights Management expirer. Cela est approprié si, par exemple, vous avez testé [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] avant de le déployer dans un environnement de production.

Toutefois, si vous avez déployé [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] en production, vérifiez que vous disposez d’une copie de votre clé de locataire Azure Rights Management avant de désactiver le service, et faites-le avant l’expiration de votre abonnement, car cela vous permet de conserver un accès au contenu protégé par Azure Rights Management après la désactivation du service. Si vous avez utilisé la solution BYOK qui vous permet de générer et gérer votre propre clé dans un module de sécurité matériel, vous disposez déjà de votre clé de locataire Azure Rights Management. Toutefois, si celle-ci était gérée par Microsoft (par défaut), consultez les instructions relatives à l’exportation de votre clé de locataire dans l’article [Opérations pour votre clé de client Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Même après l'expiration de votre abonnement, votre locataire Azure Rights Management reste disponible pour la consommation de contenu pendant une période prolongée. En revanche, vous ne pouvez plus exporter votre clé de locataire.

Lorsque vous avez votre clé de locataire Azure Rights Management, vous pouvez déployer Rights Management (AD RMS) et importer votre clé de locataire en tant que TPD. Ensuite, vous disposez des options suivantes pour désaffecter votre déploiement d’Azure Rights Management :

|Si vous êtes dans cette situation...|… procédez ainsi :|
|----------------------------|--------------|
|Vous souhaitez que tous les utilisateurs continuent à se servir de Rights Management, mais qu’ils recourent à une solution locale plutôt qu’à Azure RMS →|Utilisez l’applet de commande [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) pour diriger les utilisateurs existants vers votre déploiement local quand ils consomment du contenu protégé après cette modification. Les utilisateurs utilisent automatiquement l'installation AD RMS pour consommer le contenu protégé.<br /><br />Pour que les utilisateurs consomment du contenu protégé avant cette modification, redirigez vos clients vers le déploiement local à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 ou Office 2013, comme décrit dans la section [Service de découverte des services](../rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS, et de la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez cesser complètement d'utiliser les technologies Rights Management →|Attribuez des [droits de super utilisateur](../deploy-use/configure-super-users.md) à un administrateur désigné et fournissez-lui l’[outil de protection RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Cet administrateur peut ensuite utiliser l’outil pour déchiffrer en bloc les fichiers des dossiers qui ont été protégés par Azure Rights Management afin que les fichiers se retrouvent sans protection et puissent ainsi être lus sans technologie de Rights Management comme Azure RMS ou AD RMS. Cet outil peut être utilisé avec Azure RMS et AD RMS. Vous avez ainsi le choix de déchiffrer des fichiers avant ou après la désactivation d'Azure RMS, ou d'opter pour une combinaison.|
|Vous ne parvenez pas à identifier tous les fichiers protégés par Azure RMS, ou vous souhaitez que tous les utilisateurs puissent lire automatiquement tout fichier protégé manqué →|Déployez un paramètre de Registre sur tous les ordinateurs clients à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 et Office 2013, comme décrit dans la section [Service de découverte des services](../rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS, et de la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Déployez également un autre paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en affectant la valeur **1** à **DisableCreation**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez disposer d'un service de récupération manuel contrôlé pour tout fichier manqué →|Attribuez des [droits de super utilisateur](../deploy-use/configure-super-users.md) à des utilisateurs désignés dans un groupe de récupération de données et fournissez-leur l’[outil de protection RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) afin qu’ils puissent ôter la protection des fichiers quand des utilisateurs standard le leur demandent.<br /><br />Sur tous les ordinateurs, déployez le paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en affectant la valeur **1** à **DisableCreation**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Pour plus d'informations sur les procédures évoquées dans ce tableau, voir les ressources suivantes :

-   Pour plus d’informations sur AD RMS et pour obtenir des références relatives au déploiement, consultez [Vue d’ensemble des services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/library/hh831364.aspx).

-   Pour obtenir des instructions sur l’importation de votre clé de locataire Azure RMS sous la forme d’un fichier de TPD, consultez [Ajouter un domaine de publication approuvé](https://technet.microsoft.com/library/cc771460.aspx).

-   Pour installer le module Windows PowerShell pour Azure RMS, pour définir l’URL de migration, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Lorsque vous êtes prêt à désactiver le service Azure RMS pour votre organisation, suivez les instructions suivantes.

## Désactivation de Rights Management
Exécutez l’une des procédures suivantes pour désactiver [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Vous pouvez également utiliser l’applet de commande Windows PowerShell [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) pour désactiver [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### Pour désactiver Rights Management à partir du centre d’administration Office 365

1.  [Connectez-vous à Office 365 avec le compte de votre établissement scolaire ou de votre entreprise](https://portal.office.com/) qui sert d’administrateur pour votre déploiement d’Office 365.

2.  Si le Centre d’administration Office 365 ne s’affiche pas automatiquement, sélectionnez l’icône du lanceur d’applications en haut à gauche, puis choisissez **Admin**. La vignette **Admin** s'affiche uniquement pour les administrateurs Office 365.

    > [!TIP]
    > Pour obtenir l’aide du centre d’administration, consultez [À propos du Centre d’administration Office 365 - Aide de l’administrateur](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  Dans le volet gauche, développez **PARAMÈTRES DE SERVICE**.

4.  Cliquez sur **Rights Management**.

5.  Dans la page **RIGHTS MANAGEMENT**, cliquez sur **Gérer**.

6.  Dans la page **rights management**, cliquez sur **désactiver**.

7.  À l’invite **Voulez-vous désactiver Rights Management ?**, cliquez sur **désactiver**.

Le message **Rights Management n’est pas activé** s’affiche alors, avec une option pour l’activer.

#### Pour désactiver Rights Management à partir du portail Azure Classic

1.  Connectez-vous au [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  Dans le volet gauche, cliquez sur **ACTIVE DIRECTORY**.

3.  Dans la page **active directory**, cliquez sur **RIGHTS MANAGEMENT**.

4.  Sélectionnez le répertoire à gérer pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], cliquez sur **DÉSACTIVER**, puis confirmez votre action.

Le **STATUT DE RIGHTS MANAGEMENT** apparaît alors comme **Inactif** et l’option **DÉSACTIVER** est remplacée par **ACTIVER**.





<!--HONumber=Apr16_HO4-->


