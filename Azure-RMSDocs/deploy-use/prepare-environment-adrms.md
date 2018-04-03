---
title: Préparer l’environnement pour Azure RMS et AD RMS
description: Conseils si vous avez Azure Rights Management avec AD RMS déployé.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a233ddab67832e2de59b1fc0727296a8f3017db7
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Préparation de l’environnement pour Azure Rights Management quand vous avez également Active Directory Rights Management Services (AD RMS)

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Conseils importants si vous utilisez déjà Active Directory Rights Management Services (AD RMS) et que l’un des scénarios suivants s’applique :

- [Votre abonnement incluant Azure Rights Management a été acheté en février 2018 ou après](#your-subscription-was-purchased-during-or-after-february-2018).

- [Vous voyez une option permettant d’activer la protection quand vous configurez Azure Information Protection dans le portail Azure](#you-see-an-option-to activate-azure-rights-management-when-you-configure-azure-information-protection)

## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>Votre abonnement a été acheté en février 2018 ou après

Depuis fin février 2018, de nouveaux abonnements incluant Azure Information Protection activent le service Azure Rights Management par défaut. Si ce service est automatiquement activé pour vous alors que vous utilisez également Active Directory Rights Management Services (AD RMS), cette combinaison n’est pas compatible. Sans étapes supplémentaires, certains ordinateurs peuvent automatiquement commencer à utiliser le service Azure Rights Management et se connecter à votre cluster AD RMS. Ce scénario n’est pas pris en charge et provoque des résultats imprévisibles. Il est donc important de désactiver Azure Rights Management dès que possible. 

Quand vous êtes prêt à migrer les ordinateurs d’AD RMS vers le service Azure Rights Management, vous pouvez démarrer le processus de migration. L’une des étapes de la migration consiste à réactiver le service, mais cette opération s’effectue une fois que vous avez exporté les informations de configuration d’AD RMS vers le service Azure Rights Management. Cet ordre garantit que les documents et les e-mails qui étaient protégés par AD RMS peuvent toujours être ouverts.

La première étape consiste à désactiver le service Azure Rights Management.

### <a name="step-1-deactivate-azure-rights-management"></a>Étape 1 : Désactiver Azure Rights Management
Exécutez l’une des procédures suivantes pour désactiver [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Vous pouvez également utiliser l’applet de commande Windows PowerShell [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) pour désactiver [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Pour désactiver Rights Management à partir du centre d’administration Office 365

1. Accédez à la [page Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) réservée aux administrateurs Office 365.
    
    Si vous êtes invité à vous connecter, utilisez un compte qui est administrateur général pour Office 365.

2. Sur la page **rights management** , cliquez sur **désactiver**.

3.  À l’invite **Voulez-vous désactiver Rights Management ?**, cliquez sur **Désactiver**.

Le message **Rights Management n’est pas activé** s’affiche alors, avec une option pour l’activer.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Pour désactiver Rights Management à partir du portail Azure

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
    Si vous n’avez pas accédé au panneau Azure Information Protection avant, consultez les [étapes supplémentaires](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time) à suivre une seule fois pour ajouter ce panneau au portail.

2. Dans le panneau **Azure Information Protection** initial, sélectionnez **Activation de la protection**. 

3.  Dans le panneau **Azure Information Protection - Activation de la protection**, sélectionnez **Désactiver**. Sélectionnez **Oui** pour confirmer votre choix.

La barre d’informations affiche **Désactivation terminée** et **Désactiver** est maintenant remplacé par **Activer**. 

### <a name="step-2-start-planning-for-migration"></a>Étape 2 : Commencer la planification de la migration

Consultez les instructions de migration : [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Vous voyez une option pour activer la protection quand vous configurez Azure Information Protection

Le panneau **Azure Information Protection - Activation de la protection** contient une option permettant d’activer le service Azure Rights Management (Azure RMS).  

Si vous utilisez également d’Active Directory Rights Management Services (AD RMS), ne sélectionnez pas l’option **Activer**. L’activation d’Azure Rights Management quand vous avez également AD RS n’est pas une combinaison compatible. Ce scénario n’est pas pris en charge et provoque des résultats imprévisibles. Il est donc important de ne pas activer Azure Rights Management à ce stade.  

Quand vous êtes prêt à migrer les ordinateurs d’AD RMS vers le service Azure Rights Management, vous pouvez démarrer un processus de migration. L’une des étapes de la migration consiste à activer le service, mais cette opération s’effectue une fois que vous avez exporté les informations de configuration d’AD RMS vers le service Azure Rights Management. Ce processus permet de s’assurer que les documents et e-mails qui étaient protégés par AD RMS peuvent toujours être ouverts. 

Quand le service Azure Rights Management n’est pas activé, vous pouvez toujours utiliser Azure Information Protection pour les étiquettes qui appliquent uniquement la classification. Une stratégie par défaut spéciale est créée pour vous. Elle n’inclut pas la protection des données, et les options de configuration restent indisponibles jusqu’à ce que le service Azure Rights Management soit activé.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Étape 1 : Configurer votre stratégie Azure Information Protection pour la classification et l’étiquetage, sans protection

À partir du panneau **Azure Information Protection** initial, sélectionnez **Stratégie globale** pour afficher et configurer votre stratégie par défaut qui n’inclut pas d’options de protection des données. Pour en savoir plus, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Étape 2 : Commencer la planification de la migration

Consultez les instructions de migration : [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-start-to-configure-labels-for-protection"></a>Étape 3 : Commencer à configurer les étiquettes pour la protection

Une fois que vous avez activé le service Azure Rights Management dans le cadre du processus de migration, vous pouvez configurer des étiquettes pour la protection des données. Toutefois, si vous migrez des utilisateurs par lots, vérifiez que les étiquettes qui appliquent la protection ont pour portée uniquement les utilisateurs migrés.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

