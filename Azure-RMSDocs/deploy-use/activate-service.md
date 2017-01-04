---
title: "Activation d’Azure Rights Management | Azure Information Protection"
description: "Le service Azure Rights Management doit être activé pour que votre organisation puisse commencer à protéger des documents et e-mails importants à l’aide d’applications et de services prenant en charge cette solution de protection des informations."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/09/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ced42d0856b992d3539575d64f5a49706f1768b3
ms.openlocfilehash: 80fd7a7ce1ac6b7a8b2867729dd3e09e9b106d9b


---

# <a name="activating-azure-rights-management"></a>Activation d'Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Quand le service Azure Rights Management d’Azure Information Protection est activé, votre organisation peut commencer à protéger des données importantes à l’aide d’applications et de services prenant en charge cette solution de protection des informations. Les administrateurs peuvent également gérer et surveiller les fichiers et messages électroniques protégés de votre organisation. Ce service doit être activé pour que vous puissiez commencer à utiliser les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans Office, SharePoint et Exchange, et à protéger des fichiers sensibles ou confidentiels.

Si vous voulez en savoir plus sur le service Azure Rights Management avant de l’activer (par exemple, les problèmes métier qu’il résout, certains scénarios d’utilisation classiques et son fonctionnement), consultez [Qu’est-ce qu’Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Avant d’activer [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], vérifiez que votre organisation a un plan de services incluant les services de protection des données Azure Rights Management. Si ce n’est pas le cas, vous ne pouvez pas activer Azure Rights Management.
>
> Vous devez avoir un [plan Premium Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) ou un [plan Office 365 incluant Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Quand le service Azure Rights Management est activé, tous les utilisateurs de votre organisation peuvent appliquer la protection des informations à leurs fichiers, et tous les utilisateurs peuvent ouvrir (consommer) des fichiers protégés par ce service. Toutefois, si vous préférez, vous pouvez restreindre les personnes autorisées à appliquer la protection des informations, en utilisant des contrôles d'intégration pour un déploiement échelonné. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](#configuring-onboarding-controls-for-a-phased-deployment) de cet article.

Pour découvrir comment activer le service Rights Management à partir de votre portail de gestion, choisissez si vous allez utiliser le centre d’administration Office 365 (version préliminaire ou classique) ou le portail de gestion classique Azure :


- [Centre d’administration Office 365 – préversion](activate-office365-preview.md)
- [Centre d’administration Office 365 – classique](activate-office365-classic.md)
- [Portail Azure Classic](activate-azure-classic.md)

En guise d’alternative, vous pouvez utiliser PowerShell pour activer [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] :

1. Installez l’outil d’administration Azure Rights Management, qui installe le module d’administration Azure Rights Management. Pour obtenir des instructions, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2. À partir d’une session PowerShell, exécutez [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) et, à l’invite, fournissez les détails du compte d’administrateur général de votre locataire Azure Information Protection.

3. Exécutez [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) pour activer le service Azure Rights Management.

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configuration de contrôles d'intégration pour un déploiement échelonné
Si vous ne souhaitez pas que tous les utilisateurs puissent protéger des fichiers immédiatement à l’aide d’Azure Rights Management, vous pouvez configurer des contrôles d’intégration d’utilisateur à l’aide de la commande PowerShell [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) . Vous pouvez exécuter cette commande avant ou après avoir activé le service Azure Rights Management.

> [!IMPORTANT]
> Pour utiliser cette commande, vous devez disposer au moins de la version **2.1.0.0** du [module Azure Rights Management PowerShell](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Pour vérifier la version que vous avez installée, exécutez : **(Get-Module aadrm – ListAvailable).Version**

Par exemple, si vous souhaitez initialement que seuls les administrateurs du groupe « Département informatique » (dont l'ID d'objet est fbb99ded-32a0-45f1-b038-38b519009503) puissent protéger du contenu à des fins de test, utilisez la commande suivante :

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Notez que pour cette option de configuration, vous devez spécifier un groupe. Vous ne pouvez pas spécifier des utilisateurs individuels. Pour obtenir l’ID d’objet du groupe, utilisez Azure AD PowerShell. Par exemple, pour la [version 1.0](https://msdn.microsoft.com/library/azure/jj151815\(v=azure.98\).aspx) du module, utilisez la commande [Get-MsolGroup](https://msdn.microsoft.com/library/azure/dn194130\(v=azure.98\).aspx).

Ou bien, si vous souhaitez vous assurer que seuls les utilisateurs disposant d’une licence appropriée pour utiliser Azure Information Protection puissent protéger du contenu :

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```

Pour plus d’informations sur cette applet de commande et pour obtenir des exemples supplémentaires, consultez l’aide de [Set-AadrmOnboardingControlPolicy](https://msdn.microsoft.com/library/dn857521.aspx).

Lorsque vous utilisez ces contrôles d'intégration, tous les utilisateurs de l'organisation peuvent toujours consommer du contenu protégé par votre sous-ensemble d'utilisateurs, mais ils ne peuvent pas appliquer la protection des informations à eux-mêmes à partir d'applications clientes. Par exemple, dans leurs clients Office, ils ne voient pas les modèles par défaut qui sont automatiquement publiés au moment de l’activation du service Azure Rights Management, ou les modèles personnalisés que vous pourriez configurer.  Les applications côté serveur, telles qu’Exchange, peuvent implémenter leurs propres contrôles utilisateur pour l’intégration de Rights Management et obtenir le même résultat.


## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] étant à présent activé pour votre organisation, consultez la [Feuille de route pour le déploiement d’Azure Information Protection](../plan-design/deployment-roadmap.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre Azure Information Protection à la disposition des utilisateurs et des administrateurs. 

Par exemple, vous pouvez utiliser des [modèles personnalisés](configure-custom-templates.md) pour faciliter l’application par les utilisateurs de la protection des informations à des fichiers, connecter vos serveurs locaux pour l’utilisation de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] via l’installation du [connecteur Rights Management](deploy-rms-connector.md) et déployer l’application de partage [Rights Management](../rms-client/sharing-app-windows.md) qui prend en charge la protection de tous les types de fichiers sur tous les appareils. 

Les services Office, comme Exchange Online et SharePoint Online, nécessitent une configuration supplémentaire avant que vous puissiez utiliser leurs fonctionnalités de gestion des droits relatifs à l’information (IRM). Pour plus d’informations sur la façon dont vos applications fonctionnent avec le service Rights Management, consultez [Comment les applications prennent en charge le service Azure Rights Management](../understand-explore/applications-support.md).

## <a name="comments"></a>Commentaires

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Dec16_HO2-->


