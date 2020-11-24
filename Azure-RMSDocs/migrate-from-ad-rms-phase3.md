---
title: Migrer un déploiement AD RMS vers Azure Information Protection - Phase 3
description: Phase 3 de la migration d’AD RMS vers Azure Information Protection, couvrant l’étape 7 de la migration d’AD RMS vers Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b58710ebd4486319126bc2f33266d349d23fa888
ms.sourcegitcommit: 2085eedf24a6f72cbafcbacad023122a04faccc9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2020
ms.locfileid: "95568451"
---
# <a name="migration-phase-3---client-side-configuration"></a>Phase de migration 3 : Configuration côté client

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations suivantes pour la Phase 3 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent l’étape 7 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Étape 7. Reconfigurer les ordinateurs Windows pour qu’ils utilisent Azure Information Protection

Reconfigurez vos ordinateurs Windows pour utiliser Azure Information Protection à l’aide de l’une des méthodes suivantes :

- **Redirection DNS**. Méthode la plus simple et la plus préférée, lorsqu’elles sont prises en charge. 

    Pris en charge pour les ordinateurs Windows qui utilisent Office 2016 ou des applications de bureau « démarrer en un clic », notamment :

    - Applications Microsoft 365
    - Office 2019
    - Office 2016 Cliquer pour exécuter des applications de bureau

    Vous oblige à créer un nouvel enregistrement SRV et à définir une autorisation de refus NTFS pour les utilisateurs sur le point de terminaison de publication AD RMS.

    Pour plus d’informations, consultez [reconfiguration du client à l’aide de la redirection DNS](#client-reconfiguration-by-using-dns-redirection).

- **Modifications du Registre**. Concerne tous les environnements pris en charge, y compris :

    - Ordinateurs Windows qui utilisent Office 2016 ou des applications de bureau « démarrer en un clic », comme indiqué ci-dessus
    - Ordinateurs Windows qui utilisent d’autres applications
    
    Apportez les modifications de Registre nécessaires manuellement, ou modifiez et déployez des scripts téléchargeables pour apporter des modifications au registre.

    Pour plus d’informations, consultez [reconfiguration du client à l’aide des modifications du Registre](#client-reconfiguration-by-using-registry-edits).


> [!TIP]
> Si vous avez un mélange de versions d’Office qui peuvent et ne peuvent pas utiliser la redirection DNS, vous pouvez utiliser une combinaison de redirection DNS et de modification du Registre, ou modifier le registre comme une méthode unique pour tous les ordinateurs Windows.


## <a name="client-reconfiguration-by-using-dns-redirection"></a>Reconfiguration des clients à l’aide de la redirection DNS

Cette méthode convient uniquement pour les clients Windows qui exécutent des applications Microsoft 365 et Office 2016 (ou version ultérieure) des applications de bureau « démarrer en un clic ». 

1. Créez un enregistrement DNS SRVS au format suivant :
    
    ```sh
    _rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.
    ```
    
    Pour *\<AD RMS cluster>* , spécifiez le nom de domaine complet de votre cluster AD RMS. Par exemple, **rmscluster.contoso.com**.
    
    Si vous n’avez qu’un seul cluster AD RMS dans ce domaine, vous pouvez spécifier uniquement le nom de domaine du cluster AD RMS. Dans notre exemple, il s’agit de **contoso.com**. Quand vous spécifiez le nom de domaine dans cet enregistrement, la redirection s’applique à tous les clusters AD RMS de ce domaine.
    
    Le *\<port>* nombre est ignoré.
    
    Pour *\<your tenant URL\>* , spécifiez votre propre [URL du service Azure Rights Management pour votre locataire](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).
    
    Si vous utilisez le rôle de serveur DNS sur Windows Server, vous pouvez utiliser le tableau suivant en guise d’exemple pour spécifier les propriétés d’un enregistrement SRV dans la console Gestionnaire DNS.
    
    |Champ|Valeur|  
    |-----------|-----------|  
    |**Domaine**|_tcp.rmscluster.contoso.com|  
    |**Service**|_rmsredir|  
    |**Protocole**|_http|  
    |**Priorité**|0|  
    |**Poids**|0|  
    |**Numéro de port**|80|  
    |**Hôte offrant ce service**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  

2. Définissez une autorisation Deny sur le point de terminaison de publication AD RMS pour les utilisateurs exécutant Microsoft 365 Apps ou Office 2016 (ou version ultérieure) :

    a. Sur l’un de vos serveurs AD RMS dans le cluster, démarrez la console Gestionnaire des services Internet (IIS).

    b. Accédez à **site Web par défaut** et développez **_wmcs**.

    c. Cliquez avec le bouton droit sur **Gestionnaire de licences** et sélectionnez **basculer vers l’affichage du contenu**.

    d. Dans le volet d’informations, cliquez avec le bouton droit sur **License. asmx**  >  **Propriétés**  >  **modifier**

    e. Dans la boîte de dialogue **autorisations pour License. asmx** , sélectionnez **utilisateurs** si vous souhaitez définir la redirection pour tous les utilisateurs, ou cliquez sur **Ajouter** , puis spécifiez un groupe contenant les utilisateurs que vous souhaitez rediriger.
    
    Même si tous vos utilisateurs emploient une version d’Office qui prend en charge la redirection DNS, vous préférerez peut-être spécifier initialement un sous-ensemble d’utilisateurs pour une migration en plusieurs phases.
    
    f. Pour votre groupe sélectionné, sélectionnez **Refuser** pour les autorisations **Lecture et exécution** et **Lecture**, puis cliquez deux fois sur **OK**.

    g. Pour vérifier que cette configuration fonctionne comme prévu, essayez de vous connecter au fichier licensing.asmx directement à partir d’un navigateur. Vous devez voir le message d’erreur suivant, qui déclenche le client exécutant Microsoft 365 Apps ou Office 2019 ou Office 2016 pour Rechercher l’enregistrement SRV :
    
    **Message d’erreur 401.3 : vous ne disposez pas des autorisations permettant d’afficher ce répertoire ou cette page à l’aide des informations d’identification que vous avez fournies (accès refusé en raison des listes de contrôle d’accès).**


## <a name="client-reconfiguration-by-using-registry-edits"></a>Reconfiguration du client à l’aide des modifications du Registre

Cette méthode convient à tous les clients Windows et doit être utilisée s’ils n’exécutent pas Microsoft 365 applications, ou Office 2016 (ou version ultérieure). Cette méthode utilise deux scripts de migration pour reconfigurer les clients AD RMS :

- Migrate-Client.cmd

- Migrate-User.cmd

Le script de configuration du client (Migrate-Client.cmd) configure les paramètres au niveau de l’ordinateur dans le Registre, ce qui signifie qu’il doit s’exécuter dans un contexte de sécurité pouvant effectuer ces changements. Cela signifie généralement l’une des méthodes suivantes :

- Utiliser la stratégie de groupe pour exécuter le script comme script de démarrage de l’ordinateur

- Utiliser l’installation des logiciels de la stratégie de groupe pour affecter le script à l’ordinateur

- Utiliser une solution de déploiement de logiciels pour déployer le script sur les ordinateurs Par exemple, utilisez [les packages et les programmes](/sccm/apps/deploy-use/packages-and-programs) System Center Configuration Manager. Dans les propriétés du package et du programme, sous **Mode d’exécution**, indiquez que le script s’exécute avec des autorisations administratives sur l’appareil. 

- Utilisez un script d’ouverture de session si l’utilisateur dispose de privilèges d’administrateur local.

Le script de configuration utilisateur (Migrate-User.cmd) configure les paramètres au niveau de l’utilisateur et nettoie le magasin de licences de client. Cela signifie que ce script doit s’exécuter dans le contexte de l’utilisateur réel. Par exemple :

- Utilisez un script d’ouverture de session.

- Utilisez l’installation des logiciels de la stratégie de groupe pour publier le script à exécuter par l’utilisateur.

- Utilisez une solution de déploiement de logiciels pour déployer le script sur les utilisateurs. Par exemple, utilisez [les packages et les programmes](/sccm/apps/deploy-use/packages-and-programs) System Center Configuration Manager. Dans les propriétés du package et du programme, sous **Mode d’exécution**, indiquez que le script s’exécute avec les autorisations de l’utilisateur. 

- Demandez à l’utilisateur d’exécuter le script quand il est connecté à son ordinateur.

Les deux scripts incluent un numéro de version et ne sont pas réexécutés tant que ce numéro de version n’est pas changé. Cela signifie que vous pouvez laisser les scripts en place jusqu’à ce que la migration soit terminée. Toutefois, si vous changez les scripts que les ordinateurs et les utilisateurs doivent réexécuter sur leurs ordinateurs Windows, modifiez la ligne suivante dans les deux scripts avec une valeur plus élevée :

```sh
SET Version=20170427
```

Le script de configuration de l’utilisateur, conçu pour s’exécuter après le script de configuration du client, utilise le numéro de version dans cette vérification. Il s’arrête si le script de configuration du client avec la même version n’a pas été exécuté. Cette vérification garantit que les deux scripts sont exécutés dans la bonne séquence. 

Quand vous ne pouvez pas migrer tous vos clients Windows à la fois, exécutez les procédures suivantes pour des lots de clients. Pour chaque utilisateur disposant d’un ordinateur Windows que vous souhaitez migrer dans votre lot, ajoutez l’utilisateur au groupe **AIPMigrated** que vous avez créé précédemment.

### <a name="modifying-the-scripts-for-registry-edits"></a>Modification des scripts pour les modifications du Registre

1. Retournez aux scripts de migration **Migrate-Client.cmd** et **Migrate-User.cmd** que vous avez extraits après les avoir téléchargés au cours de la [phase de préparation](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2. Suivez les instructions de **Migrate-client. cmd** pour modifier le script afin qu’il contienne l’URL du service Azure Rights Management de votre locataire, ainsi que les noms de vos serveurs pour votre URL de licence extranet de cluster AD RMS et l’URL de licence intranet. Ensuite, incrémentez la version du script comme expliqué précédemment. Une bonne pratique pour le suivi des versions de script consiste à utiliser la date du jour au format suivant : AAAAMMJJ
    
   > [!IMPORTANT]
   > Comme avant, veillez à ne pas introduire d’espaces supplémentaires avant ou après les adresses.
   > 
   > De plus, si vos serveurs AD RMS utilisent des certificats de serveur SSL/TLS, vérifiez si les valeurs des URL de licence incluent le numéro de port **443** dans la chaîne. Par exemple : https://rms.treyresearch.net:443/_wmcs/licensing. Ces informations sont disponibles dans la console Active Directory Rights Management Services quand vous cliquez sur le nom du cluster et que vous consultez les informations **Détails du cluster**. Si vous voyez le numéro de port 443 dans l’URL, incluez cette valeur quand vous modifiez le script. Par exemple : https://rms.treyresearch.net:<strong>443</strong>. 
    
   Si vous devez récupérer l’URL de votre service Azure Rights Management pour *&lt; YourTenantURL &gt;*, reportez-vous à [pour identifier votre URL Azure Rights Management Service](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. À l’aide des instructions fournies au début de cette étape, configurez les méthodes de déploiement de votre script pour exécuter **Migrate-Client.cmd** et **Migrate-User.cmd** sur les ordinateurs clients Windows utilisés par les membres du groupe AIPMigrated. 

## <a name="next-steps"></a>Étapes suivantes

Pour poursuivre la migration, passez à la [Phase 4 : Configuration des services de prise en charge](migrate-from-ad-rms-phase4.md).
