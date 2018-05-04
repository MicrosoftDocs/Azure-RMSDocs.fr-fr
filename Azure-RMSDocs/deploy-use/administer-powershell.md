---
title: Administration d’Azure Rights Management à l’aide de Windows PowerShell - AIP
description: Découvrez comment utiliser le module PowerShell pour le service Azure Rights Management (AADRM) pour Azure Information Protection afin d’administrer ce service dans votre organisation.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/13/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6e8c45c2ff7ae70dc321e2486151fddaf5791ccf
ms.sourcegitcommit: affda7572064edaf9e3b63d88f4a18d0d6932b13
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/16/2018
---
# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Administration du service Azure Rights Management à l’aide de Windows PowerShell

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Devez-vous utiliser PowerShell pour administrer le service Azure Rights Management pour Azure Information Protection ? Ce n’est peut-être pas nécessaire si l’ensemble de votre configuration peut être effectuée dans le portail Azure ou le portail Office 365. Toutefois, vous devez utiliser PowerShell pour certaines configurations avancées et vous pouvez aussi préférer utiliser PowerShell pour avoir un contrôle de ligne de commande et des scripts plus efficaces.

Le tableau de la section suivante répertorie certains des scénarios de configuration avancée qui utilisent PowerShell. Lorsque la configuration peut également être effectuée sans utiliser PowerShell, cette information est également incluse dans le tableau.

Pour obtenir la liste complète des applets de commande disponibles pour ce module avec plus d'informations sur chacune d'elles, consultez [AADRM](/powershell/module/aadrm/?view=azureipps#aadrm).

> [!NOTE]
> Pour connaître les instructions d'installation du module PowerShell, consultez [Installation du module PowerShell AADRM](install-powershell.md).

Outre ce module PowerShell côté service, le client Azure Information Protection installe un module PowerShell supplémentaire, **AzureInformationProtection**. Ce module client prend en charge la classification et la protection de plusieurs fichiers, permettant ainsi, par exemple, de protéger en bloc tous les fichiers d’un dossier. Pour plus d’informations, consultez [Utilisation de PowerShell avec le client Azure Information Protection](../rms-client/client-admin-guide-powershell.md) dans le Guide de l’administrateur.

## <a name="cmdlets-grouped-by-administration-task"></a>Applets de commande groupées par tâche d’administration

|Si vous avez besoin de…|…utilisez les applets de commande suivantes|
|-------------------|------------------------------|
|migrer de Rights Management local (AD RMS ou Windows RMS) vers Azure Information Protection.|[Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd)<br /><br />[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)|
|vous connecter au service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ou vous en déconnecter pour votre organisation.|[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)<br /><br />[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice)|
|Générer et gérer votre propre clé de locataire : scénario BYOK (Bring Your Own Key).|[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)<br /><br />[Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey)<br /><br />[Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys)|
|activer ou désactiver le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.<br /><br />Vous pouvez également effectuer ces actions dans les portails de gestion. Pour plus d’informations, consultez [Activation du service Azure Rights Management](activate-service.md).|[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm)<br /><br />[Disable-Aadrm](/powershell/aadrm/vlatest/disable-aadrm)|
|Gérer le site de suivi de document pour Azure Information Protection.|[Disable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/disable-aadrmdocumenttrackingfeature)<br /><br />[Enable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/enable-aadrmdocumenttrackingfeature)<br /><br />[Get-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/get-aadrmdocumenttrackingfeature)<br /><br />[Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/set-aadrmdonottrackusergroup)<br /><br />[Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup)<br /><br />[Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup)<br /><br />[Get-AadrmTrackingLog](/powershell/module/aadrm/Get-AadrmTrackingLog)<br /><br />[Get-AadrmDocumentLog](/powershell/module/aadrm/Get-AadrmDocumentLog)|
|Configurer des contrôles d’intégration pour un déploiement échelonné du service Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/get-aadrmonboardingcontrolpolicy)<br /><br />[Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy)|
|Créer et gérer des modèles Rights Management pour votre organisation.<br /><br />Vous pouvez également effectuer la plupart de ces actions à partir du portail Azure, bien que PowerShell offre un contrôle plus précis. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).|[Add-AadrmTemplate](/powershell/aadrm/vlatest/add-aadrmtemplate)<br /><br />[Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate)<br /><br />[Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate)<br /><br />[Get-AadrmTemplateProperty](/powershell/aadrm/vlatest/get-aadrmtemplateproperty)<br /><br />[Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate)<br /><br />[New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition)<br /><br />[Remove-AadrmTemplate](/powershell/aadrm/vlatest/remove-aadrmtemplate)<br /><br />[Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty)|
|Configurer le nombre maximal de jours pendant lesquels le contenu que votre organisation protège est accessibles sans connexion Internet (période de validité de licence d'utilisation).|[Get-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/get-aadrmmaxuselicensevaliditytime)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime)|
|gérer la fonctionnalité de super utilisateur de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)<br /><br />[Disable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/disable-aadrmsuperuserfeature)<br /><br />[Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser)<br /><br />[Get-AadrmSuperUser](/powershell/aadrm/vlatest/get-aadrmsuperuser)<br /><br />[Remove-AadrmSuperUser](/powershell/aadrm/vlatest/remove-aadrmsuperuser)<br /><br />[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup)<br /><br />[Get-AadrmSuperUserGroup](/powershell/aadrm/vlatest/get-aadrmsuperusergroup)<br /><br />[Clear-AadrmSuperUserGroup](/powershell/aadrm/vlatest/clear-aadrmsuperusergroup)|
|gérer les utilisateurs et les groupes autorisés à administrer le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Add-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/add-aadrmrolebasedadministrator)<br /><br />[Get-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/get-aadrmrolebasedadministrator)<br /><br />[Remove-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/remove-aadrmrolebasedadministrator)|
|obtenir un journal des tâches d’administration de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|journaliser et analyser la journalisation de l’utilisation de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Get-AadrmUserLog](/powershell/aadrm/vlatest/get-aadrmuserlog)|
|afficher la configuration actuelle de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] pour votre organisation.|[Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)|
|migrer votre organisation d’Azure Information Protection vers un déploiement AD RMS local.|[Set-AadrmMigrationUrl](/powershell/aadrm/vlatest/set-aadrmmigrationurl)<br /><br />[Get-AadrmMigrationUrl](/powershell/aadrm/vlatest/get-aadrmmigrationurl)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
