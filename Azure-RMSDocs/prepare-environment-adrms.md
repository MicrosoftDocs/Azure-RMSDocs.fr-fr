---
title: Préparer l’environnement pour Azure RMS et AD RMS
description: Conseils si vous avez Azure Rights Management avec AD RMS déployé.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/29/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c8219221fe9b932e0d09901dccf496df5f83ef76
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183923"
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Préparation de l’environnement pour Azure Rights Management quand vous avez également Active Directory Rights Management Services (AD RMS)

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Conseils pour l’utilisation des services AD RMS (Active Directory Rights Management Services)

Si le service Azure Rights Management est activé et que vous utilisez aussi AD RMS, cette combinaison n’est pas compatible. Sans étapes supplémentaires, certains ordinateurs peuvent automatiquement commencer à utiliser le service Azure Rights Management et se connecter à votre cluster AD RMS. Ce scénario n’est pas pris en charge et provoque des résultats imprévisibles. Il est donc important de suivre quelques étapes supplémentaires. 

**Pour vérifier si vous avez déployé AD RMS :**

1. Bien que cela soit facultatif, la plupart des déploiements AD RMS publient le point de connexion de service (SCP) dans Active Directory afin que les ordinateurs du domaine puissent détecter le cluster AD RMS. 
    
    Utilisez l’éditeur ADSI pour voir si vous avez un point de connexion de service publié dans Active Directory : `CN=Configuration [server name], CN=Services, CN=RightsManagementServices, CN=SCP`

2. Si vous n’utilisez pas un point de connexion de service, les ordinateurs Windows qui se connectent à un cluster AD RMS doivent être configurés pour la découverte du service côté client ou la redirection de licences à l’aide du registre Windows : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation` ou `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\ServiceLocation`
    
    Pour plus d’informations sur ces configurations de registre, consultez [Activation de la découverte du service côté client à l’aide du Registre Windows](./rms-client/client-deployment-notes.md#enabling-client-side-service-discovery-by-using-the-windows-registry) et [Redirection du trafic du serveur de licences](./rms-client/client-deployment-notes.md#redirecting-licensing-server-traffic).   

Si AD RMS est déployé pour votre organisation, envisagez si vous pouvez migrer vers Azure Information Protection. Azure Information Protection présente de nombreux avantages par rapport à AD RMS. Par exemple, une meilleure prise en charge des appareils mobiles et l’intégration avec les services Office 365, ainsi qu’avec Exchange Server et SharePoint Server. Pour plus d’informations, consultez [Comparaison d’Azure Information Protection avec AD RMS](compare-on-premise.md).

Lorsque vous migrez vers Azure Information Protection, vous ne perdez pas l’accès au contenu précédemment protégé, et vous n’êtes pas obligé d’ôter la protection sur votre contenu ou de le protéger à nouveau. Les documents et les e-mails qui étaient protégés par AD RMS peuvent toujours être ouverts, même après le déprovisionnement d’AD RMS.

Si vous décidez de migrer vers Azure Information Protection ou si vous décidez d’accepter les limitations dans l’utilisation de votre déploiement AD RMS actuel, vous devez tout d’abord vous assurer que le service Azure Rights Management est désactivé. Pour obtenir des instructions, suivez les étapes du scénario qui s’applique à votre cas :

- [Votre abonnement incluant Azure Rights Management a été acheté en février 2018 ou après](#your-subscription-was-purchased-during-or-after-february-2018)

- [Votre abonnement a été acheté avant ou pendant février 2018, et vous disposez d’Exchange Online](#your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online)

- [Vous voyez une option permettant d’activer la protection quand vous configurez Azure Information Protection dans le portail Azure](#you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection)


## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>Votre abonnement a été acheté en février 2018 ou après

Depuis fin février 2018, de nouveaux abonnements incluant Azure Information Protection activent le service Azure Rights Management par défaut. Si ce service est automatiquement activé pour vous alors que vous utilisez également Active Directory Rights Management Services (AD RMS), cette combinaison n’est pas compatible. Il est donc important que vous désactiviez le service Azure Rights Management dès que possible. 

### <a name="step-1-deactivate-azure-rights-management"></a>Étape 1 : Désactiver Azure Rights Management
Exécutez l’une des procédures suivantes pour désactiver Azure Rights Management.

> [!TIP]
> Vous pouvez également utiliser l’applet de commande Windows PowerShell [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) pour désactiver le service Azure Rights Management.

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Pour désactiver Rights Management à partir du Centre d’administration Microsoft 365

1. Accédez à la [page Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) réservée aux administrateurs Office 365.
    
    Si vous êtes invité à vous connecter, utilisez un compte qui est administrateur général pour Office 365.

2. Sur la page **rights management** , cliquez sur **désactiver**.

3.  À l’invite **Voulez-vous désactiver Rights Management ?**, cliquez sur **Désactiver**.

Le message **Rights Management n’est pas activé** s’affiche alors, avec une option pour l’activer.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Pour désactiver Rights Management à partir du portail Azure

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
    Si vous n’avez pas accédé au panneau Azure Information Protection avant, consultez les [étapes supplémentaires](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time) à suivre une seule fois pour ajouter ce panneau au portail.

2. Sélectionnez **Activation de la protection** dans les options du menu. 

3.  Dans le panneau **Azure Information Protection - Activation de la protection**, sélectionnez **Désactiver**. Sélectionnez **Oui** pour confirmer votre choix.

La barre d’informations affiche **Désactivation terminée** et **Désactiver** est maintenant remplacé par **Activer**. 

### <a name="step-2-start-planning-for-migration"></a>Étape 2 : Commencer la planification de la migration

Consultez les instructions pour la migration : [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)


## <a name="your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online"></a>Votre abonnement a été acheté avant ou pendant février 2018, et vous disposez d’Exchange Online

Microsoft commence à activer le service Azure Rights Management pour les abonnements incluant Azure Rights Management ou Azure Information Protection, et les locataires qui utilisent Exchange Online. Pour ces locataires, l’activation automatique commencera le 1er août 2018.

Si le service est activé automatiquement pour vous et que vous utilisez aussi AD RMS, cette combinaison n’est pas compatible ; il est donc important que votre locataire désactive la mise à jour automatique du service. 

### <a name="step-1-opt-out-from-the-automatic-service-update"></a>Étape 1 : Désactiver la mise à jour automatique du service

Utilisez la commande Exchange Online PowerShell [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration) suivante : `Set-IRMConfiguration -AutomaticServiceUpdateEnabled $false`

[Plus d’informations](https://support.office.com/article/protection-features-in-azure-information-protection-rolling-out-to-existing-office-365-tenants-7ad6f58e-65d7-4c82-8e65-0b773666634d) 

### <a name="step-2-start-planning-for-migration"></a>Étape 2 : Commencer la planification de la migration

Consultez les instructions pour la migration : [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)


## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Vous voyez une option pour activer la protection quand vous configurez Azure Information Protection

Le panneau **Azure Information Protection - Activation de la protection** contient une option permettant d’activer le service Azure Rights Management.  

Si vous utilisez également AD RMS, ne sélectionnez pas l’option **Activer**. Quand le service Azure Rights Management n’est pas activé, vous pouvez toujours utiliser Azure Information Protection pour les étiquettes qui appliquent uniquement la classification. Une stratégie par défaut spéciale est créée pour vous. Elle n’inclut pas la protection des données, et les options de configuration restent indisponibles jusqu’à ce que le service Azure Rights Management soit activé.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Étape 1 : Configurer votre stratégie Azure Information Protection pour la classification et l’étiquetage, sans protection

À partir du panneau **Azure Information Protection - Étiquettes**, affichez et configurez les étiquettes qui n’incluent pas d’options pour la protection des données. Pour plus d’informations sur la façon de configurer les paramètres d’étiquette et de stratégie, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Étape 2 : Commencer la planification de la migration

Consultez les instructions pour la migration : [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)

### <a name="step-3-configure-labels-for-protection"></a>Étape 3 : Configurer les étiquettes pour la protection

Une fois que vous avez activé le service Azure Rights Management dans le cadre du processus de migration, vous pouvez configurer des étiquettes pour la protection des données. Toutefois, si vous migrez des utilisateurs par lots, vérifiez que les étiquettes qui appliquent la protection ont pour portée uniquement les utilisateurs migrés.


