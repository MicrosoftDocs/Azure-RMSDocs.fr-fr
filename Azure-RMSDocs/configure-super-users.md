---
title: Configurer des super utilisateurs pour Azure Rights Management - AIP
description: Découvrez et implémentez la fonctionnalité de super utilisateur du service Azure Rights Management d’Azure Information Protection. Grâce à celle-ci, les personnes et services autorisés peuvent toujours lire et inspecter les données qu’Azure Rights Management protège pour votre organisation. Cette capacité, parfois appelée « reasoning over data », est un élément déterminant pour conserver le contrôle des données de votre entreprise.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3a4cf3eaaf177a9424a438d0cdbee54b6a0a252e
ms.sourcegitcommit: 5b4eb0e17fb831d338d8c25844e9e6f4ca72246d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53173823"
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Grâce à la fonctionnalité de super utilisateur du service Azure Rights Management d’Azure Information Protection, les personnes et services autorisés peuvent toujours lire et inspecter les données qu’Azure Rights Management protège pour votre organisation. Si nécessaire, la protection peut ensuite être supprimée ou modifiée.

Un super utilisateur a toujours le [droit d’utilisation](configure-usage-rights.md) Contrôle total Rights Management pour les documents et e-mails qui ont été protégés par le locataire Azure Information Protection de votre organisation. Cette fonctionnalité, parfois appelée « reasoning over data », est un élément déterminant pour conserver le contrôle des données de votre entreprise. Par exemple, vous pouvez utiliser cette fonctionnalité pour les scénarios suivants :

- Un employé quitte l’organisation et vous devez lire les fichiers qu’il a protégés.

- Un administrateur doit supprimer la stratégie de protection actuellement configurée pour les fichiers et appliquer une nouvelle stratégie de protection.

- Exchange Server doit indexer les boîtes aux lettres pour des opérations de recherche.

- Vous avez des services informatiques existants pour les solutions de prévention contre la perte de données (DLP), les passerelles de chiffrement de contenu (CEG) et les produits anti-programme malveillant qui doivent inspecter des fichiers déjà protégés.

- Vous devez déchiffrer des fichiers en bloc à des fins d’audit, juridiques ou de conformité.

## <a name="configuration-for-the-super-user-feature"></a>Configuration de la fonctionnalité de super utilisateur

Par défaut, la fonctionnalité de super utilisateur n’est pas activée et ce rôle n’est attribué à aucun utilisateur. Elle est automatiquement activée si vous configurez le connecteur Rights Management pour Exchange. Elle n’est pas requise pour les services standard qui exécutent Exchange Online, SharePoint Online ou SharePoint Server.

Si vous devez activer manuellement la fonctionnalité de super utilisateur : utilisez l’applet de commande Windows PowerShell [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature), désignez des utilisateurs (ou des comptes de service) en fonction des besoins à l’aide de l’applet de commande [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) ou [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup), puis ajoutez des utilisateurs (ou d’autres groupes) en fonction des besoins de ce groupe. 

Bien que l’utilisation d’un groupe de super utilisateurs soit plus facile à gérer, n’oubliez pas que pour des raisons de performances, Azure Rights Management [met en cache l’appartenance au groupe](prepare.md#group-membership-caching-by-azure-information-protection). Par conséquent, si vous devez affecter un nouvel utilisateur en tant que super utilisateur afin de déchiffrer le contenu immédiatement, ajoutez-le à l’aide de l’applet de commande Add-AadrmSuperUser, plutôt que de l’ajouter à un groupe existant configuré à l’aide de l’applet de commande Set-AadrmSuperUserGroup.

> [!NOTE]
> Si vous n’avez pas encore installé le module Windows PowerShell pour Azure Rights Management, consultez [Installation du module PowerShell AADRM](install-powershell.md).

Peu importe le moment où vous activez la fonctionnalité de super utilisateur ou ajoutez des utilisateurs en tant que super utilisateurs. Par exemple, si vous activez la fonctionnalité jeudi et que vous ajoutez un utilisateur vendredi, cet utilisateur peut immédiatement ouvrir le contenu qui a été protégé au début de la semaine.

## <a name="security-best-practices-for-the-super-user-feature"></a>Bonnes pratiques de sécurité pour la fonctionnalité de super utilisateur

- Limitez et surveillez les administrateurs désignés comme administrateurs généraux pour votre locataire Office 365 ou Azure Information Protection ou qui se voient attribuer le rôle de GlobalAdministrator par le biais de l’applet de commande [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator). Ces utilisateurs peuvent activer la fonctionnalité de super utilisateur, ainsi que désigner des utilisateurs (et eux-mêmes) comme super utilisateurs, et potentiellement déchiffrer tous les fichiers que votre organisation protège.

- Pour voir quels utilisateurs et comptes de service sont désignés comme super utilisateurs, utilisez l’applet de commande [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser). Pour savoir si un groupe de super utilisateurs est configuré, utilisez l’applet de commande [Get-AadrmSuperUserGroup](/powershell/module/aadrm/get-aadrmsuperusergroup) et vos outils de gestion d’utilisateur standard pour vérifier quels utilisateurs sont membres de ce groupe. Comme toutes les actions d’administration, les opérations d’activation ou de désactivation de la fonctionnalité de super utilisateur, ainsi que d’ajout ou de suppression de super utilisateurs sont enregistrées et peuvent être auditées à l’aide de la commande [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) . Consultez la section suivante pour un exemple. Quand les super utilisateurs déchiffrent des fichiers, l’action est enregistrée et peut être auditée à l’aide de la [ journalisation de l’utilisation](log-analyze-usage.md).

- Si vous n’avez pas besoin de la fonctionnalité de super utilisateur pour les services quotidiens, activez-la uniquement lorsque nécessaire, puis désactivez-la à l’aide de l’applet de commande [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) .

### <a name="example-auditing-for-the-super-user-feature"></a>Exemple d’audit de la fonctionnalité de super utilisateur

L’extrait de journal suivant montre des exemples d’entrées lors de l’utilisation de l’applet de commande [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog). 

Dans cet exemple, l’administrateur pour la société Contoso Ltd confirme que la fonctionnalité de super utilisateur est désactivée, ajoute Richard Simone comme super utilisateur, vérifie que celui-ci est bien le seul super utilisateur configuré pour le service Azure Rights Management, puis active la fonctionnalité de super utilisateur pour permettre à Richard de déchiffrer des fichiers protégés par un employé qui a quitté la société.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>Options de script pour les super utilisateurs
Une personne désignée comme super utilisateur pour Azure Rights Management devra souvent supprimer la protection de plusieurs fichiers de plusieurs emplacements. Bien qu’il soit possible de le faire manuellement, il est plus efficace (et souvent plus fiable) de le faire à l’aide d’un script. Pour ce faire, vous pouvez utiliser les applets de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) et [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) en fonction des besoins. 

Si vous utilisez la classification et la protection, vous pouvez également utiliser [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) pour appliquer une nouvelle étiquette n’appliquant pas la protection, ou supprimer l’étiquette qui a appliqué la protection. 

Pour plus d’informations sur ces applets de commande, consultez [Utilisation de PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) dans le guide de l’administrateur du client Azure Information Protection.

> [!NOTE]
> Le module AzureInformationProtection est différent et vient en complément du [module PowerShell AADRM](administer-powershell.md) qui gère le service Azure Rights Management pour Azure Information Protection.

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>Conseils d’utilisation d’Unprotect-RMSFile pour eDiscovery

Même si vous pouvez utiliser l’applet de commande Unprotect-RMSFile pour déchiffrer le contenu protégé dans des fichiers PST, utilisez cette applet de commande stratégiquement dans le cadre de votre processus eDiscovery. L’exécution d’Unprotect-RMSFile sur des fichiers volumineux d’un ordinateur nécessite de nombreuses ressources (mémoire et espace disque) et la taille de fichier maximale prise en charge pour cette applet de commande est de 5 Go.

Dans l’idéal, utilisez [Office 365 eDiscovery](/office365/securitycompliance/ediscovery) pour rechercher dans les e-mails protégés et extraire une pièce jointe protégée dans les e-mails. La capacité de super utilisateur est automatiquement intégrée à Exchange Online afin qu’eDiscovery dans le Centre de sécurité et conformité Office 365 puisse rechercher des éléments chiffrés avant l’exportation, ou déchiffrer un e-mail chiffré lors de l’exportation.

Si vous ne pouvez pas utiliser Office 365 eDiscovery, vous pouvez recourir à une autre solution eDiscovery qui s’intègre au service Azure Rights Management pour exploiter les données de la même façon. Par ailleurs, si votre solution e-Discovery ne peut pas lire et déchiffrer automatiquement le contenu protégé, vous pouvez toujours utiliser cette solution dans un processus à plusieurs étapes qui vous permet d’exécuter Unprotect-RMSFile plus efficacement :

1. Exportez l’e-mail en question dans un fichier PST depuis Exchange Online ou Exchange Server, ou à partir de la station de travail où l’utilisateur a stocké son e-mail.

2. Importez le fichier PST dans votre outil eDiscovery. Étant donné que l’outil ne peut pas lire le contenu protégé, il est probable que ces éléments vont générer des erreurs.

3. À partir de tous les éléments que l’outil n’a pas pu ouvrir, générez un fichier PST qui, cette fois, contient uniquement des éléments protégés. Ce second fichier PST sera probablement beaucoup plus petit que le fichier PST d’origine.

4. Exécutez Unprotect-RMSFile sur ce second fichier PST pour déchiffrer le contenu de ce fichier beaucoup plus petit. À partir de la sortie, importez le fichier PST maintenant déchiffré dans votre outil de découverte.

Pour obtenir plus d’informations et de conseils sur l’exécution d’eDiscovery sur les boîtes aux lettres et les fichiers PST, consultez le billet de blog suivant : [Azure Information Protection and eDiscovery Processes](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216).

