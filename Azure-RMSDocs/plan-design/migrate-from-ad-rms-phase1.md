---
title: "Migrer un déploiement AD RMS vers Azure Information Protection - Phase 1"
description: "Phase 1 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 1 à 3 de la migration d’AD RMS vers Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c74bbf88adced03ba73c2431c4c3ccd2ea3359d1
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2018
---
# <a name="migration-phase-1---preparation"></a>Phase de migration 1 : Préparation

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*

Utilisez les informations suivantes pour la Phase 1 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 1 à 3 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) et préparent votre environnement pour la migration sans aucun impact sur vos utilisateurs.


## <a name="step-1-install-the-aadrm-powershell-module-and-identify-your-tenant-url"></a>Étape 1 : Installer le module PowerShell AADRM et identifier l’URL de votre locataire

Installez le module AADRM afin de pouvoir configurer et gérer le service qui assure la protection des données pour Azure Information Protection.

Pour connaître les instructions d'installation, voir [Installation du module PowerShell AADRM](../deploy-use/install-powershell.md).

> [!NOTE]
> Si vous avez déjà téléchargé ce module Windows PowerShell, exécutez la commande suivante pour vérifier que le numéro de votre version est au minimum **2.9.0.0** : `(Get-Module aadrm -ListAvailable).Version`

Pour suivre certaines des instructions de migration, vous devez connaître l’URL de service Azure Rights Management de votre locataire pour pouvoir la fournir quand vous voyez des références à *\<URL de votre locataire\>*. Votre URL de service Azure Rights Management a le format suivant : **{GUID}.rms.[Region].aadrm.com**.

Par exemple : **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

### <a name="to-identify-your-azure-rights-management-service-url"></a>Pour identifier l’URL du service Azure Rights Management

1. Connectez-vous au service Azure Rights Management et indiquez les informations d’identification de l’administrateur général de votre locataire quand vous y êtes invité :
    
        Connect-AadrmService
    
2. Obtenez la configuration de votre locataire :
    
        Get-AadrmConfiguration
    
3. Copiez la valeur affichée pour **LicensingIntranetDistributionPointUrl** et, à partir de cette chaîne, supprimez `/_wmcs\licensing`. 
    
    Ce qui reste est l’URL de votre service Azure Rights Management pour votre locataire Azure Information Protection. Cette valeur est souvent abrégée en *URL de votre locataire* dans les instructions de migration suivantes.
    
    Vous pouvez vérifier que vous avez la valeur correcte en exécutant la commande PowerShell suivante :
    
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

## <a name="step-2-prepare-for-client-migration"></a>Étape 2. Préparer la migration des clients

Pour la plupart des migrations, comme il n’est pas pratique de migrer tous les clients à la fois, vous pouvez les migrer par lots. Cela signifie que, pendant une période donnée, certains clients utilisent Azure Information Protection et d’autres continuent à utiliser AD RMS. Pour prendre en charge les utilisateurs avant et après la migration, utilisez les contrôles d’intégration et déployez un script de prémigration. Cette étape est nécessaire pendant le processus de migration afin que les utilisateurs qui n’ont pas encore migré puissent consommer le contenu qui a été protégé par les utilisateurs migrés qui utilisent maintenant Azure Rights Management.

1. Créez un groupe nommé, par exemple, **AIPMigrated**. Vous pouvez créer ce groupe dans Active Directory et le synchroniser dans le cloud, ou dans Office 365 ou Azure Active Directory. N’attribuez pas d’utilisateurs à ce groupe pour l’instant. Lors d’une prochaine étape, quand les utilisateurs auront migré, vous les ajouterez au groupe.

    Notez l’ID d’objet de ce groupe. Pour ce faire, vous pouvez utiliser Azure AD PowerShell. Par exemple, pour la version 1.0 du module, utilisez la commande [Get-MsolGroup](/powershell/msonline/v1/Get-MsolGroup). Vous pouvez aussi copier l’ID d’objet du groupe à partir du portail Azure.

2. Configurez ce groupe pour les contrôles d’intégration afin d’autoriser uniquement les utilisateurs de ce groupe à employer Azure Rights Management pour protéger le contenu. Pour ce faire, dans une session PowerShell, connectez-vous au service Azure Rights Management et indiquez vos informations d’identification d’administrateur général quand vous y êtes invité :

        Connect-Aadrmservice

    Configurez ensuite ce groupe pour les contrôles d’intégration en remplaçant l’ID d’objet de groupe dans cet exemple par le vôtre, puis entrez **O** pour confirmer quand vous y êtes invité :

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501" -Scope WindowsApp

3. [Téléchargez le fichier suivant](https://go.microsoft.com/fwlink/?LinkId=524619) qui contient les scripts de migration de clients :
    
    **Migration-Scripts.zip**
    
4. Extrayez les fichiers et suivez les instructions de **Prepare-Client.cmd** pour ajouter le nom du serveur pour votre URL de licence extranet du cluster AD RMS. 
    
    Pour trouver ce nom : dans la console Active Directory Rights Management Services, cliquez sur le nom du cluster. À partir des informations dans **Détails du cluster**, copiez le nom du serveur issu de la valeur **Licensing** (Licences) dans la section relative aux URL de cluster extranet. Par exemple : **rmscluster.contoso.com**.

    > [!IMPORTANT]
    > Les instructions incluent le remplacement des exemples d’adresses **adrms.contoso.com** par les adresses de vos serveurs AD RMS. Quand vous effectuez cette opération, vérifiez qu’il n’y a pas d’espaces supplémentaires avant ou après vos adresses ; ces derniers engendreraient une interruption du script de migration et il serait très difficile de les identifier comme étant à l’origine du problème. Certains outils d’édition ajoutent automatiquement un espace après le collage du texte.
    >

5. Déployez ce script sur tous les ordinateurs Windows pour vous assurer que, quand vous commencez à migrer les clients, ceux qui ne le sont pas encore continuent de communiquer avec les services AD RMS même s’ils utilisent le contenu protégé par les clients migrés qui utilisent maintenant Azure Rights Management.

    Vous pouvez utiliser une stratégie de groupe ou un autre mécanisme de déploiement de logiciel pour déployer ce script.

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>Étape 3. Préparer le déploiement Exchange pour la migration

Si vous utilisez Exchange Online ou Exchange sur site, vous avez peut-être déjà intégré Exchange à votre déploiement AD RMS. Dans cette étape, vous allez les configurer pour utiliser la configuration AD RMS existante pour prendre en charge le contenu protégé par Azure RMS. 

Vérifiez que vous disposez de [l’URL de service Azure Rights Management de votre locataire](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) pour pouvoir remplacer *&lt;URLdevotrelocataire&gt;* par cette valeur dans les commandes suivantes. 

**Si vous avez intégré Exchange Online à AD RMS** : ouvrez une session Exchange Online PowerShell et exécutez les commandes PowerShell suivantes une par une ou dans un script :

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 

**Si vous avez intégré Exchange sur site à AD RMS** : pour chaque organisation Exchange, ajoutez tout d’abord les valeurs de Registre sur chaque serveur Exchange, puis exécutez les commandes PowerShell : 

Valeurs de Registre pour Exchange 2013 et Exchange 2016 :

**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://\<URL de votre locataire\>/_wmcs/licensing

**Données :** https://\<URL de licence extranet AD RMS\>/_wmcs/licensing

---

Valeurs de Registre pour Exchange 2010 :

**Chemin du Registre :**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Type :** Reg_SZ

**Valeur :** https://\<URL de votre locataire\>/_wmcs/licensing

**Données :** https://\<URL de licence extranet AD RMS>/_wmcs/licensing

---

Commandes PowerShell à exécuter l’une après l’autre, ou dans un script

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset


Après avoir exécuté ces commandes pour Exchange Online ou Exchange sur site, si votre déploiement Exchange a été configuré pour prendre en charge le contenu qui a été protégé par AD RMS, il prend également en charge le contenu protégé par Azure RMS après la migration. Votre déploiement Exchange continue à utiliser les services AD RMS pour prendre en charge le contenu protégé jusqu’à une étape ultérieure de la migration.


## <a name="next-steps"></a>Étapes suivantes
Passez à la [Phase 2 : Configuration côté serveur](migrate-from-ad-rms-phase2.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
