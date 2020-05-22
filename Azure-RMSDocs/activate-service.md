---
title: Activation du service de protection à partir de Azure Information Protection
description: Le service de protection, Azure Rights Management, doit être activé pour que votre organisation puisse commencer à protéger des documents et des e-mails à l’aide d’applications et de services prenant en charge cette solution de protection des informations.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3b4dd50ba7afd8a6d3d1c85e66b6cfab12fa88ed
ms.sourcegitcommit: 8499602fba94fbfa28d7682da2027eeed6583c61
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83746413"
---
# <a name="activating-the-protection-service-from-azure-information-protection"></a>Activation du service de protection à partir de Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> Ces informations de configuration sont destinées aux administrateurs qui sont responsables d’un service qui s’applique à tous les utilisateurs dans une organisation. Si vous recherchez des informations et une aide utilisateur sur l’utilisation des fonctionnalités de Rights Management pour une application spécifique ou sur l’ouverture d’un fichier ou e-mail protégé par des droits, utilisez l’aide et les conseils qui accompagnent votre application.
>
> Par exemple, pour les applications Office, cliquez sur l'icône d'aide, puis entrez les termes recherchés, comme **Rights Management** ou **IRM**. Pour le client Azure Information Protection pour Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](./rms-client/client-user-guide.md).
>
> Pour le support technique et d’autres questions sur le service, consultez les informations dans [Options de support technique et ressources de la communauté](information-support.md#support-options-and-community-resources).

Lorsque le service de protection pour Azure Information Protection est activé pour votre organisation, les administrateurs et les utilisateurs peuvent commencer à protéger des données importantes à l’aide d’applications et de services qui prennent en charge cette solution de protection des informations. Les administrateurs peuvent également gérer et surveiller les documents et e-mail protégés de votre organisation. 


## <a name="do-you-need-to-activate-the-protection-service-azure-rights-management"></a>Avez-vous besoin d’activer le service de protection, Azure Rights Management ?

Si vous disposez d’un plan de service incluant Azure Rights Management, vous n’aurez peut-être pas besoin d’activer le service :

- **Si vous avez obtenu votre abonnement incluant Azure Rights Management ou Azure Information Protection fin février 2018 ou après :** le service est automatiquement activé pour vous. Vous n’avez pas à activer le service, sauf si vous ou un autre administrateur global pour votre organisation a désactivé Azure Rights Management.

- **Si votre abonnement incluant Azure Rights Management ou Azure Information Protection a été obtenu avant ou pendant février 2018 :** Microsoft commence à activer le service Azure Rights Management pour ces abonnements si votre locataire utilise Exchange Online. Pour ces abonnements, l’activation automatique commencera le 1er août 2018 lorsque le service sera activé pour vous, sauf si vous constatez que **AutomaticServiceUpdateEnabled** est défini sur **false** lorsque vous exécutez [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps). 

Si aucun des scénarios suivants ne s’applique à vous, vous devez activer manuellement le service de protection. 

Quand le service est activé, tous les utilisateurs de votre organisation peuvent appliquer la protection des informations à leurs documents et e-mails, et tous les utilisateurs peuvent ouvrir (consommer) des documents et e-mails protégés par le service Azure Rights Management. Toutefois, si vous préférez, vous pouvez restreindre les personnes autorisées à appliquer la protection des informations, en utilisant des contrôles d'intégration pour un déploiement échelonné. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](#configuring-onboarding-controls-for-a-phased-deployment) de cet article.

## <a name="how-to-activate-or-confirm-the-status-of-the-protection-service"></a>Comment activer ou confirmer l’état du service de protection 

> [!IMPORTANT]
> N’activez pas le service de protection si vous avez services AD RMS (Active Directory Rights Management Services) (AD RMS) déployé pour votre organisation. [Plus d’informations](prepare-environment-adrms.md)

Pour utiliser cette solution de protection des données, votre organisation doit disposer d’un plan de service qui inclut le service Azure Rights Management d’Azure Information Protection. Sans cela, le service de protection ne peut pas être activé. Vous devez disposer d’un des éléments suivants :

- Un [plan Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- Un [plan Office 365 incluant Rights Management](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Lorsque le service de protection est activé, tous les utilisateurs de votre organisation peuvent appliquer la protection des informations à leurs documents et e-mails, et tous les utilisateurs peuvent ouvrir (consommer) des documents et des e-mails qui ont été protégés par ce service. Toutefois, si vous préférez, vous pouvez restreindre les personnes autorisées à appliquer la protection des informations, en utilisant des contrôles d'intégration pour un déploiement échelonné. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](#configuring-onboarding-controls-for-a-phased-deployment) de cet article.

## <a name="choosing-your-activation-method"></a>Choix de votre méthode d’activation

Pour obtenir des instructions sur l’activation du service de protection à partir de votre portail de gestion, indiquez si vous souhaitez utiliser le centre d’administration Microsoft 365 ou le Portail Azure :

- [Centre d’administration Microsoft 365](activate-office365.md) : nécessite un compte d’administrateur général

- [Portail Azure](activate-azure.md) : ne nécessite pas de compte Administrateur général

Vous pouvez également utiliser la commande Windows PowerShell suivante :

1. Installez le module AIPService pour configurer et gérer le service de protection. Pour obtenir des instructions, consultez [installation du module PowerShell AIPService](install-powershell.md).

2. À partir d’une session PowerShell, exécutez [Connect-AipService](/powershell/module/aipservice/connect-aipservice)et, lorsque vous y êtes invité, fournissez les détails du compte d’administrateur général pour votre locataire Azure information protection.

3. Exécutez la [AipService](/powershell/module/aipservice/get-aipservice) pour vérifier si le service de protection est activé. L’état **Activé** confirme l’activation tandis que l’état **Désactivé** indique que le service est désactivé.

4. Pour activer le service, exécutez [Enable-AipService](/powershell/module/aipservice/enable-aipservice).

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configuration de contrôles d'intégration pour un déploiement échelonné
Si vous ne souhaitez pas que tous les utilisateurs puissent protéger des documents et des e-mails immédiatement à l’aide de Azure Information Protection, vous pouvez configurer des contrôles d’intégration d’utilisateur à l’aide de la commande PowerShell [Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) . Vous pouvez exécuter cette commande avant ou après avoir activé le service Azure Rights Management.

Par exemple, si vous souhaitez initialement que seuls les administrateurs du groupe « Département informatique » (dont l'ID d'objet est fbb99ded-32a0-45f1-b038-38b519009503) puissent protéger du contenu à des fins de test, utilisez la commande suivante :

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

Notez que pour cette option de configuration, vous devez spécifier un groupe. Vous ne pouvez pas spécifier des utilisateurs individuels. Pour obtenir l’ID d’objet du groupe, vous pouvez utiliser Azure AD PowerShell. Par exemple, pour la version 1.0 du module, utilisez la commande [Get-MsolGroup](/powershell/msonline/v1/get-msolgroup). Vous pouvez aussi copier la valeur **ID d’objet** du groupe à partir du portail Azure.

Si vous voulez que seuls les utilisateurs disposant d’une licence appropriée pour utiliser Azure Information Protection puissent protéger du contenu :

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $True
```

Quand vous n’avez plus besoin d’utiliser des contrôles d’intégration, que vous ayez utilisé l’option de groupe ou de gestion des licences, exécutez :

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
```

Pour plus d’informations sur cette applet de commande et des exemples supplémentaires, consultez l’aide de [Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) .

Lorsque vous utilisez ces contrôles d'intégration, tous les utilisateurs de l'organisation peuvent toujours consommer du contenu protégé par votre sous-ensemble d'utilisateurs, mais ils ne peuvent pas appliquer la protection des informations à eux-mêmes à partir d'applications clientes. Par exemple, ils ne voient pas dans leurs applications Office les modèles de protection par défaut qui sont automatiquement publiés lors de l’activation du service de protection, ou les modèles personnalisés que vous pouvez configurer. Les applications côté serveur, telles qu’Exchange, peuvent implémenter leurs propres contrôles par utilisateur pour obtenir le même résultat. Par exemple, pour empêcher les utilisateurs de protéger des e-mails dans Outlook sur le web, utilisez [Set-OwaMailboxPolicy](/powershell/module/exchange/client-access/set-owamailboxpolicy?view=exchange-ps) pour définir le paramètre *IRMEnabled* sur *$false*.


## <a name="next-steps"></a>Étapes suivantes
Lorsque le service de protection est activé pour votre organisation, utilisez la feuille de [route de déploiement Azure information protection](deployment-roadmap.md) pour vérifier si d’autres étapes de configuration peuvent s’avérer nécessaires avant de déployer des Azure information protection pour les utilisateurs et les administrateurs. 

Par exemple, vous pouvez utiliser des [modèles](configure-policy-templates.md) pour faciliter l’application de la protection aux fichiers par les utilisateurs, connecter vos serveurs locaux pour utiliser le service de protection en installant le [connecteur Rights Management](deploy-rms-connector.md)et déployer le [client Azure information protection](./rms-client/aip-client.md) qui prend en charge la protection de tous les types de fichiers sur tous les appareils. 

Les services Office, tels qu’Exchange Online et Microsoft SharePoint, nécessitent une configuration supplémentaire avant que vous puissiez utiliser leurs fonctionnalités d’Rights Management d’informations (IRM). Pour plus d’informations sur la façon dont vos applications fonctionnent avec le service de protection, Azure Rights Management, consultez [Comment les applications prennent en charge le service azure Rights Management](applications-support.md).

