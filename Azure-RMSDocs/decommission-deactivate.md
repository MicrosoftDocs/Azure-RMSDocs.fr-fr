---
title: Désaffecter et désactiver Azure RMS
description: Informations et instructions à prendre en compte si vous décidez de ne plus utiliser ce service de protection basé sur le cloud d’Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9add69440b76874e8d3d08125da1173d65049b54
ms.sourcegitcommit: 6ae7844205506786e09937f663457572bc8f71c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70800827"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Désaffectation et désactivation de la protection pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous pouvez toujours contrôler si votre organisation protège le contenu en utilisant le service Azure Rights Management à partir d’Azure Information Protection. Si vous décidez de ne plus utiliser ce service de protection des informations, vous aurez toujours accès au contenu précédemment protégé.

Si vous n’avez pas besoin d’un accès permanent à un contenu précédemment protégé, désactivez le service et laissez votre abonnement Azure Information Protection expirer. Cela est approprié si, par exemple, vous avez testé Azure Information Protection avant de le déployer dans un environnement de production.

Toutefois, si vous avez déployé Azure Information Protection dans des documents et des e-mails protégés, assurez-vous que vous disposez d’une copie de votre clé de locataire Azure Information Protection et d’un trusted publishing domain approprié (TPD) avant de désactiver Azure Service Rights Management. Assurez-vous de disposer d’une copie de votre clé et du TPD avant l’expiration de votre abonnement pour vous assurer que vous pouvez conserver l’accès au contenu protégé par Azure Rights Management après la désactivation du service. 

Si vous avez utilisé la solution BYOK qui vous permet de générer et gérer votre propre clé dans un module de sécurité matériel, vous avez déjà votre clé de locataire Azure Information Protection. Vous obtiendrez également un TPD approprié si vous avez suivi les instructions qui [préparent une prochaine sortie Cloud](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631). Toutefois, si votre clé de locataire a été gérée par Microsoft (valeur par défaut), consultez les instructions relatives à l’exportation de votre clé de locataire dans [opérations pour votre Azure information protection](operations-tenant-key.md) article de clé de locataire.

> [!TIP]
> Même après l’expiration de votre abonnement, votre locataire Azure Information Protection reste disponible pour la consommation de contenu pendant une période prolongée. En revanche, vous ne pouvez plus exporter votre clé de locataire.

Lorsque vous avez votre clé de locataire Azure Information Protection et TPD, vous pouvez déployer Rights Management localement (AD RMS) et importer votre clé de locataire en tant que trusted publishing domain (TPD). Ensuite, vous disposez des options suivantes pour désaffecter votre déploiement d’Azure Information Protection :

|Si vous êtes dans cette situation...|… procédez ainsi :|
|----------------------------|--------------|
|Vous voulez que tous les utilisateurs continuent à utiliser Rights Management, mais qu’ils recourent à une solution locale plutôt qu’à Azure Information Protection    →|Redirigez vos clients vers le déploiement local à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 ou Office 2013. Pour obtenir des instructions, consultez la [section détection du service](./rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS. Pour Office 2010, utilisez la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez cesser complètement d'utiliser les technologies Rights Management →|Attribuez des [droits de super utilisateur](configure-super-users.md) à un administrateur désigné et installez le [client Azure Information Protection](./rms-client/client-admin-guide-install.md) pour cet utilisateur.<br /><br />Cet administrateur peut ensuite utiliser le module PowerShell de ce client pour déchiffrer en bloc des fichiers dans des dossiers qui ont été protégés par Azure Information Protection. Les fichiers sont replacés dans un état non protégé et peuvent donc être lus sans une technologie Rights Management, comme Azure Information Protection ou AD RMS. Étant donné que ce module PowerShell peut être utilisé avec Azure Information Protection et AD RMS, vous avez la possibilité de déchiffrer des fichiers avant ou après la désactivation du service de protection à partir d’Azure Information Protection ou d’une combinaison.|
|Vous n’êtes pas en mesure d’identifier tous les fichiers qui ont été protégés par Azure Information Protection. Vous voulez que tous les utilisateurs puissent lire automatiquement les fichiers protégés qui ont été laissés de côté    →|Déployez un paramètre de Registre sur tous les ordinateurs clients à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 et Office 2013, comme décrit dans la [section Service Discovery](./rms-client/client-deployment-notes.md) des notes de déploiement du client RMS. Pour Office 2010, utilisez la clé de Registre **LicenseServerRedirection** , comme décrit dans [paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Déployez également un autre paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Vous souhaitez disposer d'un service de récupération manuel contrôlé pour tout fichier manqué →|Attribuez des [droits de super utilisateur](configure-super-users.md) à des utilisateurs désignés dans un groupe de récupération de données et installez le [client Azure Information Protection](./rms-client/client-admin-guide-install.md) pour que ces derniers puissent ôter la protection des fichiers quand des utilisateurs standard le leur demandent.<br /><br />Sur tous les ordinateurs, déployez le paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [Paramètres du Registre Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|

Pour plus d'informations sur les procédures évoquées dans ce tableau, voir les ressources suivantes :

- Pour plus d'informations sur AD RMS et des références relatives au déploiement, voir [Vue d’ensemble des services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/library/hh831364.aspx).

- Pour obtenir des instructions sur l’importation de votre clé de locataire Azure Information Protection sous la forme d’un fichier de TPD, consultez [Ajouter un domaine de publication approuvé](https://technet.microsoft.com/library/cc771460.aspx).

- Pour utiliser PowerShell avec le client Azure Information Protection, consultez [ Utilisation de PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

Lorsque vous êtes prêt à désactiver le service de protection à partir de Azure Information Protection, suivez les instructions ci-dessous.

## <a name="deactivating-rights-management"></a>Désactivation de Rights Management
Utilisez l’une des procédures suivantes pour désactiver le service de protection, Azure Rights Management.

> [!TIP]
> Vous pouvez également utiliser l’applet de commande PowerShell [Disable-AipService pour désactiver](/powershell/module/aipservice/disable-aipservice)Rights Management.

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Pour désactiver Rights Management à partir du Centre d’administration Microsoft 365

1. Accédez à la [page Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) réservée aux administrateurs Office 365.
    
    Si vous êtes invité à vous connecter, utilisez un compte qui est administrateur général pour Office 365.

2. Sur la page **rights management** , cliquez sur **désactiver**.

3.  À l’invite **Voulez-vous désactiver Rights Management ?** , cliquez sur **Désactiver**.

Le message **Rights Management n’est pas activé** s’affiche alors, avec une option pour l’activer.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Pour désactiver Rights Management à partir du portail Azure

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.

    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection** initial, sélectionnez **Activation de la protection**. 

3.  Dans le panneau **Azure Information Protection - Activation de la protection**, sélectionnez **Désactiver**. Sélectionnez **Oui** pour confirmer votre choix.

La barre d’informations affiche **Désactivation terminée** et **Désactiver** est maintenant remplacé par **Activer**. 
