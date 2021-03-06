---
title: Désaffecter et désactiver Azure RMS
description: Informations et instructions à prendre en compte si vous décidez de ne plus utiliser ce service de protection basé sur le cloud d’Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 058e814ba2759cf70ca1cc36875992ea1ab69ab7
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809630"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Désaffectation et désactivation de la protection pour Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Vous pouvez toujours contrôler si votre organisation protège le contenu en utilisant le service Azure Rights Management à partir d’Azure Information Protection. Si vous décidez de ne plus utiliser ce service de protection des informations, vous aurez toujours accès au contenu précédemment protégé.

Si vous n’avez pas besoin d’un accès permanent à un contenu précédemment protégé, désactivez le service et laissez votre abonnement Azure Information Protection expirer. Cela est approprié si, par exemple, vous avez testé Azure Information Protection avant de le déployer dans un environnement de production.

Toutefois, si vous avez déployé Azure Information Protection dans des documents et des e-mails protégés, assurez-vous que vous disposez d’une copie de votre clé de locataire Azure Information Protection et d’un trusted publishing domain approprié (TPD) avant de désactiver le service Azure Rights Management. Assurez-vous de disposer d’une copie de votre clé et du TPD avant l’expiration de votre abonnement pour vous assurer que vous pouvez conserver l’accès au contenu protégé par Azure Rights Management après la désactivation du service. 

Si vous avez utilisé la solution BYOK qui vous permet de générer et gérer votre propre clé dans un module de sécurité matériel, vous avez déjà votre clé de locataire Azure Information Protection. Vous obtiendrez également un TPD approprié si vous avez suivi les instructions qui [préparent une prochaine sortie Cloud](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631). Toutefois, si votre clé de locataire a été gérée par Microsoft (valeur par défaut), consultez les instructions relatives à l’exportation de votre clé de locataire dans [opérations pour votre Azure information protection](operations-tenant-key.md) article de clé de locataire.

> [!TIP]
> Même après l’expiration de votre abonnement, votre locataire Azure Information Protection reste disponible pour la consommation de contenu pendant une période prolongée. En revanche, vous ne pouvez plus exporter votre clé de locataire.

Lorsque vous avez votre clé de locataire Azure Information Protection et TPD, vous pouvez déployer Rights Management localement (AD RMS) et importer votre clé de locataire en tant que trusted publishing domain (TPD). Ensuite, vous disposez des options suivantes pour désaffecter votre déploiement d’Azure Information Protection :

|Si vous êtes dans cette situation...|… procédez ainsi :|
|----------------------------|--------------|
|Vous souhaitez que tous les utilisateurs continuent à se servir de Rights Management, mais qu’ils recourent à une solution locale plutôt qu’à Azure Information Protection →|Redirigez vos clients vers le déploiement local à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 ou Office 2013. Pour obtenir des instructions, consultez la [section détection du service](./rms-client/client-deployment-notes.md) dans les notes de déploiement du client RMS. <br><br>Pour Office 2010, utilisez la clé de Registre **LicenseServerRedirection** pour Office 2010, comme décrit dans [paramètres du Registre Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)). <br><br>**Important**: la prise en charge étendue d’Office 2010 a pris fin le 13 octobre 2020. Pour plus d’informations, consultez [AIP et versions héritées de Windows et d’Office](known-issues.md#aip-and-legacy-windows-and-office-versions).|
|Vous souhaitez cesser complètement d'utiliser les technologies Rights Management →|Attribuez des [droits de super utilisateur](configure-super-users.md) à un administrateur désigné et installez le [client Azure Information Protection](./rms-client/client-admin-guide-install.md) pour cet utilisateur.<br /><br />Cet administrateur peut ensuite utiliser le module PowerShell de ce client pour déchiffrer en bloc des fichiers dans des dossiers qui ont été protégés par Azure Information Protection. Les fichiers sont replacés dans un état non protégé et peuvent donc être lus sans une technologie Rights Management, comme Azure Information Protection ou AD RMS. Étant donné que ce module PowerShell peut être utilisé avec Azure Information Protection et AD RMS, vous avez la possibilité de déchiffrer des fichiers avant ou après la désactivation du service de protection à partir d’Azure Information Protection ou d’une combinaison.|
|Vous n’êtes pas en mesure d’identifier tous les fichiers qui ont été protégés par Azure Information Protection. Vous souhaiterez aussi peut-être que tous les utilisateurs puissent lire automatiquement les fichiers protégés qui ont été laissés de côté    →|Déployez un paramètre de Registre sur tous les ordinateurs clients à l’aide de la clé de Registre **LicensingRedirection** pour Office 2016 et Office 2013, comme décrit dans la [section Service Discovery](./rms-client/client-deployment-notes.md) des notes de déploiement du client RMS. <br><br>**Pour Office 2010**: <br>-Utilisez la clé de Registre **LicenseServerRedirection** , comme décrit dans [paramètres du Registre Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)). <br>-Déployez un autre paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [paramètres du Registre Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)). <br><br>**Important**: la prise en charge étendue d’Office 2010 a pris fin le 13 octobre 2020. Pour plus d’informations, consultez [AIP et versions héritées de Windows et d’Office](known-issues.md#aip-and-legacy-windows-and-office-versions).|
|Vous souhaitez disposer d'un service de récupération manuel contrôlé pour tout fichier manqué →|Attribuez des [droits de super utilisateur](configure-super-users.md) à des utilisateurs désignés dans un groupe de récupération de données et installez le [client Azure Information Protection](./rms-client/client-admin-guide-install.md) pour que ces derniers puissent ôter la protection des fichiers quand des utilisateurs standard le leur demandent.<br /><br />Sur tous les ordinateurs, déployez le paramètre de Registre pour empêcher les utilisateurs de protéger de nouveaux fichiers en définissant **DisableCreation** sur **1**, comme décrit dans [paramètres du Registre Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)).|
| | |

Pour plus d'informations sur les procédures évoquées dans ce tableau, voir les ressources suivantes :

- Pour plus d’informations sur les AD RMS et les références de déploiement, consultez [services AD RMS (Active Directory Rights Management Services) vue d’ensemble](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831364(v=ws.11)).

- Pour obtenir des instructions sur l’importation de votre clé de locataire Azure Information Protection sous la forme d’un fichier de TPD, consultez [Ajouter un domaine de publication approuvé](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771460(v=ws.11)).

- Pour utiliser PowerShell avec le client Azure Information Protection, consultez [ Utilisation de PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

Lorsque vous êtes prêt à désactiver le service de protection à partir de Azure Information Protection, suivez les instructions ci-dessous.

## <a name="deactivating-rights-management"></a>Désactivation de Rights Management
Utilisez l’une des procédures suivantes pour désactiver le service de protection, Azure Rights Management.

> [!TIP]
> Vous pouvez également utiliser l’applet de commande PowerShell [Disable-AipService pour désactiver](/powershell/module/aipservice/disable-aipservice)Rights Management.

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Pour désactiver Rights Management à partir du Centre d’administration Microsoft 365

1. Accédez à la [page Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) pour Microsoft 365 les administrateurs.
    
    Si vous êtes invité à vous connecter, utilisez un compte d’administrateur général pour Microsoft 365.

2. Dans la page **Gestion des droits**, cliquez sur **Désactiver**.

3.  Quand vous y êtes invité, voulez **-vous désactiver les Rights Management ?** cliquez sur **Désactiver**.

Le message **Rights Management n’est pas activé** s’affiche alors, avec une option pour l’activer.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Pour désactiver Rights Management à partir du portail Azure

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**.

    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. Dans le volet **Azure information protection** initial, sélectionnez **activation** de la protection. 

3.  Dans le volet **Azure information protection d’activation** de la protection, sélectionnez **Désactiver**. Sélectionnez **Oui** pour confirmer votre choix.

La barre d’informations affiche **Désactivation terminée** et **Désactiver** est maintenant remplacé par **Activer**.