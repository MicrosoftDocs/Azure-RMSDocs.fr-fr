---
title: Deploy the Azure Information Protection scanner - AIP
description: Instructions to install, configure, and run the current version of the Azure Information Protection scanner to discover, classify, and protect files on data stores.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0b53c721725f83b8e197552d4c1fa502583fc2f9
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474362"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2*
>
> [!NOTE]
> This article is for the current general availability version of the Azure Information Protection scanner with the Azure Information Protection client (classic), and the preview version of the scanner for the current general availability version of the Azure Information Protection unified labeling client.
> 
> If you have previously installed the scanner and want to upgrade it, use the following upgrade instructions and then use the instructions on this page, omitting the step to install the scanner:
> - For the classic client: [Upgrading the Azure Information Protection scanner](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> - For the unified labeling client: [Upgrading the Azure Information Protection scanner](./rms-client/clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> 
> If you have a version of the scanner that is older than 1.48.204.0 and you're not ready to upgrade it, see [Deploying previous versions of the Azure Information Protection scanner to automatically classify and protect files](deploy-aip-scanner-previousversions.md).


Utilisez ces informations pour en savoir plus sur le scanneur Azure Information Protection, puis sur la manière de l’installer, de le configurer et de l’exécuter correctement.

Ce scanneur s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les magasins de données suivants :

- Dossiers locaux sur l’ordinateur Windows Server qui exécute le scanneur.

- Chemins UNC pour les partages réseau qui utilisent le protocole SMB (Server Message Block).

- Document libraries and folders for SharePoint Server 2019 through SharePoint Server 2013. SharePoint 2010 est également pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Pour analyser et étiqueter des fichiers sur des référentiels cloud, utilisez [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) au lieu du scanneur.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Présentation du scanneur Azure Information Protection

When you have configured labels that apply automatic classification, files that this scanner discovers can then be labeled. Les étiquettes appliquent une classification et elles appliquent ou suppriment éventuellement la protection :

![Présentation de l’architecture du scanneur Azure Information Protection](./media/infoprotect-scanner.png)

Le scanneur peut inspecter tous les fichiers que Windows est capable d’indexer à l’aide de filtres IFilter installés sur l’ordinateur. Ensuite, pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise la détection de modèles et les types d’informations sensibles de protection contre la perte de données intégrée à Office 365 ou les modèles regex Office 365. Because the scanner uses the Azure Information Protection client (the classic client or unified labeling client), the scanner can classify and protect the same file types:

- The classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)

- The unified labeling  client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)

Vous pouvez exécuter le scanneur en mode découverte uniquement, dans lequel vous utilisez les rapports pour vérifier ce qui se passerait si les fichiers étaient étiquetés. Ou bien, vous pouvez exécuter le scanneur pour appliquer automatiquement les étiquettes. Vous pouvez également exécuter le scanneur pour découvrir les fichiers contenant des types d’informations sensibles, sans configurer d’étiquettes pour les conditions qui appliquent la classification automatique.

Notez que le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers dans les magasins de données que vous spécifiez. Vous pouvez configurer ce cycle pour s’exécuter une ou plusieurs fois.

Vous pouvez spécifier les types de fichiers à analyser, ou à exclure de l’analyse, en définissant une liste de types de fichiers dans le cadre de la configuration du scanneur.


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prérequis pour le scanneur Azure Information Protection
Avant d’installer le scanneur Azure Information Protection, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Autres informations|
|---------------|--------------------|
|Ordinateur Windows Server pour exécuter le service du scanneur :<br /><br />- Processeurs 4 cœurs<br /><br />- 8 Go de RAM<br /><br />- 10 Go d’espace libre (en moyenne) pour les fichiers temporaires|Windows Server 2019, Windows Server 2016, or Windows Server 2012 R2. <br /><br />Remarque : À des fins de test ou d’évaluation dans un environnement hors production, vous pouvez utiliser un système d’exploitation client Windows qui est [pris en charge par le client Azure Information Protection](requirements.md#client-devices).<br /><br />Il peut s’agir d’un ordinateur physique ou virtuel doté d’une connexion réseau rapide et fiable aux magasins de données à scanner.<br /><br /> Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo. <br /><br /> If internet connectivity is not possible because of your organization policies, see the [Deploying the scanner with alternative configurations](#deploying-the-scanner-with-alternative-configurations) section. Otherwise, make sure that this computer has internet connectivity that allows the following URLs over HTTPS (port 443):<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com <br /> \*.protection.outlook.com (scanner from the unified labeling client only)|
|Compte de service pour exécuter le service du scanneur|En plus d’exécuter le service du scanneur sur l’ordinateur Windows Server, ce compte Windows s’authentifie auprès d’Azure AD, puis télécharge la stratégie Azure Information Protection. Ce compte doit être un compte Active Directory et synchronisé avec Azure AD. Si vous ne pouvez pas synchroniser ce compte en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />Ce compte de service a la configuration suivante :<br /><br />- **Ouvrir une session localement**, attribution des droits utilisateur. Ce droit est exigé pour l’installation et la configuration du scanneur, mais pas pour son fonctionnement. Vous devez accorder ce droit au compte de service, mais vous pouvez le supprimer après avoir vérifié que le scanneur peut détecter, classifier et protéger des fichiers. Si l’attribution de ce droit, même pendant une courte période, n’est pas possible en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />- **Ouvrir une session en tant que service**, attribution des droits utilisateur. Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur. <br /><br />- Autorisations d’accès aux dépôts de données : vous devez accorder des autorisations de **Lecture** et **Écriture** pour l’analyse des fichiers, puis l’application d’une classification et d’une protection aux fichiers qui remplissent les conditions stipulées dans la stratégie Azure Information Protection. Pour exécuter le scanneur en mode découverte uniquement, l’autorisation **Lecture** suffit.<br /><br />- For labels that reprotect or remove protection: To ensure that the scanner always has access to protected files, make this account a [super user](configure-super-users.md) for Azure Information Protection, and ensure that the super user feature is enabled. En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que ce compte est inclus dans les contrôles d’intégration que vous avez configurés.|
|SQL Server pour stocker la configuration du scanneur :<br /><br />- Instance locale ou distante<br /><br />- [Case insensitive collation](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />-Rôle sysadmin pour installer le scanneur|SQL Server 2012 est la version minimale pour les éditions suivantes :<br /><br />- SQL Server Entreprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance SQL Server lorsque vous spécifiez un nom de profil personnalisé pour le scanneur. When you use the preview version of the scanner from the unified labeling client, multiple scanners can share the same configuration database.<br /><br />Lorsque vous installez le scanneur et si votre compte a le rôle Sysadmin, le processus d’installation crée automatiquement la base de données de configuration du scanneur et accorde le rôle db_owner requis au compte de service qui exécute le scanneur. Si vous ne pouvez pas disposer du rôle Sysadmin ou si les stratégies de votre organisation requièrent que les bases de données soient créées et configurées manuellement, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br /> For capacity guidance, see [Storage requirements and capacity planning for SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).|
|Either of the following Azure Information Protection clients is installed on the Windows Server computer <br /><br /> - Classic client <br /><br /> - Unified labeling client ([current general availability version only](./rms-client/unifiedlabelingclient-version-release-history.md#version-25330)) |Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.<br /><br />For installation and upgrade instructions: <br /> - [Classic client](./rms-client/client-admin-guide.md)<br /> - [Unified labeling client](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner) |
|Étiquettes configurées qui appliquent une classification automatique et éventuellement une protection|For instructions for the classic client to configure a label for conditions and to apply protection:<br /> - [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)<br /> - [Comment configurer une étiquette pour la protection Rights Management](configure-policy-protection.md) <br /><br />Tip: You can use the instructions from the [tutorial](infoprotect-quick-start-tutorial.md) to test the scanner with a label that looks for credit card numbers in a prepared Word document. Vous devez toutefois modifier la configuration de l’étiquette afin que **Sélectionner comment cette étiquette est appliquée** soit défini sur **Automatique** plutôt que sur **Recommandé**. Supprimez ensuite l’étiquette du document (si elle est appliquée), puis copiez le fichier dans un référentiel de données pour le scanneur. Pour effectuer un test rapide, il peut s’agir d’un dossier local sur l’ordinateur du scanneur.<br /><br /> For instructions for the unified labeling client to configure a label for auto-labeling and to apply protection:<br /> - [Apply a sensitivity label to content automatically](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)<br /> - [Restrict access to content by using encryption in sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)<br /><br /> Bien que vous puissiez exécuter le scanneur même si vous n’avez pas configuré les étiquettes qui appliquent la classification automatique, ce scénario n’est pas abordé dans ces instructions. [Plus d’informations](#using-the-scanner-with-alternative-configurations)|
|For SharePoint document libraries and folders to be scanned:<br /><br />- SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|D’autres versions de SharePoint ne sont pas prises en charge pour le scanneur.<br /><br />When you use [versioning](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), the scanner inspects and labels the last published version. If the scanner labels a file and [content approval](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) is required, that labeled file must be approved to be available for users. <br /><br />Pour les grandes batteries de serveurs SharePoint, regardez si vous devez augmenter le seuil d’affichage de liste (par défaut, 5 000) pour le scanneur pour accéder à tous les fichiers. For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Pour scanner des documents Office :<br /><br />- formats de fichier 97-2003 et formats Office Open XML pour Word, Excel et PowerPoint|For more information about the file types that the scanner supports for these file formats, see the following information: <br />- Classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)<br />- Unified labeling client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)|
|Pour les chemins longs :<br /><br />- 260 caractères maximum, sauf si le scanneur est installé sur Windows 2016 et que l’ordinateur est configuré pour prendre en charge les chemins longs.|Windows 10 and Windows Server 2016 support path lengths greater than 260 characters with the following [group policy setting](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/): **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **All Settings** > **Enable Win32 long paths**<br /><br /> Pour plus d’informations sur la prise en charge des chemins de fichiers longs, consultez la section consacrée à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

If you can't meet all the requirements in the table because they are prohibited by your organization policies, see the [alternative configurations](#deploying-the-scanner-with-alternative-configurations) section.

When you deploy the scanner in production, or you're testing the performance for multiple scanners, see the next section for capacity planning guidance for SQL Server.

However, if you're ready to start deploying the scanner, go straight to [configuring the scanner section](#configure-the-scanner-in-the-azure-portal).

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Storage requirements and capacity planning for SQL Server

The amount of disk space required for the scanner's configuration database and the specification of the computer running SQL Server can vary for each environment, so we encourage you to do your own testing. However, you can use the following guidance as a starting point.

See the [Optimizing the performance of the scanner](#optimizing-the-performance-of-the-scanner) section for additional information.

##### <a name="scanner-from-the-classic-client"></a>Scanner from the classic client:

- **Disk size**: The size of the configuration database will vary for each deployment but we recommend you allocate 500 MB for every 1,000,000 files that you want to scan.

- **For each scanner**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

##### <a name="scanner-from-the-unified-labeling-client"></a>Scanner from the unified labeling client:

- **Disk size**: Although the size of the scanner configuration database will vary for each deployment, you can use the following equation as guidance: `100 KB + <file count> *(1000 + 4*<average file name length>)`. 
    
    For example, to scan 1 million files that have an average file name length of 250 bytes, allocate 2 GB disk space.

- **For multiple scanners, up to 12**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

- **For multiple scanners more than 12 (maximum 40)** : 8 core processes; 16 GB RAM recommended (8 GB minimum).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Déploiement du scanneur avec d’autres configurations

Les prérequis répertoriés dans la table correspondent aux exigences par défaut pour le scanneur et sont recommandés pour obtenir la configuration la plus simple pour le déploiement du scanneur. Ils doivent être adaptés aux tests initiaux, afin que vous puissiez vérifier les fonctionnalités du scanneur. Toutefois, dans un environnement de produit, les stratégies de votre organisation peuvent interdire ces exigences par défaut en raison d’une ou plusieurs des restrictions suivantes :

- Servers are not allowed internet connectivity

- Vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

- Les comptes de service ne peut pas obtenir le droit **Ouvrir une session localement**

- Service accounts cannot be synchronized to Azure Active Directory but servers have internet connectivity

Le scanneur peut prendre en charge ces restrictions, mais celles-ci nécessitent une configuration supplémentaire.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction: The scanner server cannot have internet connectivity

Follow the instructions from the admin guides to support a disconnected computer:

- For the classic client: [Support for disconnected computers](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the classic client cannot apply protection, remove protection, or inspect protected files by using your organization's cloud-based key. Instead, the scanner is limited to using labels that apply classification only, or apply protection that uses [HYOK](configure-adrms-restrictions.md)

- For the unified labeling client: [Support for disconnected computers](./rms-client/clientv2-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the unified labeling client can apply protection, remove protection, and inspect protected files by using the *DelegatedUser* parameter with the [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) cmdlet.

Effectuez ensuite les opérations suivantes :

1. Configurez le scanneur dans le portail Azure, en créant un profil de scanneur. Si vous avez besoin d’aide pour cette étape, consultez [Configurer le scanneur dans le portail Azure](#configure-the-scanner-in-the-azure-portal).

2. Export your scanner profile from the **Azure Information Protection - Profiles** pane, by using the **Export** option.

3. Pour finir, dans une session PowerShell, exécutez [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) et spécifiez le fichier qui contient les paramètres exportés.

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

Si le rôle Sysadmin peut vous être attribué temporairement pour installer le scanneur, vous pouvez supprimer ce rôle lorsque l’installation du scanneur est terminée. Lorsque vous utilisez cette configuration, la base de données est automatiquement créée pour vous et le compte de service du scanneur obtient automatiquement les autorisations nécessaires. Toutefois, le compte d’utilisateur qui configure le scanneur nécessite le rôle db_owner pour la base de données de configuration du scanneur, et vous devez attribuer manuellement ce rôle au compte d’utilisateur.

If you cannot be granted the Sysadmin role even temporarily, you must ask a user with Sysadmin rights to manually create a database before you install the scanner. For this configuration, the following roles must be assigned:
    
|Compte|Rôle au niveau de la base de données|
|--------------------------------|---------------------|
|Compte de service pour le scanneur|db_owner|
|Compte utilisateur pour l’installation du scanneur|db_owner|
|Compte utilisateur pour la configuration du scanneur |db_owner|

En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Mais si vous utilisez des comptes différents, ils ont tous les deux besoin du rôle db_owner pour la base de données de configuration du scanneur :

- If you do not specify your own profile name for the scanner (classic client only), the configuration database is named **AIPScanner_\<computer_name>** . 

- If you specify your own profile name, the configuration database is named **AIPScanner_\<profile_name>** (classic client) or **AIPScannerUL_\<profile_name>** (unified labeling client).

To create a user and grant db_owner rights on this database, ask the Sysadmin to run the following SQL script twice. The first time, for the service account that runs the scanner, and the second time for you to install and manage the scanner. Before running the script:
1. Replace *domain\user* with the domain name and user account name of the service account or user account.
2. Replace *DBName* with the name of the scanner configuration database.

SQL script:

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END

En outre :

- You must be a local administrator on the server that will run the scanner
- The service account that will run the scanner must be granted Full Control permissions to the following registry keys:
    
    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

If, after configuring these permissions, you see an error when you install the scanner, the error can be ignored and you can manually start the scanner service.


#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restriction : le compte de service pour le scanneur ne peut pas obtenir le droit **Ouvrir une session localement**

If your organization policies prohibit the **Log on locally** right for service accounts but allow the **Log on as a batch job** right, use the following instructions:

- For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.

- For the unified labeling client: Use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction: The scanner service account cannot be synchronized to Azure Active Directory but the server has internet connectivity

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- Pour le compte de service du scanneur, vous pouvez utiliser un compte Windows local ou un compte Active Directory.

- For the Azure Active Directory account, use the following instructions:
    - For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    - For the unified labeling client: Specify your local account for the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.


## <a name="configure-the-scanner-in-the-azure-portal"></a>Configurer le scanneur dans le portail Azure

Before you install the scanner, or upgrade it from an older general availability version of the scanner, create a profile for the scanner in the Azure portal. Vous configurez le profil pour définir les paramètres du scanneur et les référentiels de données à analyser.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. Recherchez les options de menu **Scanneur**, puis sélectionnez **Profils**.

3. Dans le volet **Azure Information Protection - Profils**, sélectionnez **Ajouter** :
    
    ![Ajouter un profil pour le scanneur Azure Information Protection](./media/scanner-add-profile.png)

4. Dans le volet **Ajouter un nouveau profil**, donnez un nom au scanneur utilisé pour identifier ses paramètres de configuration et référentiels de données à analyser. Par exemple, vous pouvez spécifier **Europe** pour identifier l’emplacement géographique des référentiels de données couverts par votre scanneur. Lorsque vous installerez ou mettrez à niveau le scanneur ultérieurement, vous devrez spécifier le même nom de profil.
    
    Si vous le souhaitez, entrez une description des raisons administratives, pour vous aider à identifier le nom de profil du scanneur.

5. For this initial configuration, configure the following settings, and then select **Save** but do not close the pane:
    
    For the **Profile settings** section:
    - **Schedule**: Keep the default of **Manual**
    - **Info types to be discovered**: Change to **Policy only**
    - **Configure repositories**: Do not configure at this time because the profile must first be saved.
    
    For the **Policy enforcement** section:
    - **Enforce**: Select **Off**
    - **Label files based on content**: Keep the default of **On**
    - **Default label**: Keep the default of **Policy default**
    - **Relabel files**: Keep the default of **Off**
    
    For the **Configure file settings** section:
    - **Preserve "Date modified", "Last modified" and "Modified by"** : Keep the default of **On**
    - **File types to scan**: Keep the default file types for **Exclude**
    - **Default owner**: Keep the default of **Scanner Account**

6. Maintenant que le profil est créé et enregistré, vous pouvez revenir à l’option **Configure repositories** (Configurer des référentiels) pour spécifier les magasins de données à analyser. You can specify local folders, UNC paths, and SharePoint Server URLs for SharePoint on-premises document libraries and folders. 
    
    SharePoint Server 2019, SharePoint Server 2016, and SharePoint Server 2013 are supported for SharePoint. SharePoint Server 2010 est également pris en charge lorsque vous bénéficiez d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
    To add your first data store, still on the **Add a new profile** pane, select **Configure repositories** to open the **Repositories** pane:
    
    ![Configurer des référentiels de données pour le scanneur Azure Information Protection](./media/scanner-repositories-bar.png)

7. Dans le volet **Référentiels**, sélectionnez **Ajouter** :
    
    ![Ajouter un référentiel de données pour le scanneur Azure Information Protection](./media/scanner-repository-add.png)

8. On the **Repository** pane, specify the path for the data repository. 
    
    Les caractères génériques ne sont pas pris en charge, ni les emplacements WebDav.
    
    Exemples :
    
    - Pour un chemin d’accès local : `C:\Folder`
    
    - Pour un partage réseau : `C:\Folder\Filename`
    
    - Pour un chemin d’accès UNC : `\\Server\Folder`
    
    - Pour une bibliothèque SharePoint : `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > Si vous ajoutez un chemin d’accès SharePoint pour « Documents partagés » :
    >
     >- Spécifiez **Documents partagés** dans le chemin d’accès lorsque vous souhaitez analyser tous les documents et tous les dossiers de Documents partagés. Par exemple : `http://sp2013/Shared Documents`
     >
     >- Spécifiez **Documents** dans le chemin d’accès lorsque vous souhaitez analyser tous les documents et tous les dossiers d’un sous-dossier sous Documents partagés. Par exemple : `http://sp2013/Documents/Sales Reports`
    
    For the remaining settings on this pane, do not change them for this initial configuration, but keep them as **Profile default**. Cela signifie que le référentiel de données hérite des paramètres du profil de scanneur. 
    
    Sélectionnez **Enregistrer**.

9. Si vous souhaitez ajouter un autre référentiel de données, répétez les étapes 7 et 8.

10. You can now close **Repositories** pane and your profile pane. Back on the **Azure Information Protection - Profiles** pane, you see your profile name displayed, together with the **SCHEDULE** column showing **Manual** and the **ENFORCE** column is blank.

Vous pouvez maintenant installer le scanneur avec le profil de scanneur que vous venez de créer.

## <a name="install-the-scanner"></a>Installer le scanneur

1. Connectez-vous à l’ordinateur Windows Server qui exécutera le scanneur. Utilisez un compte disposant de droits d’administrateur local et qui est autorisé à écrire dans la base de données principale SQL Server.

2. Ouvrez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Exécutez la cmdlet [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), en spécifiant l’instance SQL Server où créer une base de données pour le scanneur Azure Information Protection et le nom du profil de scanneur que vous avez spécifié dans la section précédente : 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    Exemples utilisant le nom de profil **Europe** :
    
    - Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    Quand vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur (\<domaine\nom d’utilisateur>) et le mot de passe.

4. Vérifiez que le service est maintenant installé en utilisant **Outils d’administration** > **Services**. 
    
    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie afin de pouvoir exécuter le scanneur sans assistance. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Obtenir un jeton Azure AD pour le scanneur

The Azure AD token lets the scanner authenticate to the Azure Information Protection service.

1. Return to the Azure portal to create two Azure AD applications (just one Azure AD application for the scanner from the unified labeling client) that are needed to specify an access token for authentication. This token lets the scanner run non-interactively.
    
    To create these applications, follow the instructions in the admin guides for the relevant clients:
    
    - For the classic client: [How to label files non-interactively for Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)
    
    - For the unified labeling client: [How to label files non-interactively for Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

2. À partir de l’ordinateur Windows Server, si votre compte de service de scanneur a reçu l’autorisation **Ouvrir une session localement** pour l’installation : connectez-vous avec ce compte et démarrez une session PowerShell. Exécutez [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), en spécifiant les valeurs copiées à partir de l’étape précédente :
    
    **For the classic client:**
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    Lorsque vous y êtes invité, spécifiez le mot de passe des informations d’identification de votre compte de service pour Azure AD, puis cliquez sur **Accepter**.
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation see [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    
    **For the unified labeling client:**
    
    ```
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation, use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) from that client's admin guide.

The scanner now has a token to authenticate to Azure AD, which is valid for one year, two years, or never expires, according to your configuration of the **Web app /API** (classic client) or client secret (unified labeling client) in Azure AD. Quand le jeton expire, vous devez répéter les étapes 1 et 2.

Vous pouvez maintenant exécuter votre première analyse en mode découverte.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Exécuter un cycle de découverte et afficher les rapports pour le scanneur

1. In the Azure portal, on the **Azure Information Protection - Profiles** pane, select your scanner's profile, and then the **Scan now** option:
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)
    
    Dans votre session PowerShell, vous pouvez également exécuter la commande suivante :
    
        Start-AIPScan

2. Attendez que le scanneur termine son cycle. Une fois que le scanneur a parcouru tous les fichiers inclus dans les magasins de données que vous avez spécifiés, le service s’arrête alors que le service du scanneur continue de s’exécuter :
    
    - On the **Azure Information Protection - Profiles** pane, use the **Refresh** option and wait until you see values for the **LAST SCAN RESULTS** column and the **LAST SCAN (END TIME)** column.
    
    - Dans PowerShell, vous pouvez exécuter `Get-AIPScannerStatus` pour surveiller le changement d’état.
    
    - Scanner from the classic client only: Check the local Windows **Applications and Services** event log, **Azure Information Protection**. Ce journal indique également lorsque le scanneur a terminé l’analyse, avec un résumé des résultats. Recherchez l’ID d’événement d’information **911**.

3. Passez en revue les rapports stockés dans %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Les fichiers de résumé .txt incluent la durée de l’analyse, le nombre de fichiers analysés et le nombre de fichiers correspondants aux types d’informations. Les fichiers .csv offrent plus de détails pour chaque fichier. Ce dossier stocke jusqu’à 60 rapports pour chaque cycle d’analyse et tous, sauf le dernier rapport, sont compressés afin de réduire l’espace disque requis.
    
    > [!NOTE]
    > Vous pouvez modifier le niveau de journalisation à l’aide du paramètre *ReportLevel* avec [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration), mais vous ne pouvez pas modifier l’emplacement ou le nom du dossier de rapport. Envisagez d’utiliser une jointure de répertoire pour le dossier si vous souhaitez stocker les rapports sur un autre volume ou une autre partition.
    >
    > Par exemple, à l’aide de la commande [Mklink](/windows-server/administration/windows-commands/mklink) : `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    Avec notre paramètre **Policy only** (Stratégie uniquement) pour **Info types to be discovered** (Types d’infos à découvrir), seuls les fichiers qui remplissent les conditions que vous avez configurées pour la classification automatique sont inclus dans les rapports détaillés. Si vous ne voyez pas les étiquettes appliquées, vérifiez que la configuration de votre étiquette inclut la classification automatique au lieu de la classification recommandée.
    
    > [!TIP]
    > Les scanneurs envoient ces informations à Azure Information Protection toutes les cinq minutes, ce qui permet de voir les résultats en quasi temps quasi réel sur le Portail Azure. Pour plus d’informations, consultez [Création de rapports pour Azure Information Protection](reports-aip.md). 
        
    If the results are not as you expect, you might need to reconfigure the conditions that you specified for you labels. Si tel est le cas, répétez les étapes 1 à 3 jusqu’à ce que vous soyez prêt à modifier la configuration pour appliquer la classification et éventuellement la protection. 

Le portail Azure affiche des informations portant uniquement sur la dernière analyse. Si vous devez consulter les résultats des analyses précédentes, accédez aux rapports qui sont stockés sur l’ordinateur du scanneur, dans le dossier %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

Quand vous êtes prêt à étiqueter automatiquement les fichiers que le scanneur découvre, passez à la procédure suivante. 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurer le scanneur pour appliquer la classification et la protection

Si vous suivez ces instructions, le scanneur s’exécute une seule fois en mode création de rapports uniquement. Pour modifier ces paramètres, modifiez le profil du scanneur :

1. Back on the **Azure Information Protection - Profiles** pane, select the scanner profile to edit it.

2. On the \<**profile name**> pane, change the following two settings, and then select **Save**:
    
   - From the **Profile settings** section: Change the **Schedule** to **Always**
   - From the **Policy enforcement** section: Change **Enforce** to **On**
    
     Il existe d’autres paramètres de configuration que vous pouvez modifier. Par exemple, si les attributs de fichier sont modifiés et que le scanneur peut réétiqueter les fichiers. Utilisez l’aide contextuelle des informations pour plus d’informations sur chaque paramètre de configuration.

3. Make a note of the current time and start the scanner again from the **Azure Information Protection - Profiles** pane:
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)
    
    Vous pouvez également exécuter la commande suivante dans votre session PowerShell :
    
        Start-AIPScan

4. Scanner from the classic client only: Monitor the event log for the informational type **911** again, with a time stamp later than when you started the scan in the previous step.
    
    Puis examinez les rapports pour déterminer quels fichiers ont été étiquetés, quelle classification a été appliquée et si une protection a été appliquée. Ou bien, utilisez le portail Azure pour consulter plus facilement ces informations.

Puisque nous avons configuré la planification pour qu’elle s’exécute en continu, lorsque le scanneur a parcouru tous les fichiers, il démarre automatiquement un nouveau cycle pour découvrir les fichiers nouveaux et modifiés.

## <a name="how-files-are-scanned"></a>Procédure d’analyse des fichiers

Lors de l’analyse de fichiers, le scanneur effectue les processus suivants.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Determine whether files are included or excluded for scanning 
The scanner automatically skips files that are excluded from classification and protection, such as executable files and system files. For more information, see the following admin guides:

- For the classic client: [File types that are excluded from classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- For the unified labeling client: [File types that are excluded from classification and protection](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

Vous pouvez modifier ce comportement en définissant une liste de types de fichiers à analyser ou à exclure de l’analyse. Vous pouvez spécifier cette liste pour le scanneur à appliquer à tous les référentiels de données par défaut, et vous pouvez spécifier une liste pour chaque référentiel de données. Pour spécifier cette liste, utilisez le paramètre **Files types to scan** (Types de fichiers à analyser) dans le profil du scanneur :

![Configurer les types de fichiers à analyser pour le scanneur Azure Information Protection](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. Inspect and label files

Le scanneur utilise ensuite des filtres pour analyser les types de fichiers pris en charge. Ces mêmes filtres sont utilisés par le système d’exploitation pour Windows Search et l’indexation. Sans configuration supplémentaire, Windows IFilter permet d’analyser les types de fichiers utilisés par Word, Excel, PowerPoint ansi que les documents PDF et les fichiers texte.

For a full list of file types that are supported by default, and additional information how to configure existing filters that include .zip files and .tiff files, see the following admin guides:

- For the classic client: [File types supported for inspection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)
- For the unified labeling client: [File types supported for inspection](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)

Après inspection, ces types de fichiers peuvent être étiquetés à l’aide des conditions que vous avez spécifiées pour vos étiquettes. Ou, si vous utilisez le mode de découverte, ces fichiers peuvent être signalés comme contenant les conditions que vous avez spécifiées pour vos étiquettes ou tous les types d’informations sensibles connus. 

Toutefois, le scanneur ne peut pas étiqueter les fichiers dans les cas suivants :

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- L’étiquette applique la classification et la protection, mais le scanneur ne protège pas le type de fichier.
    
    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Other file types can be protected when you [change which file types are protected](#change-which-file-types-to-protect) as described in a following section.

Par exemple, après inspection des fichiers portant l’extension .txt, le scanneur ne peut pas appliquer une étiquette configurée pour la classification mais pas pour la protection, car le type de fichier .txt ne prend pas en charge la classification uniquement. If the label is configured for classification and protection, and the .txt file name extension is included for the scanner to protect, the scanner can label the file. 

> [!TIP]
> Pendant ce processus, si le scanneur s’arrête et ne termine pas l’analyse d’un grand nombre de fichiers dans un référentiel :
> 
> - Vous devrez peut-être augmenter le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers. Le renforcement du serveur pour SharePoint peut être l’une des raisons expliquant pourquoi le scanneur dépasse le nombre de connexions réseau autorisées et s’arrête.
>     
>     To check whether this is the cause of the scanner stopping, look to see if the following error message is logged for the scanner in %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (zipped if there are multiple logs): **Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port**
>    
>     Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).
> 
> - Pour les grandes batteries de serveurs SharePoint, vous devrez peut-être augmenter le seuil d’affichage de liste (par défaut, 5 000). For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. Label files that can't be inspected
Pour les types de fichiers qui ne peuvent pas être inspectés, le scanneur applique l’étiquette par défaut dans la stratégie Azure Information Protection ou l’étiquette par défaut que vous configurez pour le scanneur.

Comme dans l’étape précédente, le scanneur ne peut pas étiqueter les fichiers dans les cas suivants :

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- L’étiquette applique la classification et la protection, mais le scanneur ne protège pas le type de fichier.
    
    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Other file types can be protected when you change which file types to protect, as described next.

## <a name="change-which-file-types-to-protect"></a>Change which file types to protect

By default, the scanner protects Office file types and PDF files only. You can change this behavior so that for example, the scanner protects all file types, which is the same protection behavior as the client. Or, the scanner protects additional file types that you specify, in addition to Office file types and PDF files. 

For configuration instructions, see the following sections.

### <a name="scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected"></a>Scanner from the classic client: Use the registry to change which file types are protected

This section applies to the scanner from the classic client only.

To change the default scanner behavior for protecting file types other than Office files and PDFs, you must edit the registry and specify the additional file types that you want to be protected, and the type of protection (native or generic). Pour obtenir des instructions, consultez [Configuration de l’API de fichier](develop/file-api-configuration.md) dans le Guide du développeur. Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ». En outre, spécifiquement pour le scanneur :

- The scanner has its own default behavior: Only Office file formats and PDF documents are protected by default. Si le Registre n’est pas modifié, aucun des autres types de fichiers ne sera étiqueté ou protégé par le scanneur.

- If you want the same default protection behavior as the Azure Information Protection client, where all files are automatically protected with native or generic protection: Specify the `*` wildcard as a registry key, `Encryption` as the value (REG_SZ), and `Default` as the value data.

Lorsque vous modifiez le Registre, créez manuellement la clé **MSIPC** et la clé **FileProtection** si elles n’existent pas, ainsi qu’une clé pour chaque extension de nom de fichier.

Par exemple, pour que le scanneur protège les fichiers TIFF en plus des fichiers Office et PDF, le Registre devrait ressembler à l’image suivante, une fois que vous l’avez modifié. Les fichiers TIFF, qui sont des fichiers image, prennent en charge la protection native et l’extension de nom de fichier résultante est .ptiff.

![Modification du Registre pour que le scanneur applique une protection](./media/editregistry-scanner.png)

For a list of text and images file types that similarly support native protection but must be specified in the registry, see [Supported file types for classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection).

Pour les fichiers ne prenant pas en charge la protection native, indiquez l’extension de nom de fichier comme nouvelle clé et **PFile** pour la protection générique. L’extension de nom de fichier résultante pour le fichier protégé est .pfile.

### <a name="scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected"></a>Scanner from the unified labeling client: Use PowerShell to change which file types are protected

This section applies to the scanner from the unified labeling client only.

For a label policy that applies to the user account downloading labels for the scanner, specify a PowerShell advanced setting named **PFileSupportedExtensions**. 

> [!NOTE]
> For a scanner that has access to the internet, this user account is the account that you specify for the *DelegatedUser* parameter with the Set-AIPAuthentication command.

Example 1:  PowerShell command for the scanner to protect all file types, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Example 2: PowerShell command for the scanner to protect .xml files and .tiff files in addition to Office files and PDF files, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}

For detailed instructions, see [Change which file types to protect](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) from the admin guide.


## <a name="when-files-are-rescanned"></a>Lorsque les fichiers sont réanalysés

Pour le premier cycle d’analyse, le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, il inspecte uniquement les fichiers nouveaux ou modifiés. 

You can force the scanner to inspect all files again from the **Azure Information Protection - Profiles** pane in the Azure portal. Select your scanner profile from the list, and then select the **Rescan all files** option:

![Relancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-rescan-files2.png)

La réinspection de tous les fichiers est utile quand vous voulez que les rapports contiennent tous les fichiers. Ce choix de configuration est généralement utilisé lorsque le scanneur s’exécute en mode découverte. Lorsqu’une analyse complète est terminée, le scanneur passe automatiquement en mode incrémentiel pour inspecter uniquement les fichiers nouveaux ou modifiés lors des analyses suivantes.

In addition, all files are inspected when the scanner from the classic client downloads an Azure Information Protection policy that has new or changed conditions and the scanner from the unified labeling client has new or changed settings for automatic and recommended labeling. 

The scanner refreshes the policy according to the following triggers:

- Scanner from the classic client: Every hour and when the service starts and the policy is older than one hour. 

- Scanner from the unified labeling client: Every four hours. 

> [!TIP]
> If you need to refresh the policy sooner than the default interval, for example, during a testing period: 
>
> - Scanner from the classic client: Manually delete the policy file, **Policy.msip** from **%LocalAppData%\Microsoft\MSIP\Policy.msip**.
>
> - Scanner from the unified labeling client: Manually delete the contents from **%LocalAppData%\Microsoft\MSIP\mip\\<*processname*>\mip**.
>
Ensuite, redémarrez le service du scanneur Azure Information Protection. If you changed protection settings for your labels, also wait 15 minutes from when you saved the protection settings before you restart the service.


## <a name="editing-in-bulk-for-the-data-repository-settings"></a>Modification en bloc des paramètres de référentiel de données

Pour les référentiels de données que vous avez ajoutés à un profil de scanneur, vous pouvez utiliser les options **Exporter** et **Importer** pour modifier rapidement les paramètres. Par exemple, pour vos référentiels de données SharePoint, vous souhaitez ajouter un nouveau type de fichier à exclure de l’analyse.

Instead of editing each data repository in the Azure portal, use the **Export** option from the **Repositories** pane:

![Exportation de paramètres de référentiel de données pour le scanneur](./media/export-scanner-repositories.png)

Manually edit the file to make the change, and then use the **Import** option on the same pane.

## <a name="using-the-scanner-with-alternative-configurations"></a>Utilisation du scanneur avec d’autres configurations

There are three alternative scenarios that the Azure Information Protection scanner supports where labels do not need to be configured for any conditions: 

- Appliquer une étiquette par défaut à tous les fichiers dans un référentiel de données.
    
    For this configuration, set **Label files based on content** to **Off**. Then set the **Default label** to **Custom**, and select the label to use.
    
    The contents of the files are not inspected and all unlabeled files in the data repository are labeled according to the default label that you specify for the data repository or the scanner profile. 
    
    For the scanner from the unified labeling client, you can also select **Enforce default label** if you want the default label to be applied on all files, even if they are already labeled.
    

- Remove existing labels from all files in a data repository.
    
    Applicable to the scanner from the unified labeling client only, this configuration lets you remove existing labels, which includes protection if it was applied with that label. Protection that was applied independently from a label is retained. Use this configuration if you need to remove all labels from files in a repository.
    
    Configurez les paramètres suivants :
    - **Label files based on content**: **Off**
    - **Default label**: **None**
    - **Relabel files**: **On** with the **Enforce default label** checkbox selected

- Identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.
    
    Pour cette configuration, définissez les **Info types to be discovered** (Types d’infos à découvrir) sur **Tous**.
    
    For the scanner from the classic client: The scanner uses any custom conditions that you have specified for labels in the Azure Information Protection policy, and the list of information types that are available to specify for labels in the Azure Information Protection policy. 
    
    For the scanner from the unified labeling client: The scanner uses any custom sensitive info types that you have specified and the list of built-in sensitive info types that are available to select in your labeling management center.
    
    Ce paramètre vous permet de retrouver des informations sensibles que vous ne pensiez peut-être pas avoir, mais au détriment des taux d’analyse du scanneur.
    
    The following quickstart for the scanner uses this configuration: [Quickstart: Find what sensitive information you have](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Optimisation des performances du scanneur

Utilisez les instructions suivantes pour vous aider à optimiser les performances du scanneur. However, if your priority is the responsiveness of the scanner computer rather than the scanner performance, you can use an advanced client setting to limit the number of threads used by the scanner:

- Scanner from the classic client: [Limit the number of threads used by the scanner](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)

- Scanner from the unified labeling client: [Limit the number of threads used by the scanner](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)

Pour optimiser les performances de l’analyseur :

- **Veillez à avoir une connexion haut débit fiable entre l’ordinateur de l’analyseur et le magasin de données analysé**
    
    Par exemple, placez l’ordinateur de l’analyseur dans le même réseau local ou (de préférence) dans le même segment réseau que le magasin de données analysé.
    
    La qualité de la connexion réseau affecte les performances de l’analyseur parce que pour examiner les fichiers, celui-ci transfère le contenu des fichiers à l’ordinateur exécutant son service. Quand vous réduisez (ou supprimez) le nombre de tronçons réseau que ces données doivent traverser, vous réduisez également la charge sur votre réseau. 

- **Assurez-vous que l’ordinateur de l’analyseur dispose de ressources processeur**
    
    L’inspection du contenu des fichiers ainsi que le chiffrement et le déchiffrement des fichiers sont des actions qui sollicitent le processeur de manière intense. Surveillez les cycles d’analyse standard de vos magasins de données spécifiés pour déterminer si un manque de ressources processeur affecte les performances de l’analyseur.
    
- **N’analysez pas les dossiers locaux sur l’ordinateur exécutant le service de l’analyseur**
    
    Si vous avez des dossiers à analyser sur un serveur Windows, installez l’analyseur sur un autre ordinateur et configurez ces dossiers comme partages réseau à analyser. En séparant les deux fonctions d’hébergement des fichiers et d’analyse des fichiers, les ressources informatiques de ces services n’entrent pas en concurrence.

Si nécessaire, installez plusieurs instances du scanneur. Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance SQL Server lorsque vous spécifiez un nom de profil personnalisé pour le scanneur. For the scanner from the unified labeling client, multiple scanners can share the same profile, which results in quicker scanning times.

Autres facteurs qui affectent les performances de l’analyseur :

- La charge actuelle et les temps de réponse des magasins de données qui contiennent les fichiers à analyser

- Si l’analyseur s’exécute en mode découverte ou en mode d’application
    
    Le mode découverte a généralement un taux d’analyse plus élevé que le mode d’application, car la découverte nécessite une seule action de lecture de fichier tandis que le mode d’application nécessite des actions de lecture et d’écriture.

- You change the conditions in the Azure Information Protection policy (classic client) or auto-labeling in the label policy (unified labeling client)
    
    Votre premier cycle d’analyse lorsque le scanneur doit inspecter chaque fichier prend plus temps que les cycles d’analyse suivants qui, par défaut, inspectent uniquement les fichiers nouveaux et modifiés. However, if you change the conditions or auto-labeling settings, all files are scanned again, as described in the [preceding section](#when-files-are-rescanned).

- La construction d’expressions regex pour des conditions personnalisées
    
    Pour éviter une consommation de mémoire importante et le risque de dépassements du délai d’expiration (15 minutes par fichier), passez en revue vos expressions regex pour vérifier que la correspondance des modèles est efficace. Exemple :
    
    - Évitez les [quantificateurs gourmands](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - Utilisez des groupes sans capture comme `(?:expression)` au lieu de `(expression)`

- Le niveau de journalisation que vous avez choisi
    
    Vous pouvez choisir entre **Déboguer**, **Information**, **Erreur** et **Désactivé** pour les rapports de l’analyseur. Avec **Désactivé**, vous bénéficiez des meilleures performances alors qu’avec **Déboguer**, l’analyseur est considérablement ralenti et doit être utilisé uniquement pour le dépannage. Pour plus d’informations, consultez le paramètre *ReportLevel* de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- Les fichiers eux-mêmes :
    
    - With the exception of Excel files, Office files are more quickly scanned than PDF files.
    
    - Les fichiers non protégés sont plus rapides à analyser que les fichiers protégés.
    
    - Les gros fichiers prennent évidemment plus de temps à analyser que les petits fichiers.

- En outre :
    
    - Confirm that the service account that runs the scanner has only the rights documented in the [scanner prerequisites](#prerequisites-for-the-azure-information-protection-scanner) section, and then configure the [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) to disable the low integrity level for the scanner (classic client only).
    
    - Le scanneur s’exécute plus rapidement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour appliquer une étiquette par défaut à tous les fichiers, car le scanneur n’inspecte pas le contenu du fichier.
    
    - Le scanneur s’exécute plus lentement lorsque la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) est utilisée pour identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.
    
    - You can decrease the scanner timeouts (classic client only) with [advanced client settings](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) for better scanning rates and lower memory consumption, but with the acknowledgment that some files might be skipped.

## <a name="list-of-cmdlets-for-the-scanner"></a>Liste des cmdlets pour le scanneur

Étant donné que vous configurez maintenant le scanneur à partir du portail Azure, les cmdlets de versions précédentes qui configuraient des référentiels de données et la liste de types de fichiers analysés sont désormais déconseillées. 

Les cmdlets conservées incluent des cmdlets qui installent et mettent à niveau le scanneur, modifient la base de données de configuration du scanneur et le profil, modifient le niveau de rapport local et importent des paramètres de configuration pour un ordinateur déconnecté. 

The full list of cmdlets for the scanner: 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs) - unified labeling client only

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>ID du journal des événements et descriptions pour le scanneur

Utilisez les sections suivantes pour identifier les ID d’événement possibles et les descriptions du scanneur. Ces événements sont journalisés sur le serveur qui exécute le service de scanneur, dans le journal des événements **Applications et services** Windows, **Azure Information Protection**.

> [!NOTE]
> This section applies to the scanner from the classic client only. Currently, the scanner from the unified labeling client doesn't write information to the event log.

-----

Informations **910**

**Cycle du scanneur démarré.**

Cet événement est enregistré lorsque le service du scanneur est démarré et qu’il commence à analyser les fichiers inclus dans les dépôts de données que vous avez spécifiés.

----

Informations **911**

**Cycle du scanneur terminé.**

Cet événement est journalisé quand le scanneur termine une analyse manuelle ou un cycle dans le cadre d’une planification continue.

Si le scanneur a été configuré pour s’exécuter manuellement plutôt que de manière continue, pour relancer l’analyse des fichiers, définissez la **Planification** sur **Manuel** ou **Toujours** dans le profil du scanneur, puis redémarrez le service.

----

## <a name="next-steps"></a>Étapes suivantes

Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

Vous vous demandez peut-être : [Quelle différence y a-t-il entre l’ICF de Windows Server et le scanneur d’Azure Information Protection ?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. For more information about this and other scenarios that use PowerShell, see the following sections from the admin guides:

- For the classic client: [Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)

- For the unified labeling client: [Using PowerShell with the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-powershell.md)
