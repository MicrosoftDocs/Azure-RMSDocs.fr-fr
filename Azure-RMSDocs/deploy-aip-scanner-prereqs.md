---
title: Prérequis du scanneur d’étiquetage unifiée Azure Information Protection (AIP)
description: Répertorie les conditions préalables à l’installation et au déploiement du scanneur d’étiquetage unifié Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/24/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f190a97e18533640b2edc60513bb29a7ad7d7728
ms.sourcegitcommit: 0793013ad733ac2af5de498289849979501b8f6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88788660"
---
# <a name="prerequisites-for-installing-and-deploying-the-azure-information-protection-unified-labeling-scanner"></a>Conditions préalables à l’installation et au déploiement du scanneur d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows server 2012 R2*

>[!NOTE]
> Si vous utilisez le scanneur classique, consultez [Configuration requise pour l’installation et le déploiement du Azure information protection scanneur classique](deploy-aip-scanner-prereqs-classic.md).

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

Lorsque vous êtes prêt à commencer l’installation et le déploiement de votre scanneur, poursuivez [le déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner-configure-install.md).

## <a name="windows-server-requirements"></a>Configuration requise pour Windows Server

Vous devez disposer d’un ordinateur Windows Server pour exécuter le scanneur, qui présente les spécifications système suivantes :

|Caractéristique  |Détails  |
|---------|---------|
|**Processeur**     |4 processeurs principaux         |
|**RAM**     |8 Go         |
|**Espace disque**     |10 Go d’espace libre (moyenne) pour les fichiers temporaires. </br></br>Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. </br></br>L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo.
|**Système d'exploitation**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**Remarque :** À des fins de test ou d’évaluation dans un environnement hors production, vous pouvez également utiliser n’importe quel système d’exploitation Windows [pris en charge par le client Azure information protection](requirements.md#client-devices).
|**Connectivité réseau**     | Votre ordinateur de scanneur peut être un ordinateur physique ou virtuel avec une connexion réseau rapide et fiable aux magasins de données à analyser. </br></br> Si la connexion Internet n’est pas possible en raison des stratégies de votre organisation, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations). </br></br>Dans le cas contraire, assurez-vous que cet ordinateur dispose d’une connectivité Internet qui autorise les URL suivantes sur HTTPs (port 443) :</br><br />-  \*. aadrm.com <br />-  \*. azurerms.com<br />-  \*. informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*. aria.microsoft.com <br />-  \*. protection.outlook.com |
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

    Le rôle sysadmin permet au processus d’installation de créer automatiquement la base de données de configuration du scanneur et d’accorder le rôle de **db_owner** requis au compte de service qui exécute le scanneur.

    Si vous ne pouvez pas accorder le rôle sysadmin ou si les stratégies de votre organisation nécessitent la création et la configuration de bases de données manuellement, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).

- **Capacité.** Pour obtenir des conseils sur la capacité, consultez [exigences de stockage et planification de la capacité pour SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

- **[Classement non sensible à la casse](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15)**

> [!NOTE]
> Plusieurs bases de données de configuration sur le même serveur SQL Server sont prises en charge lorsque vous spécifiez un nom de cluster personnalisé (profil) pour le scanneur, ou lorsque vous utilisez la version préliminaire du scanneur.
>
### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Exigences de stockage et planification de la capacité pour SQL Server

La quantité d’espace disque requise pour la base de données de configuration du scanneur et la spécification de l’ordinateur qui exécute SQL Server peuvent varier pour chaque environnement, nous vous encourageons donc à effectuer vos propres tests. Utilisez les instructions suivantes comme point de départ.

Pour plus d’informations, consultez [optimisation des performances du scanneur](deploy-aip-scanner-configure-install.md#optimizing-scanner-performance).

La taille du disque de la base de données de configuration de l’analyseur varie pour chaque déploiement. Utilisez l’équation suivante en guise d’aide :

```cli
100 KB + <file count> *(1000 + 4* <average file name length>)
```

Par exemple, pour analyser les fichiers 1 million dont la longueur moyenne du nom de fichier est de 250 octets, allouez un espace disque de 2 Go.

Pour plusieurs Scanneurs :

- **Jusqu’à 10 scanneurs,** utilisez :

    - 4 processeurs principaux
    - 8 Go de RAM recommandés

- **Plus de 10 scanneurs** (40 maximum), utilisez :
    - 8 processus de base
    - 16 Go de RAM recommandés

## <a name="azure-information-protection-client-requirements"></a>Configuration requise pour le client Azure Information Protection

Vous devez disposer de la [version actuelle de la disponibilité générale](./rms-client/unifiedlabelingclient-version-release-history.md) du client Azure information Protection installé sur l’ordinateur Windows Server.

Pour plus d’informations, consultez le [Guide d’administration du client d’étiquetage unifié](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner).

> [!IMPORTANT]
> Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.
>

## <a name="label-configuration-requirements"></a>Configuration requise pour l’étiquette

Vous devez configurer des étiquettes qui appliquent automatiquement la classification et, éventuellement, la protection.

Si vous n’avez pas configuré ces étiquettes, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).

Pour plus d'informations, consultez les pages suivantes :

- [Appliquer automatiquement une étiquette sensibilité au contenu](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [Restriction de l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)

## <a name="sharepoint-requirements"></a>Configuration requise pour SharePoint

Pour analyser les dossiers et bibliothèques de documents SharePoint, assurez-vous que votre serveur SharePoint est conforme aux exigences suivantes :

- **Versions prises en charge.** Les versions prises en charge sont les suivantes : SharePoint 2019, SharePoint 2016, SharePoint 2013 et SharePoint 2010. D’autres versions de SharePoint ne sont pas prises en charge pour le scanneur.

- **Version.** Lorsque vous utilisez le contrôle de [version](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), le scanneur inspecte et étiquette la dernière version publiée. Si le scanneur étiquette une approbation de fichier et de [contenu](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) est requise, ce fichier doit être approuvé pour être disponible pour les utilisateurs.  

- **Batteries de serveurs SharePoint de grande taille.** Pour les grandes batteries de serveurs SharePoint, regardez si vous devez augmenter le seuil d’affichage de liste (par défaut, 5 000) pour le scanneur pour accéder à tous les fichiers. Pour plus d’informations, consultez [gérer des listes et des bibliothèques de grande taille dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

## <a name="microsoft-office-requirements"></a>Configuration requise pour la Microsoft Office

Pour analyser les documents Office, vos documents doivent être dans l’un des formats suivants :

- Microsoft Office 97-2003
- Formats Office Open XML pour Word, Excel et PowerPoint

Pour plus d’informations, consultez [types de fichiers pris en charge par le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-file-types.md).

## <a name="file-path-requirements"></a>Exigences relatives au chemin de fichier

Par défaut, pour analyser les fichiers, vos chemins d’accès aux fichiers doivent comporter jusqu’à 260 caractères.

Pour analyser des fichiers avec des chemins d’accès de plus de 260 caractères, installez le scanneur sur un ordinateur avec l’une des versions suivantes de Windows et configurez l’ordinateur en fonction des besoins :

|Version de Windows  |Description  |
|---------|---------|
|**Windows 2016 ou version ultérieure**     |   Configurer l’ordinateur pour prendre en charge des chemins d’accès longs      |
|**Windows 10 ou Windows Server 2016**     | Définissez le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)suivant : stratégie de l' **ordinateur local**  >  **Configuration ordinateur**  >  **modèles d’administration**  >  **tous les paramètres**  >  **activer les chemins d’accès longs Win32**.    </br></br>Pour plus d’informations sur la prise en charge des chemins de fichiers longs dans ces versions, consultez la section limitation de la [longueur maximale du chemin d’accès](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation du développeur Windows 10.    |
|**Windows 10, version 1607 ou ultérieure**     |  Abonnez-vous à la fonctionnalité de **MAX_PATH** mise à jour. Pour plus d’informations, consultez [activer des chemins d’accès longs dans Windows 10 versions 1607 et ultérieures](https://docs.microsoft.com/windows/win32/fileio/naming-a-file#enable-long-paths-in-windows-10-version-1607-and-later).      |
| | |

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

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction : le serveur de scanneur ne peut pas disposer d’une connexion Internet

Pour prendre en charge un ordinateur déconnecté, procédez comme suit :

1. Configurez des étiquettes dans votre stratégie, puis importez la stratégie à l’aide de l’applet de commande [Import-AIPScannerConfiguration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration?view=azureipps) . Alors que le client d’étiquetage unifié ne peut pas appliquer la protection sans connexion Internet, le scanneur peut toujours appliquer des étiquettes basées sur des stratégies importées.

1. Configurez le scanneur dans le Portail Azure en créant un cluster de scanneur. Si vous avez besoin d’aide pour cette étape, consultez [Configurer le scanneur dans le portail Azure](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

1. Exportez votre travail de contenu à partir du volet **Azure information protection-travaux d’analyse de contenu** à l’aide de l’option d' **exportation** .

1. Dans une session PowerShell, exécutez [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) et spécifiez le fichier contenant les paramètres exportés.

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

    En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Si vous utilisez des comptes différents, ils nécessitent tous deux le rôle db_owner pour la base de données de configuration de l’analyseur. Créez cet utilisateur et les droits nécessaires. Si vous spécifiez votre propre nom de cluster (profil), la base de données de configuration est nommée **AIPScannerUL_<cluster_name>**.

En outre :

- Vous devez être un administrateur local sur le serveur qui exécutera le scanneur.
- Le compte de service qui exécutera le scanneur doit disposer des autorisations contrôle total sur les clés de Registre suivantes :

    - HKEY_LOCAL_MACHINE \SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\MSIPC\Server

Si, après avoir configuré ces autorisations, vous voyez une erreur lors de l’installation du scanneur, l’erreur peut être ignorée et vous pouvez démarrer manuellement le service du scanneur.

#### <a name="populate-the-database-manually"></a>Remplir la base de données manuellement

Remplissez la base de données à l’aide du script suivant :

```cli
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END 
```

#### <a name="create-a-user-and-grant-db_owner-rights-manually"></a>Créer un utilisateur et lui accorder des droits db_owner manuellement

Pour créer un utilisateur et accorder des droits de db_owner sur cette base de données, demandez à l’administrateur système d’effectuer les étapes suivantes :

1. Créer une base de connaissances pour le scanneur :

    ```cli
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

Si les stratégies de votre organisation interdisent le droit **ouvrir une session localement** pour les comptes de service, mais autorise le droit **ouvrir une session en tant que tâche** , utilisez le paramètre *OnBehalfOf* avec set-AIPAuthentication.

Pour plus d’informations, consultez [Comment étiqueter des fichiers de manière non interactive pour Azure information protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory mais le serveur dispose d’une connexion Internet

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- **Pour le compte de service du scanneur,** utilisez un compte Windows local ou un compte Active Directory.

- **Pour le compte Azure Active Directory,** spécifiez votre compte local pour le paramètre *OnBehalfOf* avec set-AIPAuthentication. Pour plus d’informations, consultez [Comment étiqueter des fichiers de manière non interactive pour Azure information protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez confirmé que votre système est conforme aux conditions préalables du scanneur, poursuivez [le déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner-configure-install.md).

Pour obtenir une vue d’ensemble du scanneur, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner.md).

**Plus d’informations :**

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md).
