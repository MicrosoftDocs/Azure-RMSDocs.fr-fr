---
title: "Administration du service Azure Rights Management à l’aide de Windows PowerShell | Azure Information Protection"
description: "Découvrez comment utiliser le module PowerShell pour le service Azure Rights Management (AADRM) pour Azure Information Protection afin d’administrer ce service dans votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/14/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 16d6a8a00db28c23fd650a1b8beba00333ba6ea4
ms.openlocfilehash: f9aa0d5910ba4868878ae54c446793bfc031d3c2


---

# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Administration du service Azure Rights Management à l’aide de Windows PowerShell

>*S’applique à : Azure Information Protection, Office 365*

Devez-vous utiliser PowerShell pour administrer le service Azure Rights Management pour Azure Information Protection ? Ce n’est peut-être pas le cas si vous êtes un administrateur global et si la seule configuration requise pour ce service est l’activation (ou la désactivation), et la configuration des modèles Rights Management.

Toutefois, vous devrez utiliser PowerShell pour les configurations plus complexes, et au cas où vous ne seriez pas un administrateur global, mais où vous disposeriez d’autorisations d’administration du service accordées par un administrateur global. Vous préférerez peut-être utiliser PowerShell pour un contrôle plus efficace des lignes de commande et des scripts.

Le tableau de la section suivante répertorie certains des scénarios de configuration avancée qui utilisent PowerShell. Lorsque la configuration peut également être effectuée sans utiliser PowerShell, cette information est également incluse dans le tableau.

Pour obtenir la liste complète des applets de commande disponibles avec plus d'informations sur chacune d'elles, consultez [Applets de commande d’Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Pour installer le module PowerShell, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Outre ce module PowerShell côté service, le client Azure Information Protection installe un module PowerShell supplémentaire, **AzureInformationProtection**. Ce module client prend en charge la classification et la protection de plusieurs fichiers, permettant ainsi, par exemple, de protéger en bloc tous les fichiers d’un dossier. Pour plus d’informations, consultez [Utilisation de PowerShell avec le client Azure Information Protection](../rms-client/client-admin-guide-powershell.md) dans le Guide de l’administrateur.

## <a name="cmdlets-grouped-by-administration-task"></a>Applets de commande groupées par tâche d’administration

|Si vous avez besoin de…|…utilisez les applets de commande suivantes|
|-------------------|------------------------------|
|migrer de Rights Management local (AD RMS ou Windows RMS) vers Azure Information Protection.|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|vous connecter au service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ou vous en déconnecter pour votre organisation.|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Générer et gérer votre propre clé de locataire : scénario BYOK (Bring Your Own Key).|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|activer ou désactiver le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.<br /><br />Vous pouvez également effectuer ces actions dans les portails de gestion. Pour plus d’informations, consultez [Activation du service Azure Rights Management](activate-service.md).|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Désactiver ou activer le site de suivi de document pour Azure Information Protection.|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Configurer des contrôles d’intégration pour un déploiement échelonné du service Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Créer et gérer des modèles Rights Management pour votre organisation.<br /><br />Vous pouvez également effectuer la plupart de ces actions à partir du portail Azure Classic, bien que PowerShell offre un contrôle plus précis. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour le service Azure Rights Management](configure-custom-templates.md).|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Configurer le nombre maximal de jours pendant lesquels le contenu que votre organisation protège est accessibles sans connexion Internet (période de validité de licence d'utilisation).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|gérer la fonctionnalité de super utilisateur de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|gérer les utilisateurs et les groupes autorisés à administrer le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|obtenir un journal des tâches d’administration de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|journaliser et analyser la journalisation de l’utilisation de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|afficher la configuration actuelle de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|migrer votre organisation d’Azure Information Protection vers un déploiement AD RMS local.|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Feb17_HO2-->


