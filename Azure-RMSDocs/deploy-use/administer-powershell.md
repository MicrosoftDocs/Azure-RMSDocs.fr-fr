---
# required metadata

title: Administration d’Azure Rights Management à l’aide de Windows PowerShell | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Administration d’Azure Rights Management à l'aide de Windows PowerShell
Si vous pouvez activer Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) en utilisant le Centre d’administration [!INCLUDE[o365_2](../includes/o365_2_md.md)] ou le portail Azure Classic, vous pouvez également utiliser pour cela le module Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (AADRM).

Une fois [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] activé, il est probable qu’aucune tâche administrative supplémentaire ne soit nécessaires. Cependant, certains scénarios de configuration avancée peuvent vous obliger à utiliser le module Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Le tableau suivant répertorie certains des scénarios de configuration avancée qui utilisent Windows PowerShell. Pour obtenir la liste complète des applets de commande disponibles avec plus d'informations sur chacune d'elles, consultez [Applets de commande d’Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Si vous devez installer le module Windows PowerShell pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Il existe également un module Windows PowerShell complémentaire, **RMSProtection**, qui prend en charge Azure RMS et AD RMS. Ce module prend en charge la protection et la suppression de la protection de plusieurs fichiers. Il permet ainsi, par exemple, de protéger en bloc tous les fichiers d'un dossier. Pour plus d’informations, consultez la section [Options de script pour les super utilisateurs](configure-super-users.md#scripting-options-for-super-users) dans l’article [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](configure-super-users.md).

|Si vous avez besoin de…|…utilisez les applets de commande suivantes|
|-------------------|------------------------------|
|migrer de Rights Management local (AD RMS ou Windows RMS) vers [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|vous connecter au service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ou vous en déconnecter pour votre organisation.|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Générer et gérer votre propre clé de locataire : scénario BYOK (Bring Your Own Key).|[Add-AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|activer ou désactiver le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Désactiver ou activer le site de suivi de document pour Azure Rights Management.|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Configurer des contrôles d'intégration pour un déploiement échelonné d’Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Créer et gérer des modèles de stratégie de droits pour votre organisation.|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Expout-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Impout-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Configurer le nombre maximal de jours pendant lesquels le contenu que votre organisation protège est accessibles sans connexion Internet (période de validité de licence d'utilisation).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|gérer la fonctionnalité de super utilisateur de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|gérer les utilisateurs et les groupes autorisés à administrer le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|obtenir un journal des tâches d’administration de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|journaliser et analyser la journalisation de l’utilisation de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|afficher la configuration actuelle de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|migrer votre organisation de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] vers un déploiement AD RMS local.|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|





<!--HONumber=Apr16_HO3-->

