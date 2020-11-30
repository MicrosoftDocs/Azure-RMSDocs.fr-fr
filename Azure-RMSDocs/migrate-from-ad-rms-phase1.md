---
title: Migrer un déploiement AD RMS vers Azure Information Protection - Phase 1
description: Phase 1 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 1 à 3 de la migration d’AD RMS vers Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 13c63f2e96b27a31b9afb91fbc8c03b9b198f9c1
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316821"
---
# <a name="migration-phase-1---preparation"></a>Phase de migration 1 : Préparation

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations suivantes pour la Phase 1 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 1 à 3 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) et préparent votre environnement pour la migration sans aucun impact sur vos utilisateurs.

## <a name="step-1-install-the-aipservice-powershell-module-and-identify-your-tenant-url"></a>Étape 1 : installer le module PowerShell AIPService et identifier l’URL de votre locataire

Installez le module **AIPService** pour vous permettre de configurer et de gérer le service qui fournit la protection des données pour Azure information protection.

Pour obtenir des instructions, consultez [installation du module PowerShell AIPService](./install-powershell.md).

Pour terminer certaines des instructions de migration, vous devez connaître l’URL du service Azure Rights Management pour votre locataire, afin que vous puissiez le remplacer lorsque vous voyez des références à *\<Your Tenant URL\>* . 

Votre URL de service Azure Rights Management a le format suivant : **{GUID}.rms.[Region].aadrm.com**. Par exemple : **5c6bb73b-1038-4EEC-863d-49bded473437.RMS.na.aadrm.com**

### <a name="to-identify-your-azure-rights-management-service-url"></a>Pour identifier l’URL du service Azure Rights Management

1. Connectez-vous au service Azure Rights Management et indiquez les informations d’identification de l’administrateur général de votre locataire quand vous y êtes invité :

    ```PowerShell
    Connect-AipService
    ```

2. Obtenez la configuration de votre locataire :

    ```PowerShell
    Get-AipServiceConfiguration
    ```

3. Copiez la valeur affichée pour **LicensingIntranetDistributionPointUrl** et, à partir de cette chaîne, supprimez `/_wmcs\licensing`.

    Ce qui reste est l’URL de votre service Azure Rights Management pour votre locataire Azure Information Protection. Cette valeur est souvent abrégée en *URL de votre locataire* dans les instructions de migration suivantes.

    Vous pouvez vérifier que vous avez la valeur correcte en exécutant la commande PowerShell suivante :

    ```PowerShell
    (Get-AipServiceConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]
    ```

## <a name="step-2-prepare-for-client-migration"></a>Étape 2. Préparer la migration des clients

Pour la plupart des migrations, comme il n’est pas pratique de migrer tous les clients à la fois, vous pouvez les migrer par lots. 

Cela signifie que, pendant une période donnée, certains clients utilisent Azure Information Protection et d’autres continuent à utiliser AD RMS. Pour prendre en charge les utilisateurs avant et après la migration, utilisez les contrôles d’intégration et déployez un script de prémigration. 

> [!NOTE]
> Cette étape est nécessaire pendant le processus de migration afin que les utilisateurs qui n’ont pas encore migré puissent consommer le contenu qui a été protégé par les utilisateurs migrés qui utilisent maintenant Azure Rights Management.
> 

**Pour préparer la migration des clients**

1. Créez un groupe nommé, par exemple, **AIPMigrated**. Ce groupe peut être créé dans Active Directory et synchronisé dans le Cloud, ou il peut être créé dans Microsoft 365 ou Azure Active Directory. 

    N’attribuez pas d’utilisateurs à ce groupe pour l’instant. Lors d’une prochaine étape, quand les utilisateurs auront migré, vous les ajouterez au groupe.

1. Prenez note de l’ID d’objet de ce groupe à l’aide de l’une des méthodes suivantes :

    - **Utilisez Azure AD PowerShell.** Par exemple, pour la version 1,0 du module, utilisez la commande [obtenir-msolgroup permet](/powershell/msonline/v1/Get-MsolGroup) . 
    - **Copiez l’ID d’objet** du groupe à partir de la portail Azure.

1. Configurez ce groupe pour les contrôles d’intégration afin d’autoriser uniquement les utilisateurs de ce groupe à employer Azure Rights Management pour protéger le contenu. 

    Pour ce faire, dans une session PowerShell, connectez-vous au service Azure Rights Management. Lorsque vous y êtes invité, spécifiez les informations d’identification de l’administrateur général :

    ```PowerShell
    Connect-AipService
    ```

    Configurez ce groupe pour les contrôles d’intégration, en remplaçant l’ID de votre objet de groupe par celui de cet exemple. Lorsque vous y êtes invité, entrez **Y** pour confirmer.

    ```PowerShell
    Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501" -Scope WindowsApp
    ```

1. Téléchargez le fichier [**Migration-Scripts.zip**](https://go.microsoft.com/fwlink/?LinkId=524619) .

1. Extrayez les fichiers et suivez les instructions de **Prepare-client. cmd**, afin qu’ils contiennent le nom du serveur correspondant à votre AD RMS URL de licence extranet du cluster. Pour localiser ce nom, procédez comme suit :

    1. dans la console AD RMS (Active Directory Rights Management Services), cliquez sur le nom du cluster. 

    1. À partir des informations dans **Détails du cluster**, copiez le nom du serveur issu de la valeur **Licensing** (Licences) dans la section relative aux URL de cluster extranet. Par exemple : **rmscluster.contoso.com**.

    > [!IMPORTANT]
    > Les instructions incluent le remplacement des exemples d’adresses **adrms.contoso.com** par les adresses de vos serveurs AD RMS. 
    >
    > Dans ce cas, veillez à ce qu’il n’y ait pas d’espace supplémentaire avant ou après vos adresses. Les espaces supplémentaires interrompent le script de migration et sont très difficiles à identifier comme la cause racine du problème. 
    >
    > Certains outils d’édition ajoutent automatiquement un espace après le collage du texte.
    >

5. Déployez ce script sur tous les ordinateurs Windows pour vous assurer que, quand vous commencez à migrer les clients, ceux qui ne le sont pas encore continuent de communiquer avec les services AD RMS même s’ils utilisent le contenu protégé par les clients migrés qui utilisent maintenant Azure Rights Management.

    Vous pouvez utiliser une stratégie de groupe ou un autre mécanisme de déploiement de logiciel pour déployer ce script.

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>Étape 3. Préparer le déploiement Exchange pour la migration

Si vous utilisez Exchange Online ou Exchange sur site, vous avez peut-être déjà intégré Exchange à votre déploiement AD RMS. Dans cette étape, vous allez les configurer pour utiliser la configuration AD RMS existante pour prendre en charge le contenu protégé par Azure RMS.

Vérifiez que vous disposez de [l’URL de service Azure Rights Management de votre locataire](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) pour pouvoir remplacer *&lt;URLdevotrelocataire&gt;* par cette valeur dans les commandes suivantes.

Effectuez l’une des opérations suivantes, selon que vous avez intégré Exchange sur site ou Exchange Online avec AD RMS :

- [Exchange sur site intégré avec AD RMS](#if-you-have-integrated-exchange-on-premises-with-ad-rms)
- [Exchange Online intégré avec AD RMS](#if-you-have-integrated-exchange-online-with-ad-rms)
### <a name="if-you-have-integrated-exchange-online-with-ad-rms"></a>Si vous avez intégré Exchange Online avec AD RMS

1. Ouvrez une session PowerShell Exchange Online.

1. Exécutez les commandes PowerShell suivantes une par une ou dans un script :

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 
    ```

### <a name="if-you-have-integrated-exchange-on-premises-with-ad-rms"></a>Si vous avez intégré Exchange sur site avec AD RMS

Pour chaque organisation Exchange, ajoutez les valeurs de Registre sur chaque serveur Exchange, puis exécutez les commandes PowerShell :

1. Si vous avez Exchange 2013 ou Exchange 2016, ajoutez la valeur de Registre suivante :

    - **Chemin du Registre :**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection`

    - **Tapez :** Reg_SZ

    - **Valeur :** `https://\<Your Tenant URL\>/_wmcs/licensing`

    - **Données :**`https://\<AD RMS Extranet Licensing URL\>/_wmcs/licensing`

1. Exécutez les commandes PowerShell suivantes, une par une, ou dans un script :

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset
    ```

Après avoir exécuté ces commandes pour Exchange Online ou Exchange sur site, si votre déploiement Exchange a été configuré pour prendre en charge le contenu qui a été protégé par AD RMS, il prend également en charge le contenu protégé par Azure RMS après la migration. 

Votre déploiement Exchange continue à utiliser les services AD RMS pour prendre en charge le contenu protégé jusqu’à une étape ultérieure de la migration.

## <a name="next-steps"></a>Étapes suivantes

Passez à la [Phase 2 : Configuration côté serveur](migrate-from-ad-rms-phase2.md).
