---
title: Activation du service de protection d’Azure Information Protection
description: Le service de protection Azure Rights Management, doit être activé que votre organisation puisse commencer à protéger des documents et e-mails à l’aide d’applications et services prenant en charge cette solution de protection des informations.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 16c3ded1ea8f5d7c2191b994ec63132bd5f9bf1e
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520322"
---
# <a name="activating-the-protection-service-from-azure-information-protection"></a>Activation du service de protection d’Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> Ces informations de configuration sont destinées aux administrateurs qui sont responsables d’un service qui s’applique à tous les utilisateurs dans une organisation. Si vous recherchez des informations et une aide utilisateur sur l’utilisation des fonctionnalités de Rights Management pour une application spécifique ou sur l’ouverture d’un fichier ou e-mail protégé par des droits, utilisez l’aide et les conseils qui accompagnent votre application.
>
> Par exemple, pour les applications Office, cliquez sur l'icône d'aide, puis entrez les termes recherchés, comme **Rights Management** ou **IRM**. Pour le client Azure Information Protection pour Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](./rms-client/client-user-guide.md).
>
> Pour le support technique et d’autres questions sur le service, consultez les informations dans [Options de support technique et ressources de la communauté](information-support.md#support-options-and-community-resources).

Lorsque le service de protection pour Azure Information Protection est activé pour votre organisation, les administrateurs et les utilisateurs peuvent démarrer protéger les données importantes à l’aide d’applications et services prenant en charge cette solution de protection des informations. Les administrateurs peuvent également gérer et surveiller les documents et e-mail protégés de votre organisation. 


## <a name="do-you-need-to-activate-the-protection-service-azure-rights-management"></a>Vous devez activer le service de protection, Azure Rights Management ?

Si vous disposez d’un plan de service incluant Azure Rights Management, vous n’aurez peut-être pas besoin d’activer le service :

- **Si vous avez obtenu votre abonnement incluant Azure Rights Management ou Azure Information Protection fin février 2018 ou après :** le service est automatiquement activé pour vous. Vous n’avez pas à activer le service, sauf si vous ou un autre administrateur global pour votre organisation a désactivé Azure Rights Management.

- **Si vous avez obtenu votre abonnement incluant Azure Rights Management ou Azure Information Protection avant ou courant février 2018 :** Microsoft commence à activer le service Azure Rights Management pour ces abonnements si votre locataire utilise Exchange Online. Pour ces abonnements, l’activation automatique commencera le 1er août 2018 lorsque le service sera activé pour vous, sauf si vous constatez que **AutomaticServiceUpdateEnabled** est défini sur **false** lorsque vous exécutez [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps). 

Si aucun des scénarios suivants ne s’applique à vous, vous devez activer manuellement le service de protection. 

Quand le service est activé, tous les utilisateurs de votre organisation peuvent appliquer la protection des informations à leurs documents et e-mails, et tous les utilisateurs peuvent ouvrir (consommer) des documents et e-mails protégés par le service Azure Rights Management. Toutefois, si vous préférez, vous pouvez restreindre les personnes autorisées à appliquer la protection des informations, en utilisant des contrôles d'intégration pour un déploiement échelonné. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](#configuring-onboarding-controls-for-a-phased-deployment) de cet article.

## <a name="how-to-activate-or-confirm-the-status-of-the-protection-service"></a>Comment activer ou vérifier l’état du service de protection 

> [!IMPORTANT]
> N’activez pas le service de protection si vous avez Active Directory Rights Management Services (AD RMS) déployé pour votre organisation. [Plus d’informations](prepare-environment-adrms.md)

Pour utiliser cette solution de protection des données, votre organisation doit disposer d’un plan de service qui inclut le service Azure Rights Management d’Azure Information Protection. Sans cela, le service de protection ne peut pas être activé. Vous devez disposer d’un des éléments suivants :

- Un [plan Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- Un [plan Office 365 incluant Rights Management](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Lorsque le service de protection est activé, tous les utilisateurs de votre organisation peuvent appliquer la protection des informations à leurs documents et e-mails, et tous les utilisateurs peuvent ouvrir (consommer) des documents et e-mails qui ont été protégés par ce service. Toutefois, si vous préférez, vous pouvez restreindre les personnes autorisées à appliquer la protection des informations, en utilisant des contrôles d'intégration pour un déploiement échelonné. Pour plus d’informations, consultez la section [Configuration de contrôles d’intégration pour un déploiement échelonné](#configuring-onboarding-controls-for-a-phased-deployment) de cet article.

## <a name="choosing-your-activation-method"></a>Choix de votre méthode d’activation

Pour savoir comment activer le service de protection à partir de votre portail de gestion, indiquez si vous souhaitez utiliser le centre d’administration Microsoft 365 ou le portail Azure :

- [Centre d’administration Microsoft 365](activate-office365.md) : nécessite un compte d’administrateur général

- [Portail Azure](activate-azure.md) : ne nécessite pas de compte Administrateur général

Vous pouvez également utiliser la commande Windows PowerShell suivante :

1. Installez le module AIPService, pour configurer et gérer le service de protection. Pour obtenir des instructions, consultez [installation du module PowerShell de AIPService](install-powershell.md).

2. À partir d’une session PowerShell, exécutez [Connect-AipService](/powershell/module/aipservice/connect-aipservice)et vous y êtes invité, fournissez les détails du compte administrateur général de votre locataire Azure Information Protection.

3. Exécutez [Get-AipService](/powershell/module/aipservice/get-aipservice) pour confirmer si le service de protection est activé. L’état **Activé** confirme l’activation tandis que l’état **Désactivé** indique que le service est désactivé.

4. Pour activer le service, exécutez [Enable-AipService](/powershell/module/aipservice/enable-aipservice).

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configuration de contrôles d'intégration pour un déploiement échelonné
Si vous ne souhaitez pas tous les utilisateurs puissent protéger des documents et e-mails immédiatement à l’aide d’Azure Information Protection, vous pouvez configurer des contrôles d’intégration à l’aide de la [Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) PowerShell commande. Vous pouvez exécuter cette commande avant ou après avoir activé le service Azure Rights Management.

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

Pour plus d’informations sur cette applet de commande et des exemples supplémentaires, consultez le [Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) aide.

Lorsque vous utilisez ces contrôles d'intégration, tous les utilisateurs de l'organisation peuvent toujours consommer du contenu protégé par votre sous-ensemble d'utilisateurs, mais ils ne peuvent pas appliquer la protection des informations à eux-mêmes à partir d'applications clientes. Par exemple, ils ne voient pas dans leurs applications Office les modèles de protection par défaut qui sont automatiquement publiés lors le service de protection est activé, ou des modèles personnalisés que vous pourriez configurer. Les applications côté serveur, telles qu’Exchange, peuvent implémenter leurs propres contrôles utilisateur pour obtenir le même résultat. Par exemple, pour empêcher les utilisateurs de protéger des e-mails dans Outlook sur le web, utilisez [Set-OwaMailboxPolicy](/powershell/module/exchange/client-access/set-owamailboxpolicy?view=exchange-ps) pour définir le paramètre *IRMEnabled* sur *$false*.


## <a name="next-steps"></a>Étapes suivantes
Lorsque le service de protection est activé pour votre organisation, utilisez le [calendrier de déploiement d’Azure Information Protection](deployment-roadmap.md) pour déterminer si d’autres étapes de configuration que vous devrez peut-être effectuer avant de mettre Azure Protection des informations aux utilisateurs et aux administrateurs. 

Par exemple, vous souhaiterez peut-être utiliser [modèles](configure-policy-templates.md) pour faciliter aux utilisateurs d’appliquer une protection aux fichiers, connecter vos serveurs locaux pour utiliser le service de protection en installant le [connecteur Rights Management](deploy-rms-connector.md)et déployer le [client Azure Information Protection](./rms-client/aip-client.md) qui prend en charge la protection tous les types de fichiers sur tous les appareils. 

Les services Office, comme Exchange Online et SharePoint Online, nécessitent une configuration supplémentaire avant que vous puissiez utiliser leurs fonctionnalités de gestion des droits relatifs à l’information (IRM). Pour plus d’informations sur le fonctionnement de vos applications avec le service de protection, Azure Rights Management, consultez [comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

