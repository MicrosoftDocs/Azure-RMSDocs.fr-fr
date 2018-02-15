---
title: Configurer des super utilisateurs pour Azure Rights Management - AIP
description: "Vous devez comprendre et implémenter la fonctionnalité de super utilisateur du service Azure Rights Management d’Azure Information Protection afin que les personnes et services autorisés puissent toujours lire et inspecter les données qu’Azure Rights Management protège pour votre organisation. Cette capacité, parfois appelée « reasoning over data », est un élément déterminant pour conserver le contrôle des données de votre entreprise."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a134d6619f67bfc3d26cb1726fe07e8ffca403cd
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données

>*S’applique à : Azure Information Protection, Office 365*

Grâce à la fonctionnalité de super utilisateur du service Azure Rights Management d’Azure Information Protection, les personnes et services autorisés peuvent toujours lire et inspecter les données qu’Azure Rights Management protège pour votre organisation. Si nécessaire, supprimez la protection ou modifiez la protection appliquée précédemment. 

Un super utilisateur a toujours le [droit d’utilisation](configure-usage-rights.md) Contrôle total Rights Management pour les documents et e-mails qui ont été protégés par le locataire Azure Information Protection de votre organisation. Cette capacité, parfois appelée « reasoning over data », est un élément déterminant pour conserver le contrôle des données de votre entreprise. Par exemple, vous pouvez utiliser cette fonctionnalité pour les scénarios suivants :

- Un employé quitte l’organisation et vous devez lire les fichiers qu’il a protégés.

- Un administrateur doit supprimer la stratégie de protection actuellement configurée pour les fichiers et appliquer une nouvelle stratégie de protection.

- Exchange Server doit indexer les boîtes aux lettres pour des opérations de recherche.

- Vous avez des services informatiques existants pour les solutions de prévention contre la perte de données (DLP), les passerelles de chiffrement de contenu (CEG) et les produits anti-programme malveillant qui doivent inspecter des fichiers déjà protégés.

- Vous devez déchiffrer des fichiers en bloc à des fins d’audit, juridiques ou de conformité.

Par défaut, la fonctionnalité de super utilisateur n’est pas activée et ce rôle n’est attribué à aucun utilisateur. Il est automatiquement activée si vous configurez le connecteur Rights Management pour Exchange, et il n’est pas requis pour les services standard qui exécutent Exchange Online, SharePoint Online ou SharePoint Server.

Si vous devez activer manuellement la fonctionnalité de super utilisateur : utilisez l’applet de commande Windows PowerShell [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature), désignez des utilisateurs (ou des comptes de service) en fonction des besoins à l’aide de l’applet de commande [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) ou [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup), puis ajoutez des utilisateurs (ou d’autres groupes) en fonction des besoins de ce groupe. 

Bien que l’utilisation d’un groupe de super utilisateurs soit plus facile à gérer, n’oubliez pas que pour des raisons de performances, Azure Rights Management [met en cache l’appartenance au groupe](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). Par conséquent, si vous devez affecter un nouvel utilisateur en tant que super utilisateur afin de déchiffrer le contenu immédiatement, ajoutez-le à l’aide de l’applet de commande Add-AadrmSuperUser, plutôt que de l’ajouter à un groupe existant configuré à l’aide de l’applet de commande Set-AadrmSuperUserGroup.

> [!NOTE]
> Si vous n’avez pas encore installé le module Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Recommandations de sécurité pour la fonctionnalité de super utilisateur :

- Limitez et surveillez les administrateurs désignés comme administrateurs généraux pour votre locataire Office 365 ou Azure Information Protection ou qui se voient attribuer le rôle de GlobalAdministrator par le biais de l’applet de commande [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator). Ces utilisateurs peuvent activer la fonctionnalité de super utilisateur, ainsi que désigner des utilisateurs (et eux-mêmes) comme super utilisateurs, et potentiellement déchiffrer tous les fichiers que votre organisation protège.

- Pour voir quels utilisateurs et comptes de service sont désignés comme super utilisateurs, utilisez l’applet de commande [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser). Pour savoir si un groupe de super utilisateurs est configuré, utilisez l’applet de commande [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperusergroup) et vos outils de gestion d’utilisateur standard pour vérifier les utilisateurs qui sont membres de ce groupe. Comme toutes les actions d’administration, les opérations d’activation ou de désactivation de la fonctionnalité de super utilisateur, ainsi que d’ajout ou de suppression de super utilisateurs sont enregistrées et peuvent être auditées à l’aide de la commande [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog). Quand les super utilisateurs déchiffrent des fichiers, l’action est enregistrée et peut être auditée à l’aide de la [journalisation de l’utilisation](log-analyze-usage.md).

- Si vous n’avez pas besoin de la fonctionnalité de super utilisateur pour les services quotidiens, activez-la uniquement lorsque nécessaire, puis désactivez-la à l’aide de l’applet de commande [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature).

L’extrait de journal suivant montre des exemples d’entrées lors de l’utilisation de l’applet de commande Get-AadrmAdminLog. Dans cet exemple, l’administrateur de la société Contoso Ltd confirme que la fonctionnalité de super utilisateur est désactivée, ajoute Richard Simone comme super utilisateur, vérifie que celui-ci est bien le seul super utilisateur configuré pour le service Azure Rights Management, puis active la fonctionnalité de super utilisateur pour permettre à Richard de déchiffrer des fichiers protégés par un employé qui a quitté la société.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>Options de script pour les super utilisateurs
Une personne désignée comme super utilisateur pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] devra souvent supprimer la protection de plusieurs fichiers, dans plusieurs emplacements. Bien qu’il soit possible de le faire manuellement, il est plus efficace (et souvent plus fiable) de le faire à l’aide d’un script. Pour ce faire, vous pouvez utiliser les applets de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) et [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) en fonction des besoins. 

Si vous utilisez la classification et la protection, vous pouvez également utiliser [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) pour appliquer une nouvelle étiquette n’appliquant pas la protection, ou supprimer l’étiquette qui a appliqué la protection. 

Pour plus d’informations sur ces applets de commande, consultez [Utilisation de PowerShell avec le client Azure Information Protection](../rms-client/client-admin-guide-powershell.md) dans le guide de l’administrateur du client Azure Information Protection.

> [!NOTE]
> Le module AzureInformationProtection remplace le module PowerShell de protection RMS installé avec l’outil de protection RMS. Ces deux modules diffèrent de et complètent le [module Windows PowerShell pour Azure Rights Management](administer-powershell.md) principal. Le module AzureInformationProtection prend en charge Azure Information Protection, le service Azure Rights Management (Azure RMS) d’Azure Information Protection et les services Active Directory Rights Management Services (AD RMS).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

