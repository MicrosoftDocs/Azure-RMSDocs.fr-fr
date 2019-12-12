---
title: Migrer un déploiement AD RMS vers Azure Information Protection - Phase 3
description: Phase 3 de la migration d’AD RMS vers Azure Information Protection, couvrant l’étape 7 de la migration d’AD RMS vers Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 12/06/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 613dcf3e6b35ed801fafc7718dbb0db8b664483c
ms.sourcegitcommit: 07b518c780f5e63eb5a72d7499ec7cfa40a95628
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2019
ms.locfileid: "74898916"
---
# <a name="migration-phase-3---client-side-configuration"></a>Phase de migration 3 : Configuration côté client

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations suivantes pour la Phase 3 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent l’étape 7 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Étape 7. Reconfigurer les ordinateurs Windows pour qu’ils utilisent Azure Information Protection

Pour les ordinateurs Windows qui utilisent des applications de bureau Office 365, Office 2019 ou Office 2016 « Démarrer en un clic » :

- Vous pouvez reconfigurer ces clients pour qu’ils utilisent Azure Information Protection à l’aide de la redirection DNS. Cette méthode est recommandée pour la migration des clients car elle est la plus simple. Toutefois, cette méthode est limitée aux applications de bureau Office 2016 « Démarrer en un clic » (ou ultérieur) pour les ordinateurs Windows.
    
    S vous utilisez cette méthode, vous devez créer un enregistrement SRV et définir une autorisation de refus NTFS pour les utilisateurs sur le point de terminaison de publication AD RMS.

- Pour les ordinateurs Windows qui n’utilisent pas Office 2019 ou Office 2016 « Démarrer en un clic » :
    
    Vous ne pouvez pas utiliser la redirection DNS. Vous devez utiliser des modifications du Registre à la place. Si vous avez une combinaison de versions d’Office qui peuvent et ne peuvent pas utiliser la redirection DNS, vous pouvez recourir à cette méthode unique pour tous les ordinateurs Windows ou combiner la redirection DNS et les modifications du Registre. 
    
    Pour changer plus facilement le Registre, vous pouvez modifier et déployer des scripts disponibles en téléchargement. 

Pour plus d’informations sur la reconfiguration des clients Windows, consultez les sections suivantes.

## <a name="client-reconfiguration-by-using-dns-redirection"></a>Reconfiguration des clients à l’aide de la redirection DNS

Cette méthode convient uniquement aux clients Windows qui exécutent des applications de bureau Office 365 et Office 2016 (ou version ultérieure) « Démarrer en un clic ». 

1. Créez un enregistrement DNS SRVS au format suivant :
    
    `_rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.`
    
    Remplacez *\<AD RMS cluster>* par le nom de domaine complet de votre cluster AD RMS. Par exemple, **rmscluster.contoso.com**.
    
    Si vous n’avez qu’un seul cluster AD RMS dans ce domaine, vous pouvez spécifier uniquement le nom de domaine du cluster AD RMS. Dans notre exemple, il s’agit de **contoso.com**. Quand vous spécifiez le nom de domaine dans cet enregistrement, la redirection s’applique à tous les clusters AD RMS de ce domaine.
    
    Le numéro de *\<port>* est ignoré.
    
    Remplacez *\<your tenant URL\>* par votre propre [URL du service Azure Rights Management pour votre locataire](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).
    
    Si vous utilisez le rôle de serveur DNS sur Windows Server, vous pouvez utiliser le tableau suivant en guise d’exemple pour spécifier les propriétés d’un enregistrement SRV dans la console Gestionnaire DNS.
    
    |Champ|Value|  
    |-----------|-----------|  
    |**Domaine**|_tcp.rmscluster.contoso.com|  
    |**Service**|_rmsredir|  
    |**Protocole**|_http|  
    |**Priorité**|0|  
    |**Poids**|0|  
    |**Numéro de port**|80|  
    |**Hôte offrant ce service**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  

2. Définissez une autorisation Refuser sur le point de terminaison de publication AD RMS pour les utilisateurs des applications Office 365 ou Office 2016 (ou version ultérieure) :

    a. Sur l’un de vos serveurs AD RMS dans le cluster, démarrez la console Gestionnaire des services Internet (IIS).

    b. Accédez à **site Web par défaut** et développez **_wmcs**.

    c. Cliquez avec le bouton droit sur **Gestionnaire de licences** et sélectionnez **basculer vers l’affichage du contenu**.

    d. Dans le volet d’informations, cliquez avec le bouton droit sur **License. asmx** > **Propriétés** > **modifier**

    e. Dans la boîte de dialogue **autorisations pour License. asmx** , sélectionnez **utilisateurs** si vous souhaitez définir la redirection pour tous les utilisateurs, ou cliquez sur **Ajouter** , puis spécifiez un groupe contenant les utilisateurs que vous souhaitez rediriger.
    
    Même si tous vos utilisateurs emploient une version d’Office qui prend en charge la redirection DNS, vous préférerez peut-être spécifier initialement un sous-ensemble d’utilisateurs pour une migration en plusieurs phases.
    
    f. Pour votre groupe sélectionné, sélectionnez **Refuser** pour les autorisations **Lecture et exécution** et **Lecture**, puis cliquez deux fois sur **OK**.

    g. Pour vérifier que cette configuration fonctionne comme prévu, essayez de vous connecter au fichier licensing.asmx directement à partir d’un navigateur. Le message d’erreur suivant doit s’afficher. Le client exécutant des applications Office 365, Office 2019 ou Office 2016 recherche alors l’enregistrement SRV :
    
    **Message d’erreur 401.3 : vous ne disposez pas des autorisations permettant d’afficher ce répertoire ou cette page à l’aide des informations d’identification que vous avez fournies (accès refusé en raison des listes de contrôle d’accès).**


## <a name="client-reconfiguration-by-using-registry-edits"></a>Reconfiguration du client à l’aide des modifications du Registre

Cette méthode convient à tous les clients Windows. Vous devez l’utiliser si les clients n’exécutent pas des applications Office 365, Office 2019 ou Office 2016, mais une version antérieure d’Office. Cette méthode utilise deux scripts de migration pour reconfigurer les clients AD RMS :

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

### <a name="modifying-the-scripts-for-registry-edits"></a>Modification des scripts pour les modifications du Registre

1. Retournez aux scripts de migration **Migrate-Client.cmd** et **Migrate-User.cmd** que vous avez extraits après les avoir téléchargés au cours de la [phase de préparation](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2. Suivez les instructions de **Migrate-Client.cmd** pour modifier le script afin qu’il contienne l’URL du service Azure Rights Management de votre locataire ainsi que les noms des serveurs pour les URL de licences extranet et intranet du cluster AD RMS. Ensuite, incrémentez la version du script comme expliqué précédemment. Une bonne pratique pour le suivi des versions de script consite à utiliser la date d’aujourd’hui au format suivant : AAAAMMJJ.
    
   > [!IMPORTANT]
   > Comme avant, veillez à ne pas introduire d’espaces supplémentaires avant ou après les adresses.
   > 
   > De plus, si vos serveurs AD RMS utilisent des certificats de serveur SSL/TLS, vérifiez si les valeurs des URL de licence incluent le numéro de port **443** dans la chaîne. Par exemple : https://rms.treyresearch.net:443/_wmcs/licensing. Ces informations sont disponibles dans la console Active Directory Rights Management Services quand vous cliquez sur le nom du cluster et que vous consultez les informations **Détails du cluster**. Si vous voyez le numéro de port 443 dans l’URL, incluez cette valeur quand vous modifiez le script. Par exemple : https://rms.treyresearch.net:<strong>443</strong>. 
    
   Si vous devez récupérer l’URL du service Azure Rights Management pour *&lt;URLdevotrelocataire&gt;*, consultez [Pour identifier l’URL du service Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. À l’aide des instructions fournies au début de cette étape, configurez les méthodes de déploiement de votre script pour exécuter **Migrate-Client.cmd** et **Migrate-User.cmd** sur les ordinateurs clients Windows utilisés par les membres du groupe AIPMigrated. 

## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 4 : Configuration des services de prise en charge](migrate-from-ad-rms-phase4.md).
