---
title: Administration de la protection à partir de Azure Information Protection à l’aide de PowerShell
description: Découvrez comment vous pouvez utiliser le module PowerShell pour le service de protection à partir de Azure Information Protection, pour administrer ce service pour votre locataire.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2dcb20c2bdc3f690f86968e8f3c45ae49849b827
ms.sourcegitcommit: 28c1de5f9d1426f160f0e0bafcf9f76769e662b6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71679095"
---
# <a name="administering-protection-from-azure-information-protection-by-using-powershell"></a>Administration de la protection à partir de Azure Information Protection à l’aide de PowerShell

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Avez-vous besoin d’utiliser PowerShell pour administrer le service de protection de Azure Information Protection ? Ce n’est peut-être pas nécessaire si l’ensemble de votre configuration peut être effectuée dans le portail Azure ou dans le Centre d’administration Microsoft 365. Toutefois, vous devez utiliser PowerShell pour certaines configurations avancées et vous pouvez aussi préférer utiliser PowerShell pour avoir un contrôle de ligne de commande et des scripts plus efficaces.

Le tableau de la section suivante répertorie certains des scénarios de configuration avancée qui utilisent PowerShell. Lorsque la configuration peut également être effectuée sans utiliser PowerShell, cette information est également incluse dans le tableau.

Pour obtenir la liste complète des applets de commande disponibles pour ce module, avec plus d’informations sur chacune d’elles, consultez [AIPService](/powershell/module/aipservice/?view=azureipps#aipservice).

> [!NOTE]
> Pour installer ce module PowerShell, consultez [installation du module PowerShell AIPService](install-powershell.md).

Outre ce module PowerShell côté service, le client Azure Information Protection installe un module PowerShell supplémentaire, **AzureInformationProtection**. Ce module client prend en charge la classification et la protection de plusieurs fichiers, permettant ainsi, par exemple, de protéger en bloc tous les fichiers d’un dossier. Pour plus d’informations, consultez [Utilisation de PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) dans le Guide de l’administrateur.

## <a name="cmdlets-grouped-by-administration-task"></a>Applets de commande groupées par tâche d’administration

|Si vous avez besoin de…|…utilisez les applets de commande suivantes|
|-------------------|------------------------------|
|Migrer de Rights Management local (AD RMS ou Windows RMS) vers Azure Information Protection.|[Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)<br /><br />[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)|
|vous connecter au service Rights Management ou vous en déconnecter pour votre organisation.|[Connect-AipService](/powershell/module/aipservice/connect-aipservice)<br /><br />[Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)|
|générer et gérer votre propre clé de locataire : scénario BYOK (Bring Your Own Key).|[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)<br /><br />[Use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey)<br /><br />[Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys)|
|activer ou désactiver le service Rights Management pour votre organisation.<br /><br />Vous pouvez également effectuer ces actions dans les portails de gestion. Pour plus d’informations, consultez [Activation du service de protection à partir d’Azure Information Protection](activate-service.md).|[Enable-AipService](/powershell/module/aipservice/enable-aipservice)<br /><br />[Disable-AipService](/powershell/module/aipservice/disable-aipservice)|
|Gérer le site de suivi de document pour Azure Information Protection.|[Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature)<br /><br />[Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)<br /><br />[Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature)<br /><br />[Set-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/set-aipservicedonottrackusergroup)<br /><br />[Clear-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Clear-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/get-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)<br /><br />[Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)|
|Configurer des contrôles d’intégration pour un déploiement échelonné du service Azure Rights Management.|[Get-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/get-aipserviceonboardingcontrolpolicy)<br /><br />[Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)|
|Créer et gérer des modèles Rights Management pour votre organisation.<br /><br />Vous pouvez également effectuer la plupart de ces actions à partir du portail Azure, bien que PowerShell offre un contrôle plus précis. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).|[Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)<br /><br />[Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)<br /><br />[Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)<br /><br />[Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)<br /><br />[Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetemplate)<br /><br />[New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)<br /><br />[Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)<br /><br />[Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)|
|Configurer le nombre maximal de jours pendant lesquels le contenu que votre organisation protège est accessibles sans connexion Internet (période de validité de licence d'utilisation).|[Get-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/get-aipservicemaxuselicensevaliditytime)<br /><br />[Set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)|
|gérer la fonctionnalité de superutilisateur de Rights Management pour votre organisation.|[Enable-AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)<br /><br />[Disable-AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature)<br /><br />[Add-AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser)<br /><br />[Get-AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)<br /><br />[Remove-AipServiceSuperUser](/powershell/module/aipservice/remove-aipservicesuperuser)<br /><br />[Set-AAipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup)<br /><br />[Get-AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup)<br /><br />[Clear-AipServiceSuperUserGroup](/powershell/module/aipservice/clear-aipservicesuperusergroup)|
|gérer les utilisateurs et les groupes autorisés à administrer le service Rights Management pour votre organisation.|[Add-Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator)<br /><br />[Get-Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator)<br /><br />[Remove-Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/remove-aipservicerolebasedadministrator)|
|obtenir un journal des tâches d’administration de Rights Management pour votre organisation.|[Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)|
|journaliser et analyser la journalisation de l’utilisation de Rights Management.|[Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)|
|afficher la configuration actuelle du service Rights Management pour votre organisation.|[Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)|
|Migrer votre organisation d’Azure Information Protection vers un déploiement AD RMS local.|[Set-AipServiceMigrationUrl](/powershell/module/aipservice/set-aipservicemigrationurl)<br /><br />[Get-AipServiceMigrationUrl](/powershell/module/aipservice/get-aipservicemigrationurl)|

