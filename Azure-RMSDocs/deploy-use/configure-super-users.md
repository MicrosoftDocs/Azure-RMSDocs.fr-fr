---
# required metadata

title: Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données

*S’applique à : Azure Rights Management, Office 365*

La fonctionnalité de super utilisateur de Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) garantit que les personnes et services autorisés peuvent toujours lire et inspecter les données qu’Azure RMS protège pour votre organisation. Si nécessaire, supprimez la protection ou modifiez la protection appliquée précédemment. Un super utilisateur possède toujours des droits de propriétaire complets pour toutes les licences d’utilisation octroyées par le client RMS de l’organisation. Cette capacité, parfois appelée « reasoning over data », est un élément déterminant pour conserver le contrôle des données de votre entreprise. Par exemple, vous pouvez utiliser cette fonctionnalité pour les scénarios suivants :

-   Un employé quitte l’organisation et vous devez lire les fichiers qu’il a protégés.

-   Un administrateur doit supprimer la stratégie de protection actuellement configurée pour les fichiers et appliquer une nouvelle stratégie de protection.

-   Exchange Server doit indexer les boîtes aux lettres pour des opérations de recherche.

-   Vous avez des services informatiques existants pour les solutions de prévention contre la perte de données (DLP), les passerelles de chiffrement de contenu (CEG) et les produits anti-programme malveillant qui doivent inspecter des fichiers déjà protégés.

-   Vous devez déchiffrer des fichiers en bloc à des fins d’audit, juridiques ou de conformité.

Par défaut, la fonctionnalité de super utilisateur n’est pas activée et ce rôle n’est attribué à aucun utilisateur. Elle est automatiquement activée si vous configurez le connecteur Rights Management pour Exchange. Elle n’est pas requise pour les services standard qui exécutent Exchange Online, SharePoint Online ou SharePoint Server.

Si vous devez activer manuellement la fonctionnalité de super utilisateur, utilisez l’applet de commande Windows PowerShell [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx), puis désignez des utilisateurs (ou des comptes de service) en fonction des besoins à l’aide de l’applet de commande [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) ou [Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx), puis ajoutez des utilisateurs (ou d’autres groupes) en fonction des besoins pour ce groupe. 

> [!NOTE]
> Si vous n’avez pas encore installé le module Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Recommandations de sécurité pour la fonctionnalité de super utilisateur :

-   Limitez et surveillez les administrateurs désignés comme administrateurs généraux pour votre client Office 365 ou Azure RMS ou qui se voient attribuer le rôle de GlobalAdministrator via l’applet de commande [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) . Ces utilisateurs peuvent activer la fonctionnalité de super utilisateur, ainsi que désigner des utilisateurs (et eux-mêmes) comme super utilisateurs, et potentiellement déchiffrer tous les fichiers que votre organisation protège.

-   Pour voir quels utilisateurs et comptes de service sont désignés comme super utilisateurs, utilisez l’applet de commande [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx). Pour savoir si un groupe de super utilisateurs est configuré, utilisez l’applet de commande [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) et vos outils de gestion d’utilisateur standard pour vérifier les utilisateurs qui sont membres de ce groupe. Comme toutes les actions d’administration, les opérations d’activation ou de désactivation de la fonctionnalité de super utilisateur, ainsi que d’ajout ou de suppression de super utilisateurs sont enregistrées et peuvent être auditées à l’aide de la commande [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) . Quand les super utilisateurs déchiffrent des fichiers, l’action est enregistrée et peut être auditée à l’aide de la [ journalisation de l’utilisation](log-analyze-usage.md).

-   Si vous n’avez pas besoin de la fonctionnalité de super utilisateur pour les services quotidiens, activez-la uniquement lorsque nécessaire, puis désactivez-la à l’aide de l’applet de commande [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) .

L’extrait de journal suivant montre des exemples d’entrées lors de l’utilisation de l’applet de commande Get-AadrmAdminLog. Dans cet exemple, l’administrateur pour la société Contoso Ltd confirme que la fonctionnalité de super utilisateur est désactivée, ajoute Richard Simone comme super utilisateur, vérifie que celui-ci est bien le seul super utilisateur configuré pour Azure RMS, puis active la fonctionnalité de super utilisateur pour permettre à Richard de déchiffrer des fichiers protégés par un employé qui a quitté la société.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## Options de script pour les super utilisateurs
Une personne désignée comme super utilisateur pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] devra souvent supprimer la protection de plusieurs fichiers, dans plusieurs emplacements. Bien qu’il soit possible de le faire manuellement, il est plus efficace (et souvent plus fiable) de le faire à l’aide d’un script. Pour cela, [téléchargez l’outil de protection RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256). Utilisez ensuite les applets de commande [Unprotect-RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) et [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) en fonction des besoins.

Pour plus d’informations sur ces applets de commande, consultez [Azure Rights Management Protection Cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx) (Applets de commande pour la protection Azure Rights Management).

> [!NOTE]
> Le module PowerShell RMSProtection inclus dans l’outil de protection RMS est différent du principal [module Windows PowerShell pour Azure Rights Management](administer-powershell.md) et le complète. Le module RMSProtection prend en charge Azure RMS et AD RMS.




<!--HONumber=Apr16_HO4-->


