---
title: "Migrer un déploiement AD RMS vers Azure Information Protection - Phase 3"
description: "Phase 3 de la migration d’AD RMS vers Azure Information Protection, couvrant l’étape 7 de la migration d’AD RMS vers Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 35bd2d176cb71c54a489d4f4b8faca4d668a7867
ms.sourcegitcommit: c960f1d2140dea11e54cbeb37d53d1512621d90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>Phase de migration 3 : Configuration côté client

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*

Utilisez les informations suivantes pour la Phase 3 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent l’étape 7 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-clients-to-use-azure-information-protection"></a>Étape 7. Reconfigurer les clients pour utiliser Azure Information Protection

Pour des clients appareils mobiles et des ordinateurs Mac :

- Supprimez les enregistrements SRV DNS que vous avez créés lors du déploiement de l’ [extension d'appareil mobile AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

Pour des clients Windows :

- Utilisez les scripts de migration suivants pour reconfigurer les clients AD RMS. Ces scripts réinitialisent la configuration sur des ordinateurs Windows pour que ces derniers utilisent le service Azure Rights Management plutôt qu’AD RMS : 
    
    **CleanUpRMS.cmd**
    
    - Supprime le contenu de tous les dossiers et clés de Registre utilisés par le client AD RMS pour stocker sa configuration. Ces informations incluent l’emplacement du cluster AD RMS du client.
    
    **MigrateClient.cmd**
    
    - Configure le client pour initialiser l’environnement utilisateur (démarrage) du service Azure Rights Management.
    
    - Configure le client pour se connecter à votre service Azure Rights Management et obtenir des licences d’utilisation pour le contenu protégé par votre cluster AD RMS. 

Quand vous ne pouvez pas migrer tous vos clients Windows à la fois, exécutez les procédures suivantes pour des lots de clients. Pour chaque utilisateur disposant d’un ordinateur Windows que vous souhaitez migrer dans votre lot, ajoutez l’utilisateur au groupe **AIPMigrated** que vous avez créé précédemment.

### <a name="windows-client-reconfiguration-by-using-registry-edits"></a>Reconfiguration des clients Windows à l’aide des modifications du Registre

1. Revenez aux scripts de migration, **CleanUpRMS.cmd** et **MigrateClient.cmd**, que vous avez extraits précédemment.

2.  Suivez les instructions de **MigrateClient.cmd** pour modifier le script afin qu’il contienne l’URL du service Azure Rights Management de votre locataire ainsi que les noms des serveurs pour les URL de licences extranet et intranet du cluster AD RMS.

    > [!IMPORTANT]
    > Comme avant, veillez à ne pas introduire d’espaces supplémentaires avant ou après les adresses.
    > 
    > De plus, si vos serveurs AD RMS utilisent des certificats de serveur SSL/TLS, vérifiez si les valeurs des URL de licence incluent le numéro de port **443** dans la chaîne. Par exemple : https:// rms.treyresearch.net:443/_wmcs/licensing. Ces informations sont disponibles dans la console Active Directory Rights Management Services quand vous cliquez sur le nom du cluster et que vous consultez les informations **Détails du cluster**. Si vous voyez le numéro de port 443 dans l’URL, incluez cette valeur quand vous modifiez le script. Par exemple, https://rms.treyresearch.net**:443**. 

    Si vous devez récupérer l’URL du service Azure Rights Management pour *&lt;URLdevotrelocataire&gt;*, consultez [Pour identifier l’URL du service Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3.  Exécutez **CleanUpRMS.cmd**, puis **MigrateClient.cmd** sur les ordinateurs clients Windows qui sont utilisés par les membres du groupe **AIPMigrated**. Par exemple, créez un objet de stratégie de groupe qui exécute ces scripts et attribuez-le à ce groupe d’utilisateurs.

## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 4 : Configuration des services de prise en charge](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]