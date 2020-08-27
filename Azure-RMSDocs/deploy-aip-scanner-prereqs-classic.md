---
title: Prérequis du scanneur classique Azure Information Protection (AIP)
description: Répertorie les conditions préalables à l’installation et au déploiement du Azure Information Protection scanneur classique.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 446369f3a46e99d138455afbb0cc90d9a8635fb2
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88952927"
---
# <a name="prerequisites-for-installing-and-deploying-the-azure-information-protection-classic-scanner"></a>Conditions préalables à l’installation et au déploiement du scanneur Azure Information Protection Classic

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows server 2012 R2*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle. 
> 
> Si vous utilisez le scanneur d’étiquetage unifié, consultez [Configuration requise pour l’installation et le déploiement du scanneur d’étiquetage unifié Azure information protection](deploy-aip-scanner-prereqs.md).

Avant d’installer le scanneur Azure Information Protection, assurez-vous que votre système est conforme aux exigences suivantes :

- [Configuration requise pour Windows Server](#windows-server-requirements)
- [Exigences relatives au compte de service](#service-account-requirements)
- [Configuration requise pour SQL Server](#sql-server-requirements)
- [Configuration requise pour le client Azure Information Protection](#azure-information-protection-client-requirements)
- [Configuration requise pour l’étiquette](#label-configuration-requirements)
- [Configuration requise pour SharePoint](#sharepoint-requirements)
- [Configuration requise pour la Microsoft Office](#microsoft-office-requirements)
- [Exigences relatives au chemin de fichier](#file-path-requirements)
- [Exigences relatives aux statistiques d’utilisation](#usage-statistics-requirements)

Si vous ne pouvez pas satisfaire à toutes les exigences du tableau parce qu’elles sont interdites par les stratégies de votre organisation, consultez la section [autres configurations](#deploying-the-scanner-with-alternative-configurations) .

Lors du déploiement du scanneur en production ou du test des performances de plusieurs scanneurs, consultez [exigences de stockage et planification de la capacité pour SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

Lorsque vous êtes prêt à commencer l’installation et le déploiement de votre scanneur, poursuivez [le déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner-configure-install-classic.md).

## <a name="windows-server-requirements"></a>Configuration requise pour Windows Server

Vous devez disposer d’un ordinateur Windows Server pour exécuter le scanneur, qui présente les spécifications système suivantes :

|Caractéristique  |Détails  |
|---------|---------|
|**Processeur**     |4 processeurs principaux         |
|**RAM**     |8 Go         |
|**Espace disque**     |10 Go d’espace libre (moyenne) pour les fichiers temporaires. </br></br>Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. </br></br>L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo. 
|**Système d’exploitation**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**Remarque :** À des fins de test ou d’évaluation dans un environnement hors production, vous pouvez également utiliser n’importe quel système d’exploitation Windows [pris en charge par le client Azure information protection](requirements.md#client-devices).
|**Connectivité réseau**     | Votre ordinateur de scanneur peut être un ordinateur physique ou virtuel avec une connexion réseau rapide et fiable aux magasins de données à analyser. </br></br> Si la connexion Internet n’est pas possible en raison des stratégies de votre organisation, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations). </br></br>Dans le cas contraire, assurez-vous que cet ordinateur dispose d’une connectivité Internet qui autorise les URL suivantes sur HTTPs (port 443) :</br><br />-  \*. aadrm.com <br />-  \*. azurerms.com<br />-  \*. informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*. aria.microsoft.com|
| ||

## <a name="service-account-requirements"></a>Configuration requise pour les comptes de service

Vous devez disposer d’un compte de service pour exécuter le service du scanneur sur l’ordinateur Windows Server, ainsi que pour vous authentifier auprès de Azure AD et télécharger la stratégie Azure Information Protection.

Votre compte de service doit être un compte Active Directory et être synchronisé avec Azure AD.

Si vous ne pouvez pas synchroniser ce compte en raison des stratégies de votre organisation, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).

Ce compte de service a la configuration suivante :

|Condition requise  |Détails  |
|---------|---------|
|Attribution **de droits d’utilisateur d’ouverture de session locale**     |Requis pour installer et configurer le scanneur, mais pas pour exécuter des analyses.  </br></br>Une fois que vous avez confirmé que le scanneur peut détecter, classer et protéger les fichiers, vous pouvez supprimer ce droit du compte de service.  </br></br>S’il n’est pas possible d’accorder ce droit même pendant une brève période de temps en raison des stratégies de votre organisation, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).         |
|**Ouvrir une session en tant que service**, attribution des droits utilisateur.     |  Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur.        |
|**Autorisations pour les référentiels de données**     |- **Partages de fichiers ou fichiers locaux :** Accordez des autorisations de **lecture**, d' **écriture**et de **modification** pour analyser les fichiers, puis appliquez la classification et la protection conformément à la configuration.  <br /><br />- **SharePoint :** Accordez des autorisations **contrôle total** pour analyser les fichiers, puis appliquez la classification et la protection conformément à la configuration.  <br /><br />- **Mode de découverte :** Pour exécuter le scanneur en mode détection uniquement, l’autorisation **lecture** est suffisante.         |
|**Pour les étiquettes qui reprotègent ou suppriment la protection**     | Pour vous assurer que le scanneur a toujours accès aux fichiers protégés, définissez ce compte comme [super utilisateur](configure-super-users.md) pour Azure information protection et assurez-vous que la fonctionnalité de super utilisateur est activée. </br></br>En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que le compte de service est inclus dans les contrôles d’intégration que vous avez configurés.|
| ||

## <a name="sql-server-requirements"></a>Configuration requise pour SQL Server

Pour stocker les données de configuration de l’analyseur, utilisez un serveur SQL Server avec les spécifications suivantes :

- **Instance locale ou distante.**

    Nous vous recommandons d’héberger les SQL Server et le service du scanneur sur des ordinateurs différents, sauf si vous travaillez avec un petit déploiement. 

    SQL Server 2012 est la version minimale pour les éditions suivantes :

    - SQL Server Entreprise
    - SQL Server Standard
    - SQL Server Express (recommandé pour les environnements de test uniquement)

- **Un compte avec le rôle sysadmin pour installer le scanneur.**

    Cela permet au processus d’installation de créer automatiquement la base de données de configuration de l’analyseur et d’accorder le rôle de **db_owner** requis au compte de service qui exécute le scanneur. 

    Si vous ne pouvez pas accorder le rôle sysadmin ou si les stratégies de votre organisation nécessitent la création et la configuration de bases de données manuellement, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).

- **Capacité.** Pour obtenir des conseils sur la capacité, consultez [exigences de stockage et planification de la capacité pour SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

- **[Classement non sensible à la casse](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15)**

> [!NOTE]
> Plusieurs bases de données de configuration sur le même serveur SQL Server sont prises en charge lorsque vous spécifiez un nom de cluster personnalisé (profil) pour le scanneur.
> 

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Exigences de stockage et planification de la capacité pour SQL Server

La quantité d’espace disque requise pour la base de données de configuration du scanneur et la spécification de l’ordinateur qui exécute SQL Server peuvent varier pour chaque environnement, nous vous encourageons donc à effectuer vos propres tests. Utilisez les instructions suivantes comme point de départ.

Pour plus d’informations, consultez [optimisation des performances du scanneur](deploy-aip-scanner-configure-install-classic.md#optimizing-scanner-performance).

La taille du disque de la base de données de configuration varie pour chaque déploiement. Nous vous recommandons d’allouer 500 Mo pour chaque 1 million fichiers que vous souhaitez analyser. 

Pour chaque scanneur, utilisez :

- 4 processeurs principaux
- 8 Go de RAM (4 Go minimum)

## <a name="azure-information-protection-client-requirements"></a>Configuration requise pour le client Azure Information Protection

Le client de Azure Information Protection doit être installé sur l’ordinateur Windows Server.

Pour plus d’informations, consultez le [Guide d’administration du client classique](./rms-client/client-admin-guide.md).

> [!IMPORTANT]
> Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.
> 

## <a name="label-configuration-requirements"></a>Configuration requise pour l’étiquette

Vous devez configurer des étiquettes qui appliquent automatiquement la classification et, éventuellement, la protection.

Si vous n’avez pas configuré ces étiquettes, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).

Pour plus d'informations, consultez les pages suivantes :

- [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)
- [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md)

> [!TIP] 
> Utilisez les instructions du [didacticiel](infoprotect-quick-start-tutorial.md) pour tester le scanneur avec une étiquette qui recherche des numéros de carte de crédit dans un document Word préparé. Toutefois, vous devez modifier la configuration de l’étiquette pour que l’option **Sélectionner la manière dont cette étiquette est appliquée** soit définie sur **automatique**, plutôt que sur **recommandé** ou **traiter l’étiquetage recommandé comme automatique** (disponible dans la version 2.7 du scanneur. x. x et versions ultérieures). 
>
> Supprimez ensuite l’étiquette du document (si elle est appliquée), puis copiez le fichier dans un référentiel de données pour le scanneur. 

## <a name="sharepoint-requirements"></a>Configuration requise pour SharePoint

Pour analyser les dossiers et bibliothèques de documents SharePoint, assurez-vous que votre serveur SharePoint est conforme aux exigences suivantes :

- **Versions prises en charge.** Les versions prises en charge sont les suivantes : SharePoint 2019, SharePoint 2016, SharePoint 2013 et SharePoint 2010. D’autres versions de SharePoint ne sont pas prises en charge pour le scanneur.

- **Version.** Lorsque vous utilisez le contrôle de [version](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), le scanneur inspecte et étiquette la dernière version publiée. Si le scanneur étiquette une approbation de fichier et de [contenu](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) est requise, ce fichier doit être approuvé pour être disponible pour les utilisateurs.  

- **Batteries de serveurs SharePoint de grande taille.** Pour les grandes batteries de serveurs SharePoint, regardez si vous devez augmenter le seuil d’affichage de liste (par défaut, 5 000) pour le scanneur pour accéder à tous les fichiers. Pour plus d’informations, consultez [gérer des listes et des bibliothèques de grande taille dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).


## <a name="microsoft-office-requirements"></a>Configuration requise pour la Microsoft Office

Pour analyser les documents Office, vos documents doivent être dans l’un des formats suivants :

- Microsoft Office 97-2003 
- Formats Office Open XML pour Word, Excel et PowerPoint

Pour plus d’informations, consultez [types de fichiers pris en charge par le client Azure information protection](./rms-client/client-admin-guide-file-types.md).

## <a name="file-path-requirements"></a>Exigences relatives au chemin de fichier

Pour analyser les fichiers, vos chemins d’accès aux fichiers doivent comporter 260 caractères au maximum, sauf si le scanneur est installé sur Windows 2016 et que l’ordinateur est configuré pour prendre en charge des chemins d’accès longs.

Windows 10 et Windows Server 2016 prennent en charge des longueurs de chemin de plus de 260 caractères avec le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)suivant : stratégie de l' **ordinateur local**  >  **Configuration ordinateur**  >  **modèles d’administration**  >  **tous les paramètres**  >  **activer les chemins longs Win32**

Pour plus d’informations sur la prise en charge des chemins de fichiers longs, consultez la section consacrée à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

## <a name="usage-statistics-requirements"></a>Exigences relatives aux statistiques d’utilisation

Désactivez les statistiques d’utilisation à l’aide de l’une des méthodes suivantes :

- Affectation de la valeur 0 au paramètre [AllowTelemetry](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-install#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

- Assurez-vous que l’option **contribuer à l’amélioration des Azure information protection en envoyant des statistiques d’utilisation à Microsoft** reste désélectionnée pendant le processus d’installation du scanneur.


## <a name="deploying-the-scanner-with-alternative-configurations"></a>Déploiement du scanneur avec d’autres configurations

Les conditions préalables répertoriées ci-dessus sont les conditions par défaut pour le déploiement de l’analyseur, et recommandées car elles prennent en charge la configuration d’analyseur la plus simple.

Les spécifications par défaut doivent être adaptées au test initial, afin que vous puissiez vérifier les fonctionnalités du scanneur. 

Toutefois, dans un environnement de production, les stratégies de votre organisation peuvent interdire ces exigences par défaut. Le scanneur peut prendre en charge les restrictions suivantes avec une configuration supplémentaire :

- [Le serveur de scanneur ne peut pas disposer d’une connexion Internet](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory mais le serveur dispose d’une connexion Internet](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [Restriction : le compte de service du scanneur ne peut pas se voir accorder le droit **ouvrir une session localement**](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

- [Restriction : vos étiquettes n’ont pas de conditions d’étiquetage automatique](#restriction-your-labels-do-not-have-auto-labeling-conditions)

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction : le serveur de scanneur ne peut pas disposer d’une connexion Internet

Pour prendre en charge un ordinateur déconnecté, procédez comme suit :

1. Configurez vos étiquettes qui appliquent uniquement la classification ou appliquez la protection qui utilise la [protection hyok](configure-adrms-restrictions.md). 

    Sans connexion Internet, le scanneur ne peut pas appliquer la protection, supprimer la protection ou inspecter les fichiers protégés à l’aide de la clé Cloud de votre organisation. Au lieu de cela, le scanneur est limité à l’utilisation d’étiquettes qui appliquent uniquement la classification, ou appliquez la protection qui utilise la protection HYOK.
    
    Pour plus d’informations, consultez [prise en charge des ordinateurs déconnectés](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers).

1. Configurez le scanneur dans le Portail Azure en créant un cluster de scanneur. Si vous avez besoin d’aide pour cette étape, consultez [Configurer le scanneur dans le portail Azure](deploy-aip-scanner-configure-install-classic.md#configure-the-scanner-in-the-azure-portal).

2. Exportez votre travail de contenu à partir du volet **Azure information protection-travaux d’analyse de contenu** à l’aide de l’option d' **exportation** .

3. Dans une session PowerShell, exécutez [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) et spécifiez le fichier contenant les paramètres exportés.

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

Si le rôle sysadmin peut être accordé *temporairement* pour installer le scanneur, vous pouvez supprimer ce rôle une fois l’installation du scanneur terminée.

Effectuez l’une des opérations suivantes, selon les besoins de votre organisation :

- **Vous pouvez avoir le rôle sysadmin temporairement.** Si vous avez temporairement le rôle sysadmin, la base de données est automatiquement créée pour vous et le compte de service du scanneur reçoit automatiquement les autorisations requises.

    Toutefois, le compte d’utilisateur qui configure le scanneur requiert toujours le rôle **db_owner** pour la base de données de configuration de l’analyseur. Si vous avez uniquement le rôle sysadmin jusqu’à ce que l’installation du scanneur soit terminée, [accordez manuellement le rôle db_owner au compte d’utilisateur](#create-a-user-and-grant-db_owner-rights-manually).

- **Vous ne pouvez pas avoir le rôle sysadmin**. Si vous ne pouvez pas recevoir le rôle sysadmin même temporairement, vous devez demander à un utilisateur disposant des droits d’administrateur système de créer manuellement une base de données avant d’installer le scanneur. 

    Pour cette configuration, le rôle de **db_owner** doit être affecté aux comptes suivants : 

    - Compte de service pour le scanneur

    - Compte d’utilisateur pour l’installation du scanneur

    - Compte utilisateur pour la configuration du scanneur
      
    En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Si vous utilisez des comptes différents, ils nécessitent tous deux le rôle db_owner pour la base de données de configuration de l’analyseur. Créez cet utilisateur et les droits nécessaires. 

    Si vous ne spécifiez pas votre propre nom de cluster (profil) pour le scanneur, la base de données de configuration est nommée **AIPScanner_ \<computer_name> **. </br>Poursuivez avec [la création d’un utilisateur et en accordant des droits de db_owner sur la base de données](#create-a-user-and-grant-db_owner-rights-manually). 

En outre :

- Vous devez être un administrateur local sur le serveur qui exécutera le scanneur.
- Le compte de service qui exécutera le scanneur doit disposer des autorisations contrôle total sur les clés de Registre suivantes :
    
    - HKEY_LOCAL_MACHINE \SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\MSIPC\Server

Si, après avoir configuré ces autorisations, vous voyez une erreur lors de l’installation du scanneur, l’erreur peut être ignorée et vous pouvez démarrer manuellement le service du scanneur.

#### <a name="populate-the-database-manually"></a>Remplir la base de données manuellement

Remplissez la base de données à l’aide du script suivant : 

```sql
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END 
```

#### <a name="create-a-user-and-grant-db_owner-rights-manually"></a>Créer un utilisateur et lui accorder des droits db_owner manuellement

Pour créer un utilisateur et accorder des droits de db_owner sur cette base de données, demandez à l’administrateur système d’effectuer les opérations suivantes :

1. Créer une base de connaissances pour le scanneur :

    ```sql
    **CREATE DATABASE AIPScannerUL_[clustername]**
    
    **ALTER DATABASE AIPScannerUL_[clustername] SET TRUSTWORTHY ON**
    ```
    
2. Accordez des droits à l’utilisateur qui exécute la commande d’installation et qui est utilisé pour exécuter des commandes de gestion du scanneur.

    Script SQL :
    
    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. Accordez des droits au compte de service du scanneur.

    Script SQL :

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restriction : le compte de service pour le scanneur ne peut pas obtenir le droit **Ouvrir une session localement**

Si les stratégies de votre organisation interdisent le droit **ouvrir une session localement** pour les comptes de service, mais autorise le droit **ouvrir une session en tant que tâche** , consultez [spécifier et utiliser le paramètre de jeton pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication).

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory mais le serveur dispose d’une connexion Internet

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- **Pour le compte de service du scanneur,** utilisez un compte Windows local ou un compte Active Directory.

- **Pour le compte Azure Active Directory,** [spécifiez et utilisez le paramètre Token pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication).

#### <a name="restriction-your-labels-do-not-have-auto-labeling-conditions"></a>Restriction : vos étiquettes n’ont pas de conditions d’étiquetage automatique

Si vos étiquettes n’ont pas de conditions d’étiquetage automatique, envisagez d’utiliser l’une des options suivantes lors de la configuration de votre scanneur :

|Option  |Description  |
|---------|---------|
|**Découvrir tous les types d’informations**     |  Dans votre [travail d’analyse de contenu](deploy-aip-scanner-configure-install.md#create-a-content-scan-job), définissez l’option **types d’informations sur** **tous**. </br></br>Cette option définit le travail d’analyse de contenu pour analyser votre contenu pour tous les types d’informations sensibles.      |
|**Définir une étiquette par défaut**     |   Définissez une étiquette par défaut dans votre [stratégie](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do), le [travail d’analyse de contenu](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)ou le [référentiel](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository). </br></br>Dans ce cas, le scanner applique l’étiquette par défaut sur tous les fichiers trouvés.       |
| | |

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez confirmé que votre système est conforme aux conditions préalables du scanneur, poursuivez [le déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner-configure-install-classic.md).

Pour obtenir une vue d’ensemble du scanneur, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner-classic.md).

**Plus d’informations :**

Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez [utilisation de PowerShell avec le client Azure information protection Classic](./rms-client/client-admin-guide-powershell.md) .
