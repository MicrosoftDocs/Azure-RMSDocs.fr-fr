---
# required metadata

title: Activation d’Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Activation d'Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Quand vous activez [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), votre organisation peut commencer à protéger des données importantes à l’aide d’applications et services prenant en charge cette solution de protection des informations. Les administrateurs peuvent également gérer et surveiller les fichiers et messages électroniques protégés de votre organisation. Vous devez activer [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] avant de commencer à utiliser les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans Office, SharePoint et Exchange, et à protéger des fichiers sensibles ou confidentiels.

Si vous voulez en savoir plus sur Azure Rights Management avant d’activer le service (par exemple, les problèmes métier qu’il résout, certains scénarios d’utilisation classiques et son fonctionnement), consultez [Qu’est-ce qu’Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Avant d’activer [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], vérifiez que votre organisation dispose d’un plan de services incluant les services [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Si ce n'est pas le cas, vous ne pouvez pas activer Azure RMS.
>
> Pour plus d’informations, consultez [Abonnements cloud prenant en charge Azure RMS](../get-started/requirements-subscriptions.md).

Une fois Azure RMS activé, tous les utilisateurs de votre organisation peuvent appliquer la protection des informations à leurs fichiers, et tous les utilisateurs peuvent ouvrir (consommer) des fichiers protégés par Azure RMS. Toutefois, si vous préférez, vous pouvez restreindre les personnes autorisées à appliquer la protection des informations, en utilisant des contrôles d'intégration pour un déploiement échelonné. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](#configuring-onboarding-controls-for-a-phased-deployment) de cet article.

Pour découvrir comment activer Rights Management à partir de votre portail de gestion, choisissez si vous allez utiliser le centre d’administration Office 365 (version préliminaire ou classique) ou le portail de gestion classique Azure :


- [Centre d’administration Office 365 – version préliminaire](activate-office365-preview.md)
- [Centre d’administration Office 365 – classique](activate-office365-classic.md)
- [Portail Azure Classic](activate-azure-classic.md)

En guise d’alternative, vous pouvez utiliser Windows PowerShell pour activer [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] :

1. Installez l’outil d’administration Azure Rights Management, qui installe le module d’administration Azure Rights Management. Pour obtenir des instructions, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2. À partir d’une session Windows PowerShell, exécutez [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) et, à l’invite, fournissez les détails du compte d’administrateur global de votre client Azure RMS.

3. Exécutez [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) pour activer le service Azure RMS.

## Configuration de contrôles d'intégration pour un déploiement échelonné
Si vous ne souhaitez pas que tous les utilisateurs puissent protéger des fichiers immédiatement à l'aide d'Azure RMS, vous pouvez configurer des contrôles d'intégration d'utilisateur à l'aide de la commande Windows PowerShell [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) . Vous pouvez exécuter cette commande avant ou après avoir activé Azure RMS.

> [!IMPORTANT]Pour utiliser cette commande, vous devez disposer au moins de la version **2.1.0.0** du [module Azure RMS Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Pour vérifier la version que vous avez installée, exécutez : **(Get-Module aadrm – ListAvailable).Version**

Par exemple, si vous souhaitez initialement que seuls les administrateurs du groupe « Département informatique » (dont l'ID d'objet est fbb99ded-32a0-45f1-b038-38b519009503) puissent protéger du contenu à des fins de test, utilisez la commande suivante :

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Notez que pour cette option de configuration, vous devez spécifier un groupe. Vous ne pouvez pas spécifier des utilisateurs individuels.

Ou bien, si vous souhaitez vous assurer que seuls les utilisateurs disposant d'une licence appropriée pour utiliser Azure RMS puissent protéger du contenu :

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Lorsque vous utilisez ces contrôles d'intégration, tous les utilisateurs de l'organisation peuvent toujours consommer du contenu protégé par votre sous-ensemble d'utilisateurs, mais ils ne peuvent pas appliquer la protection des informations à eux-mêmes à partir d'applications clientes. Par exemple, dans leurs clients Office, ils ne voient pas les modèles par défaut qui sont automatiquement publiés lors de l'activation d'Azure RMS, ou les modèles personnalisés que vous pourriez configurer.  Les applications côté serveur, telles qu'Exchange, peuvent implémenter leurs propres contrôles utilisateur pour l'intégration de RMS et obtenir le même résultat.


## Étapes suivantes
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] étant à présent activé pour votre organisation, consultez la [Feuille de route pour le déploiement d’Azure Rights Management](../plan-design/deployment-roadmap.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] à la disposition des utilisateurs et des administrateurs. 

Par exemple, vous pouvez utiliser des [modèles personnalisés](configure-custom-templates.md) pour faciliter l’application par les utilisateurs de la protection des informations à des fichiers, connecter vos serveurs locaux pour l’utilisation de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] via l’installation du [connecteur RMS](deploy-rms-connector.md) et déployer l’application de partage [Rights Management](../rms-client/sharing-app-windows.md) qui prend en charge la protection de tous les types de fichiers sur tous les appareils. 

Les services Office, comme Exchange Online et SharePoint Online, nécessitent une configuration supplémentaire avant que vous puissiez utiliser leurs fonctionnalités de gestion des droits relatifs à l’information (IRM). Pour plus d’informations sur la façon dont vos applications fonctionnent avec [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consultez [Comment les applications prennent en charge Azure Rights Management](../understand-explore/applications-support.md).



<!--HONumber=May16_HO3-->


