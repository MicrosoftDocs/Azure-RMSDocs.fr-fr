---
title: "Migrer un déploiement AD RMS vers Azure Information Protection - Phase 3"
description: "Phase 3 de la migration d’AD RMS vers Azure Information Protection, couvrant l’étape 7 de la migration d’AD RMS vers Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5de30d095e1c279babb8f8be74a5a9b9d54db204
ms.sourcegitcommit: 45c23b3b353ad0e438292cb1cd8d1b13061620e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>Phase de migration 3 : Configuration côté client

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*

Utilisez les informations suivantes pour la Phase 3 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent l’étape 7 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Étape 7. Reconfigurer les ordinateurs Windows pour qu’ils utilisent Azure Information Protection

Pour les ordinateurs Windows, utilisez deux scripts de migration pour reconfigurer les clients AD RMS :

- Migrate-Client.cmd

- Migrate-User.cmd

Le script de configuration du client (Migrate-Client.cmd) configure les paramètres au niveau de l’ordinateur dans le Registre, ce qui signifie qu’il doit s’exécuter dans un contexte de sécurité pouvant effectuer ces changements. Cela signifie généralement l’une des méthodes suivantes :

- Utiliser la stratégie de groupe pour exécuter le script comme script de démarrage de l’ordinateur

- Utiliser l’installation des logiciels de la stratégie de groupe pour affecter le script à l’ordinateur

- Utiliser une solution de déploiement de logiciels pour déployer le script sur les ordinateurs Par exemple, utilisez [les packages et les programmes](/sccm/apps/deploy-use/packages-and-programs) System Center Configuration Manager. Dans les propriétés du package et du programme, sous **Mode d’exécution**, indiquez que le script s’exécute avec des autorisations administratives sur l’appareil. 

- Utilisez un script d’ouverture de session si l’utilisateur dispose de privilèges d’administrateur local.

Le script de configuration utilisateur (Migrate-User.cmd) configure les paramètres au niveau de l’utilisateur et nettoie le magasin de licences de client. Cela signifie que ce script doit s’exécuter dans le contexte de l’utilisateur réel. Exemple :

- Utilisez un script d’ouverture de session.

- Utilisez l’installation des logiciels de la stratégie de groupe pour publier le script à exécuter par l’utilisateur.

- Utilisez une solution de déploiement de logiciels pour déployer le script sur les utilisateurs. Par exemple, utilisez [les packages et les programmes](/sccm/apps/deploy-use/packages-and-programs) System Center Configuration Manager. Dans les propriétés du package et du programme, sous **Mode d’exécution**, indiquez que le script s’exécute avec les autorisations de l’utilisateur. 

- Demandez à l’utilisateur d’exécuter le script quand il est connecté à son ordinateur.

Les deux scripts incluent un numéro de version et ne sont pas réexécutés tant que ce numéro de version n’est pas changé. Cela signifie que vous pouvez laisser les scripts en place jusqu’à ce que la migration soit terminée. Toutefois, si vous changez les scripts que les ordinateurs et les utilisateurs doivent réexécuter sur leurs ordinateurs Windows, modifiez la ligne suivante dans les deux scripts avec une valeur plus élevée :

    SET Version=20170427

Le script de configuration de l’utilisateur, conçu pour s’exécuter après le script de configuration du client, utilise le numéro de version dans cette vérification. Il s’arrête si le script de configuration du client avec la même version n’a pas été exécuté. Cette vérification garantit que les deux scripts sont exécutés dans la bonne séquence. 

Quand vous ne pouvez pas migrer tous vos clients Windows à la fois, exécutez les procédures suivantes pour des lots de clients. Pour chaque utilisateur disposant d’un ordinateur Windows que vous souhaitez migrer dans votre lot, ajoutez l’utilisateur au groupe **AIPMigrated** que vous avez créé précédemment.

### <a name="windows-client-reconfiguration-by-using-registry-edits"></a>Reconfiguration des clients Windows à l’aide des modifications du Registre

1. Retournez aux scripts de migration **Migrate-Client.cmd** et **Migrate-User.cmd**  que vous avez extraits après les avoir téléchargés au cours de la [phase de préparation](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2.  Suivez les instructions de **Migrate-Client.cmd** pour modifier le script afin qu’il contienne l’URL du service Azure Rights Management de votre locataire ainsi que les noms des serveurs pour les URL de licences extranet et intranet du cluster AD RMS. Ensuite, incrémentez la version du script comme expliqué précédemment. Une bonne pratique pour le suivi des versions de script consite à utiliser la date d’aujourd’hui au format suivant : AAAAMMJJ.

    > [!IMPORTANT]
    > Comme avant, veillez à ne pas introduire d’espaces supplémentaires avant ou après les adresses.
    > 
    > De plus, si vos serveurs AD RMS utilisent des certificats de serveur SSL/TLS, vérifiez si les valeurs des URL de licence incluent le numéro de port **443** dans la chaîne. Par exemple : https:// rms.treyresearch.net:443/_wmcs/licensing. Ces informations sont disponibles dans la console Active Directory Rights Management Services quand vous cliquez sur le nom du cluster et que vous consultez les informations **Détails du cluster**. Si vous voyez le numéro de port 443 dans l’URL, incluez cette valeur quand vous modifiez le script. Par exemple, https://rms.treyresearch.net**:443**. 

    Si vous devez récupérer l’URL du service Azure Rights Management pour *&lt;URLdevotrelocataire&gt;*, consultez [Pour identifier l’URL du service Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. À l’aide des instructions fournies au début de cette étape, configurez les méthodes de déploiement de votre script pour exécuter **Migrate-Client.cmd** et **Migrate-User.cmd** sur les ordinateurs clients Windows utilisés par les membres du groupe AIPMigrated. 

## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 4 : Configuration des services de prise en charge](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]