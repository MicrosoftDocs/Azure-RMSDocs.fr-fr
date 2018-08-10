---
title: Désaffecter et désactiver Azure RMS
description: Informations et instructions à prendre en compte si vous décidez de ne plus utiliser ce service de protection basé sur le cloud d’Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f70186e15f38dad6ad1380997bee61991eaf4c1d
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490042"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Désaffectation et désactivation de la protection pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous pouvez toujours contrôler si votre organisation protège le contenu en utilisant le service Azure Rights Management à partir d’Azure Information Protection. Si vous décidez de ne plus utiliser ce service de protection des informations, vous aurez toujours accès au contenu précédemment protégé.

Si vous n’avez pas besoin d’un accès permanent à un contenu précédemment protégé, désactivez le service et laissez votre abonnement Azure Information Protection expirer. Cela est approprié si, par exemple, vous avez testé Azure Information Protection avant de le déployer dans un environnement de production.

Cependant, si vous avez déployé Azure Information Protection en production et que vous avez protégé des documents et des e-mails, vérifiez que vous disposez d’une copie de votre clé de locataire Azure Information Protection avant de désactiver le service Azure Rights Management. Vérifiez que vous disposez d’une copie de votre clé avant que votre abonnement expire pour pouvoir conserver l’accès au contenu protégé par Azure Rights Management après la désactivation du service. Si vous avez utilisé la solution BYOK qui vous permet de générer et gérer votre propre clé dans un module de sécurité matériel, vous avez déjà votre clé de locataire Azure Information Protection. Mais, si la gestion a été assurée par Microsoft (par défaut), consultez les instructions d’exportation de votre clé de locataire dans l’article [Opérations pour votre clé de locataire Azure Information Protection](operations-tenant-key.md).

> [!TIP]
> Même après l’expiration de votre abonnement, votre locataire Azure Information Protection reste disponible pour la consommation de contenu pendant une période prolongée. En revanche, vous ne pouvez plus exporter votre clé de locataire.

Quand vous avez votre clé de locataire Azure Information Protection, vous pouvez déployer Rights Management localement (AD RMS) et importer votre clé de locataire en tant que TPD. Ensuite, vous disposez des options suivantes pour désaffecter votre déploiement d’Azure Information Protection :

|Si vous êtes dans cette situation...|… procédez ainsi :|
|----------------------------|--------------|
|Vous souhaitez que tous les utilisateurs continuent à se servir de Rights Management, mais qu’ils recourent à une solution locale plutôt qu’à Azure Information Protection →|Utilisez l’applet de commande [Set-AadrmMigrationUrl](/powershell/module/aadrm/Set-AadrmMigrationUrl) pour diriger les utilisateurs existants vers votre déploiement local quand ils consomment du contenu protégé après cette modification. Les utilisateurs utilisent automatiquement l'installation AD RMS pour consommer le contenu protégé.<br /><br />Pour que les utilisateurs puissent consommer du contenu qui a été protégé avant cette modification, redirigez vos clients vers le déploiement local en utilisant la clé de Registre **LicensingRedirection** pour Office 2016 ou Office 2013. Pour obtenir des instructions, consultez la [section relative à la découverte du service](./rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS et la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [Paramètres de Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez cesser complètement d'utiliser les technologies Rights Management →|Attribuez des [droits de super utilisateur](configure-super-users.md) à un administrateur désigné et installez le [client Azure Information Protection](./rms-client/client-admin-guide-install.md) pour cet utilisateur.<br /><br />Cet administrateur peut ensuite utiliser le module PowerShell depuis ce client pour déchiffrer en bloc les fichiers dans les dossiers qui ont été protégés par le service Azure Rights Management. Les fichiers sont replacés dans un état non protégé et peuvent donc être lus sans une technologie Rights Management, comme Azure Information Protection ou AD RMS. Étant donné que ce module PowerShell peut être utilisé avec le service Azure Rights Management d’Azure Information Protection et avec AD RMS, vous avez le choix entre déchiffrer des fichiers avant ou après la désactivation du service Azure Rights Management, ou opter pour une combinaison.|
|Vous n’êtes pas en mesure d’identifier tous les fichiers qui ont été protégés par le service Azure Rights Management d’Azure Information Protection. Vous souhaiterez aussi peut-être que tous les utilisateurs puissent lire automatiquement les fichiers protégés qui ont été laissés de côté    →|Déployez un paramètre de Registre sur tous les ordinateurs clients à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 et Office 2013, comme décrit dans la section [Service de découverte des services](./rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS, et de la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Déployez également un autre paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez disposer d'un service de récupération manuel contrôlé pour tout fichier manqué →|Attribuez des [droits de super utilisateur](configure-super-users.md) à des utilisateurs désignés dans un groupe de récupération de données et installez le [client Azure Information Protection](./rms-client/client-admin-guide-install.md) pour que ces derniers puissent ôter la protection des fichiers quand des utilisateurs standard le leur demandent.<br /><br />Sur tous les ordinateurs, déployez le paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Pour plus d'informations sur les procédures évoquées dans ce tableau, voir les ressources suivantes :

- Pour plus d'informations sur AD RMS et des références relatives au déploiement, voir [Vue d’ensemble des services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/library/hh831364.aspx).

- Pour obtenir des instructions sur l’importation de votre clé de locataire Azure Information Protection sous la forme d’un fichier de TPD, consultez [Ajouter un domaine de publication approuvé](https://technet.microsoft.com/library/cc771460.aspx).

- Pour installer le module Windows PowerShell pour Azure Rights Management et définir l’URL de migration, consultez [Installation du module PowerShell AADRM](install-powershell.md).

- Pour utiliser PowerShell avec le client Azure Information Protection, consultez [ Utilisation de PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

Quand vous êtes prêt à désactiver le service Azure Rights Management pour votre organisation, suivez les instructions suivantes.

## <a name="deactivating-rights-management"></a>Désactivation de Rights Management
Exécutez l’une des procédures suivantes pour désactiver Azure Rights Management.

> [!TIP]
> Vous pouvez également utiliser l’applet de commande Windows PowerShell [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) pour désactiver Rights Management.

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Pour désactiver Rights Management à partir du centre d’administration Office 365

1. Accédez à la [page Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) réservée aux administrateurs Office 365.
    
    Si vous êtes invité à vous connecter, utilisez un compte qui est administrateur général pour Office 365.    

2. Sur la page **rights management** , cliquez sur **désactiver**.

3.  À l’invite **Voulez-vous désactiver Rights Management ?**, cliquez sur **Désactiver**.

Le message **Rights Management n’est pas activé** s’affiche alors, avec une option pour l’activer.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Pour désactiver Rights Management à partir du portail Azure

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection** initial, sélectionnez **Activation de la protection**. 

3.  Dans le panneau **Azure Information Protection - Activation de la protection**, sélectionnez **Désactiver**. Sélectionnez **Oui** pour confirmer votre choix.

La barre d’informations affiche **Désactivation terminée** et **Désactiver** est maintenant remplacé par **Activer**. 




