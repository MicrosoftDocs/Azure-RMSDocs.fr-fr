---
title: "Désaffecter et désactiver Azure RMS"
description: "Informations et instructions à prendre en compte si vous décidez de ne plus utiliser ce service de protection des informations d’Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f577337cf7ce904a82ff23b165fdc7befe319092
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="decommissioning-and-deactivating-azure-rights-management"></a>Désaffectation et désactivation d’Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Vous pouvez toujours contrôler si votre organisation protège le contenu à l’aide du service Azure Rights Management d’Azure Information Protection et, si vous décidez de ne plus utiliser ce service de protection des informations, vous êtes certain de toujours avoir accès au contenu précédemment protégé. Si vous n’avez pas besoin d’un accès permanent à un contenu précédemment protégé, vous pouvez simplement désactiver le service et laisser votre abonnement Azure Information Protection expirer. Cela est approprié si, par exemple, vous avez testé Azure Information Protection avant de le déployer dans un environnement de production.

Toutefois, si vous avez déployé Azure Information Protection en production et protégé des documents et e-mails, vérifiez que vous disposez d’une copie de votre clé de locataire Azure Information Protection avant de désactiver le service Azure Rights Management, et faites-le avant l’expiration de votre abonnement, car cela vous permet de conserver un accès au contenu protégé par Azure Rights Management après la désactivation du service. Si vous avez utilisé la solution BYOK qui vous permet de générer et gérer votre propre clé dans un module de sécurité matériel, vous disposez déjà de votre clé de locataire Azure Information Protection. Toutefois, si celle-ci était gérée par Microsoft (par défaut), consultez les instructions relatives à l’exportation de votre clé de locataire dans l’article [Opérations pour votre clé de client Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Même après l’expiration de votre abonnement, votre locataire Azure Information Protection reste disponible pour la consommation de contenu pendant une période prolongée. En revanche, vous ne pouvez plus exporter votre clé de locataire.

Quand vous avez votre clé de locataire Azure Information Protection, vous pouvez déployer Rights Management localement (AD RMS) et importer votre clé de locataire en tant que TPD. Ensuite, vous disposez des options suivantes pour désaffecter votre déploiement d’Azure Information Protection :

|Si vous êtes dans cette situation...|… procédez ainsi :|
|----------------------------|--------------|
|Vous souhaitez que tous les utilisateurs continuent à se servir de Rights Management, mais qu’ils recourent à une solution locale plutôt qu’à Azure Information Protection →|Utilisez l’applet de commande [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) pour diriger les utilisateurs existants vers votre déploiement local quand ils consomment du contenu protégé après cette modification. Les utilisateurs utilisent automatiquement l'installation AD RMS pour consommer le contenu protégé.<br /><br />Pour que les utilisateurs consomment du contenu protégé avant cette modification, redirigez vos clients vers le déploiement local à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 ou Office 2013, comme décrit dans la section [Service de découverte des services](../rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS, et de la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez cesser complètement d'utiliser les technologies Rights Management →|Attribuez des [droits de super utilisateur](../deploy-use/configure-super-users.md) à un administrateur désigné et fournissez-lui l’[outil de protection RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Cet administrateur peut ensuite utiliser l’outil pour déchiffrer en bloc les fichiers des dossiers qui ont été protégés par le service Azure Rights Management afin que les fichiers se retrouvent sans protection et puissent ainsi être lus sans technologie de Rights Management comme Azure Information Protection ou AD RMS. Cet outil peut être utilisé avec le service Azure Rights Management d’Azure Information Protection et AD RMS. Vous avez ainsi le choix de déchiffrer des fichiers avant ou après la désactivation du service Azure Rights Management, ou d’opter pour une combinaison.|
|Vous ne parvenez pas à identifier tous les fichiers protégés par le service Azure Rights Management d’Azure Information Protection, ou vous souhaitez que tous les utilisateurs puissent lire automatiquement tout fichier protégé manqué →|Déployez un paramètre de Registre sur tous les ordinateurs clients à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 et Office 2013, comme décrit dans la section [Service de découverte des services](../rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS, et de la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Déployez également un autre paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez disposer d'un service de récupération manuel contrôlé pour tout fichier manqué →|Attribuez des [droits de super utilisateur](../deploy-use/configure-super-users.md) à des utilisateurs désignés dans un groupe de récupération de données et fournissez-leur l’[outil de protection RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) afin qu’ils puissent ôter la protection des fichiers quand des utilisateurs standard le leur demandent.<br /><br />Sur tous les ordinateurs, déployez le paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Pour plus d'informations sur les procédures évoquées dans ce tableau, voir les ressources suivantes :

-   Pour plus d'informations sur AD RMS et des références relatives au déploiement, voir [Vue d’ensemble des services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/library/hh831364.aspx).

-   Pour obtenir des instructions sur l’importation de votre clé de locataire Azure Information Protection sous la forme d’un fichier de TPD, consultez [Ajouter un domaine de publication approuvé](https://technet.microsoft.com/library/cc771460.aspx).

-   Pour installer le module Windows PowerShell pour Azure Rights Management, pour définir l’URL de migration, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Quand vous êtes prêt à désactiver le service Azure Rights Management pour votre organisation, suivez les instructions suivantes.

## <a name="deactivating-rights-management"></a>Désactivation de Rights Management
Exécutez l’une des procédures suivantes pour désactiver [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Vous pouvez également utiliser l’applet de commande Windows PowerShell [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) pour désactiver [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Pour désactiver Rights Management à partir du centre d’administration Office 365

1. Accédez à la [page Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) réservée aux administrateurs Office 365.
    
    Si vous êtes invité à vous connecter, utilisez un compte qui est administrateur général pour Office 365.    

2. Sur la page **rights management** , cliquez sur **désactiver**.

3.  À l’invite **Voulez-vous désactiver Rights Management ?**, cliquez sur **désactiver**.

Le message **Rights Management n’est pas activé** s’affiche alors, avec une option pour l’activer.

#### <a name="to-deactivate-rights-management-from-the-azure-classic-portal"></a>Pour désactiver Rights Management à partir du portail Azure Classic

1.  Connectez-vous au [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  Dans le volet gauche, cliquez sur **Active Directory**.

3.  Dans la page **Active Directory** , cliquez sur **RIGHTS MANAGEMENT**.

4.  Assurez-vous que le nom de votre locataire est sélectionné, cliquez sur **DÉSACTIVER**, puis confirmez votre action.

Le **STATUT DE RIGHTS MANAGEMENT** apparaît alors comme **Inactif** l’option **DÉSACTIVER** est remplacée par **ACTIVER**.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


