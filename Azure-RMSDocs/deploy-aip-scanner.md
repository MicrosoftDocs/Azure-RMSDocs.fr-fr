---
title: Déployer le scanneur Azure Information Protection-AIP
description: Instructions d’installation, de configuration et d’exécution de la version actuelle de l’analyseur de Azure Information Protection pour détecter, classer et protéger des fichiers dans des magasins de données.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c1efdbcf7d6738b5dd1d0cfb6b5d4495cec60f4b
ms.sourcegitcommit: 307258ff0a8a7a3f607c8f47f38a9801d0e06ba1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2020
ms.locfileid: "85126711"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows server 2012 R2*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

> [!NOTE]
> Cet article est destiné à la version actuelle de la disponibilité générale du scanneur de Azure Information Protection avec le client Azure Information Protection (Classic) et à la version de disponibilité générale du client d’étiquetage unifié Azure Information Protection.
> 
> Si vous avez déjà installé le scanneur et que vous souhaitez le mettre à niveau, utilisez les instructions de mise à niveau suivantes, puis suivez les instructions de cette page, en omettant l’étape d’installation du scanneur :
> - Pour le client classique : [mise à niveau du scanneur Azure information protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> - Pour le client d’étiquetage unifié : [mise à niveau du scanneur de Azure information protection](./rms-client/clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> 
> Si vous disposez d’une version du scanneur antérieure à 1.48.204.0 et que vous n’êtes pas prêt à effectuer la mise à niveau, consultez [déploiement de versions antérieures du moteur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner-previousversions.md).


Utilisez ces informations pour en savoir plus sur le scanneur Azure Information Protection, puis sur la façon d’installer, de configurer, d’exécuter et, le cas échéant, de le résoudre.

Ce scanneur s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les magasins de données suivants :

- Dossiers locaux sur l’ordinateur Windows Server qui exécute le scanneur.

- Chemins UNC pour les partages réseau qui utilisent le protocole SMB (Server Message Block).

- Bibliothèques de documents et dossiers pour SharePoint Server 2019 via SharePoint Server 2013. SharePoint 2010 est également pris en charge pour les clients disposant de la [prise en charge étendue de cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Pour analyser et étiqueter des fichiers sur des référentiels cloud, utilisez [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) au lieu du scanneur.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Présentation du scanneur Azure Information Protection

Lorsque vous avez configuré des étiquettes qui appliquent une classification automatique, les fichiers détectés par ce scanneur peuvent être étiquetés. Les étiquettes appliquent une classification et elles appliquent ou suppriment éventuellement la protection :

![Présentation de l’architecture du scanneur Azure Information Protection](./media/infoprotect-scanner.png)

Le scanneur peut inspecter tous les fichiers que Windows est capable d’indexer à l’aide de filtres IFilter installés sur l’ordinateur. Ensuite, pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise la détection de modèles et les types d’informations sensibles de protection contre la perte de données intégrée à Office 365 ou les modèles regex Office 365. Étant donné que le scanneur utilise le client Azure Information Protection (le client classique ou le client d’étiquetage unifié), le scanneur peut classifier et protéger les mêmes types de fichiers :

- Client classique : [types de fichiers pris en charge par le client Azure information protection](./rms-client/client-admin-guide-file-types.md)

- Client d’étiquetage unifié : [types de fichiers pris en charge par le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-file-types.md)

Vous pouvez exécuter le scanneur en mode découverte uniquement, dans lequel vous utilisez les rapports pour vérifier ce qui se passerait si les fichiers étaient étiquetés. Ou bien, vous pouvez exécuter le scanneur pour appliquer automatiquement les étiquettes. Vous pouvez également exécuter le scanneur pour découvrir les fichiers contenant des types d’informations sensibles, sans configurer d’étiquettes pour les conditions qui appliquent la classification automatique.

Notez que le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers dans les magasins de données que vous spécifiez. Vous pouvez configurer ce cycle pour s’exécuter une ou plusieurs fois.

Vous pouvez spécifier les types de fichiers à analyser, ou à exclure de l’analyse, en définissant une liste de types de fichiers dans le cadre de la configuration du scanneur.


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prérequis pour le scanneur Azure Information Protection
Avant d’installer le scanneur Azure Information Protection, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Informations complémentaires|
|---------------|--------------------|
|Ordinateur Windows Server pour exécuter le service du scanneur :<br /><br />- Processeurs 4 cœurs<br /><br />- 8 Go de RAM<br /><br />- 10 Go d’espace libre (en moyenne) pour les fichiers temporaires|Windows Server 2019, Windows Server 2016 ou Windows Server 2012 R2. <br /><br />Remarque : À des fins de test ou d’évaluation dans un environnement hors production, vous pouvez utiliser un système d’exploitation client Windows qui est [pris en charge par le client Azure Information Protection](requirements.md#client-devices).<br /><br />Il peut s’agir d’un ordinateur physique ou virtuel doté d’une connexion réseau rapide et fiable aux magasins de données à scanner.<br /><br /> Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo. <br /><br /> Si la connexion Internet n’est pas possible en raison des stratégies de votre organisation, consultez la section [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations) . Dans le cas contraire, assurez-vous que cet ordinateur dispose d’une connectivité Internet qui autorise les URL suivantes sur HTTPs (port 443) :<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com <br /> \*. protection.outlook.com (scanneur du client d’étiquetage unifié uniquement)|
|Compte de service pour exécuter le service du scanneur|En plus d’exécuter le service du scanneur sur l’ordinateur Windows Server, ce compte Windows s’authentifie auprès d’Azure AD, puis télécharge la stratégie Azure Information Protection. Ce compte doit être un compte Active Directory et synchronisé avec Azure AD. Si vous ne pouvez pas synchroniser ce compte en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />Ce compte de service a la configuration suivante :<br /><br />- **Ouvrir une session localement**, attribution des droits utilisateur. Ce droit est exigé pour l’installation et la configuration du scanneur, mais pas pour son fonctionnement. Vous devez accorder ce droit au compte de service, mais vous pouvez le supprimer après avoir vérifié que le scanneur peut détecter, classifier et protéger des fichiers. Si l’attribution de ce droit, même pendant une courte période, n’est pas possible en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />- **Ouvrir une session en tant que service**, attribution des droits utilisateur. Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur. <br /><br />- Autorisations sur les référentiels de données : <br /><br /> Partages de fichiers ou fichiers locaux : vous devez accorder les autorisations **lecture** et **écriture** et **modification** pour analyser les fichiers, puis appliquer la classification et la protection aux fichiers qui remplissent les conditions de la stratégie de Azure information protection. <br /><br /> SharePoint : vous devez accorder des autorisations **contrôle total** pour analyser les fichiers, puis appliquer la classification et la protection aux fichiers qui remplissent les conditions de la stratégie de Azure information protection. <br /><br /> Pour exécuter le scanneur en mode découverte uniquement, l’autorisation **Lecture** suffit.<br /><br />-Pour les étiquettes qui reprotègent ou suppriment la protection : pour s’assurer que le scanneur ait toujours accès aux fichiers protégés, définissez ce compte comme [super utilisateur](configure-super-users.md) pour Azure information protection et assurez-vous que la fonctionnalité de super utilisateur est activée. En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que ce compte est inclus dans les contrôles d’intégration que vous avez configurés.|
|SQL Server pour stocker la configuration du scanneur :<br /><br />- Instance locale ou distante<br /><br />- [Classement non sensible à la casse](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />Rôle sysadmin pour installer le scanneur|SQL Server 2012 est la version minimale pour les éditions suivantes :<br /><br />- SQL Server Entreprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance de SQL Server lorsque vous spécifiez un nom de cluster personnalisé (profil) pour le scanneur. Lorsque vous utilisez la version préliminaire du scanneur à partir du client d’étiquetage unifié, plusieurs analyseurs peuvent partager la même base de données de configuration.<br /><br />Lorsque vous installez le scanneur et si votre compte a le rôle Sysadmin, le processus d’installation crée automatiquement la base de données de configuration du scanneur et accorde le rôle db_owner requis au compte de service qui exécute le scanneur. Si vous ne pouvez pas disposer du rôle Sysadmin ou si les stratégies de votre organisation requièrent que les bases de données soient créées et configurées manuellement, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />Pour obtenir des conseils sur la capacité, consultez [exigences de stockage et planification de la capacité pour SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).|
|L’un des Azure Information Protection clients suivants est installé sur l’ordinateur Windows Server <br /><br /> -Client classique <br /><br /> -Client d’étiquetage unifié ([version de disponibilité générale actuelle uniquement](./rms-client/unifiedlabelingclient-version-release-history.md#version-25330)) |Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.<br /><br />Pour obtenir des instructions d’installation et de mise à niveau : <br /> - [Client classique](./rms-client/client-admin-guide.md)<br /> - [Client d’étiquetage unifié](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner) |
|Étiquettes configurées qui appliquent une classification automatique et éventuellement une protection|Pour obtenir des instructions pour le client classique afin de configurer une étiquette pour les conditions et pour appliquer la protection :<br /> - [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)<br /> - [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md) <br /><br />Conseil : vous pouvez utiliser les instructions du [didacticiel](infoprotect-quick-start-tutorial.md) pour tester le scanneur avec une étiquette qui recherche des numéros de carte de crédit dans un document Word préparé. Toutefois, vous devez modifier la configuration de l’étiquette pour que l’option **Sélectionner la manière dont cette étiquette est appliquée** soit définie sur **automatique**, plutôt que sur **recommandé** ou **traiter l’étiquetage recommandé comme automatique** (disponible dans la version 2.7 du scanneur. x. x et versions ultérieures). Supprimez ensuite l’étiquette du document (si elle est appliquée), puis copiez le fichier dans un référentiel de données pour le scanneur. Pour effectuer un test rapide, il peut s’agir d’un dossier local sur l’ordinateur du scanneur.<br /><br /> Pour obtenir des instructions pour le client d’étiquetage unifié afin de configurer une étiquette pour l’étiquetage automatique et appliquer la protection :<br /> - [Appliquer automatiquement une étiquette de sensibilité au contenu](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)<br /> - [Restreindre l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)<br /><br /> Bien que vous puissiez exécuter le scanneur même si vous n’avez pas configuré les étiquettes qui appliquent la classification automatique, ce scénario n’est pas abordé dans ces instructions. [Plus d’informations](#using-the-scanner-with-alternative-configurations)|
|Pour les bibliothèques de documents et les dossiers SharePoint à analyser :<br /><br />-SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|D’autres versions de SharePoint ne sont pas prises en charge pour le scanneur.<br /><br />Lorsque vous utilisez le contrôle de [version](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), le scanneur inspecte et étiquette la dernière version publiée. Si le scanneur étiquette une approbation de fichier et de [contenu](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) est requise, ce fichier doit être approuvé pour être disponible pour les utilisateurs. <br /><br />Pour les grandes batteries de serveurs SharePoint, regardez si vous devez augmenter le seuil d’affichage de liste (par défaut, 5 000) pour le scanneur pour accéder à tous les fichiers. Pour plus d’informations, consultez la documentation SharePoint suivante : [gérer les grandes listes et les bibliothèques dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Pour scanner des documents Office :<br /><br />- formats de fichier 97-2003 et formats Office Open XML pour Word, Excel et PowerPoint|Pour plus d’informations sur les types de fichiers pris en charge par le scanneur pour ces formats de fichier, consultez les informations suivantes : <br />-Client classique : [types de fichiers pris en charge par le client Azure information protection](./rms-client/client-admin-guide-file-types.md)<br />-Client d’étiquetage unifié : [types de fichiers pris en charge par le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-file-types.md)|
|Pour les chemins longs :<br /><br />- 260 caractères maximum, sauf si le scanneur est installé sur Windows 2016 et que l’ordinateur est configuré pour prendre en charge les chemins longs.|Windows 10 et Windows Server 2016 prennent en charge des longueurs de chemin de plus de 260 caractères avec le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)suivant : stratégie de l' **ordinateur local**  >  **Configuration ordinateur**  >  **modèles d’administration**  >  **tous les paramètres**  >  **activer les chemins longs Win32**<br /><br /> Pour plus d’informations sur la prise en charge des chemins de fichiers longs, consultez la section consacrée à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.|
|Statistiques d’utilisation|Veillez à désactiver l’option d’envoi des statistiques d’utilisation à Microsoft en affectant la valeur 0 au paramètre [AllowTelemetry](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-install#to-install-the-azure-information-protection-client-by-using-the-executable-installer) , ou assurez-vous que l’option **aider à améliorer Azure information protection en envoyant des statistiques d’utilisation à Microsoft** reste désélectionnée pendant le processus d’installation de l’analyseur.| 

Si vous ne pouvez pas satisfaire à toutes les exigences du tableau parce qu’elles sont interdites par les stratégies de votre organisation, consultez la section [autres configurations](#deploying-the-scanner-with-alternative-configurations) .

Lorsque vous déployez le scanneur en production ou que vous testez les performances de plusieurs scanneurs, consultez la section suivante pour obtenir des conseils sur la planification de la capacité pour SQL Server.

Toutefois, si vous êtes prêt à commencer le déploiement du scanneur, accédez directement à [la section Configuration du scanneur](#configure-the-scanner-in-the-azure-portal).

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Exigences de stockage et planification de la capacité pour SQL Server

La quantité d’espace disque requise pour la base de données de configuration du scanneur et la spécification de l’ordinateur qui exécute SQL Server peuvent varier pour chaque environnement, nous vous encourageons donc à effectuer vos propres tests. Toutefois, vous pouvez utiliser les instructions suivantes comme point de départ.

Pour plus d’informations, consultez la section [optimisation des performances de l’analyseur](#optimizing-the-performance-of-the-scanner) .

##### <a name="scanner-from-the-classic-client"></a>Analyseur du client classique :

- **Taille du disque**: la taille de la base de données de configuration varie pour chaque déploiement, mais nous vous recommandons d’allouer 500 Mo pour chaque 1 million fichiers que vous souhaitez analyser.

- **Pour chaque scanneur**: 4 processeurs principaux ; 8 Go de RAM recommandés (4 Go minimum).

##### <a name="scanner-from-the-unified-labeling-client"></a>Analyseur du client d’étiquetage unifié :

- **Taille du disque**: bien que la taille de la base de données de configuration du scanneur varie pour chaque déploiement, vous pouvez utiliser l’équation suivante comme aide : `100 KB + <file count> *(1000 + 4*<average file name length>)` . 
    
    Par exemple, pour analyser les fichiers 1 million dont la longueur moyenne du nom de fichier est de 250 octets, allouez 2 Go d’espace disque.

- **Pour plusieurs scanneurs, jusqu’à 10**processeurs principaux ; 8 Go de RAM recommandés.

- **Pour plusieurs scanneurs de plus de 10 (maximum 40)**: 8 processus principaux ; 16 Go de RAM recommandés.

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Déploiement du scanneur avec d’autres configurations

Les prérequis répertoriés dans la table correspondent aux exigences par défaut pour le scanneur et sont recommandés pour obtenir la configuration la plus simple pour le déploiement du scanneur. Ils doivent être adaptés aux tests initiaux, afin que vous puissiez vérifier les fonctionnalités du scanneur. Toutefois, dans un environnement de produit, les stratégies de votre organisation peuvent interdire ces exigences par défaut en raison d’une ou plusieurs des restrictions suivantes :

- Les serveurs ne sont pas autorisés à se connecter à Internet

- Sysadmin ne peut pas vous être accordé ou vous devez créer des bases de données et les configurer manuellement

- Les comptes de service ne peuvent pas se voir accorder le droit **ouvrir une session localement**

- Les comptes de service ne peuvent pas être synchronisés avec Azure Active Directory mais les serveurs ont une connectivité Internet

Le scanneur peut prendre en charge ces restrictions, mais celles-ci nécessitent une configuration supplémentaire.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction : le serveur de scanneur ne peut pas disposer d’une connexion Internet

Suivez les instructions des guides d’administration pour prendre en charge un ordinateur déconnecté :

- Pour le client classique : [prise en charge des ordinateurs déconnectés](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)
    
    Dans cette configuration, le scanneur du client classique ne peut pas appliquer la protection, supprimer la protection ou inspecter les fichiers protégés à l’aide de la clé Cloud de votre organisation. Au lieu de cela, le scanneur est limité à l’utilisation d’étiquettes qui appliquent uniquement la classification, ou appliquez la protection qui utilise [hyok](configure-adrms-restrictions.md)

- Pour le client d’étiquetage unifié : le client d’étiquetage unifié ne peut pas appliquer la protection sans connexion en ligne. 
    
    Le scanneur du client d’étiquetage unifié peut appliquer des étiquettes basées sur les stratégies importées à l’aide de l’applet [de commande Import-AIPScannerConfiguration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration?view=azureipps) .

Effectuez ensuite les opérations suivantes :

1. Configurez le scanneur dans le Portail Azure en créant un cluster de scanneur. Si vous avez besoin d’aide pour cette étape, consultez [Configurer le scanneur dans le portail Azure](#configure-the-scanner-in-the-azure-portal).

2. Exportez votre travail de contenu à partir du volet **Azure information protection-travaux d’analyse de contenu** , à l’aide de l’option d' **exportation** .

3. Pour finir, dans une session PowerShell, exécutez [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) et spécifiez le fichier qui contient les paramètres exportés.

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

Si le rôle Sysadmin peut vous être attribué temporairement pour installer le scanneur, vous pouvez supprimer ce rôle lorsque l’installation du scanneur est terminée. Lorsque vous utilisez cette configuration, la base de données est automatiquement créée pour vous et le compte de service du scanneur obtient automatiquement les autorisations nécessaires. Toutefois, le compte d’utilisateur qui configure le scanneur nécessite le rôle db_owner pour la base de données de configuration du scanneur, et vous devez attribuer manuellement ce rôle au compte d’utilisateur.

Si vous ne pouvez pas recevoir le rôle sysadmin même temporairement, vous devez demander à un utilisateur disposant des droits d’administrateur système de créer manuellement une base de données avant d’installer le scanneur. Pour cette configuration, les rôles suivants doivent être attribués : 
    
|Compte|Rôle au niveau de la base de données|
|--------------------------------|---------------------|
|Compte de service pour le scanneur|db_owner|
|Compte utilisateur pour l’installation du scanneur|db_owner|
|Compte utilisateur pour la configuration du scanneur |db_owner|

En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Mais si vous utilisez des comptes différents, ils ont tous les deux besoin du rôle db_owner pour la base de données de configuration du scanneur :

- Pour le client classique :

    Si vous ne spécifiez pas votre propre nom de cluster (profil) pour le scanneur, la base de données de configuration est nommée **AIPScanner_ \<computer_name> **(client classique uniquement). Passez à l’étape suivante pour créer un utilisateur et accorder des droits de db_owner sur la base de données. 

- Pour le client d’étiquetage unifié :
    
    Si vous spécifiez votre propre nom de cluster (profil), la base de données de configuration est nommée **AIPScannerUL_<cluster_name>** (client d’étiquetage unifié).
    
    Remplissez la base de données à l’aide du script suivant : 

    s’il n’existe pas (Select * from master.sys. server_principals où sid = SUSER_SID ('domaine\utilisateur')) BEGIN DECLARE @T nvarchar (500) Set @T = 'Create login' + QUOTENAME ('domaine\utilisateur') + 'de Windows’exec ( @T ) End 

Pour créer un utilisateur et accorder des droits de db_owner sur cette base de données, demandez à l’administrateur système d’effectuer les opérations suivantes :

1. Créer une base de connaissances pour le scanneur : <br>
    **Create database AIPScannerUL_ [ClusterName]** **ALTER DATABASE AIPScannerUL_ [ClusterName] Set Trustworthy on**
    - Cette étape est facultative, mais elle permet la résolution des problèmes plus facilement si nécessaire.

2. Accordez des droits à l’utilisateur qui exécute la commande d’installation et qui est utilisé pour exécuter les commandes de gestion du scanneur :

Script SQL :

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END

3. Accorder des droits au compte de service du scanneur :

Script SQL :

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    
De plus :

- Vous devez être un administrateur local sur le serveur qui exécutera le scanneur.
- Le compte de service qui exécutera le scanneur doit disposer des autorisations contrôle total sur les clés de Registre suivantes :
    
    - HKEY_LOCAL_MACHINE \SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\MSIPC\Server

Si, après avoir configuré ces autorisations, vous voyez une erreur lors de l’installation du scanneur, l’erreur peut être ignorée et vous pouvez démarrer manuellement le service du scanneur.


#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restriction : le compte de service pour le scanneur ne peut pas obtenir le droit **Ouvrir une session localement**

Si les stratégies de votre organisation interdisent le droit **ouvrir une session localement** pour les comptes de service, mais autorisent le droit **ouvrir une session en tant que tâche** , suivez les instructions ci-dessous :

- Pour le client classique : consultez [spécifier et utiliser le paramètre Token pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) à partir du Guide de l’administrateur du client.

- Pour le client d’étiquetage unifié : utilisez le paramètre *OnBehalfOf* avec set-AIPAuthentication, comme décrit dans [Comment étiqueter des fichiers de manière non interactive pour Azure information protection dans le](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) Guide d’administration de ce client.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory mais le serveur dispose d’une connexion Internet

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- Pour le compte de service du scanneur, vous pouvez utiliser un compte Windows local ou un compte Active Directory.

- Pour le compte Azure Active Directory, suivez les instructions ci-dessous :
    - Pour le client classique : consultez [spécifier et utiliser le paramètre Token pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) à partir du Guide de l’administrateur du client.
    - Pour le client d’étiquetage unifié : spécifiez votre compte local pour le paramètre *OnBehalfOf* avec set-AIPAuthentication, comme décrit dans [Comment étiqueter des fichiers de manière non interactive pour Azure information protection dans le](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) Guide d’administration de ce client.


## <a name="configure-the-scanner-in-the-azure-portal"></a>Configurer le scanneur dans le portail Azure

Avant d’installer le scanneur ou de le mettre à niveau à partir d’une ancienne version de disponibilité générale du scanneur, créez un travail de cluster et d’analyse de contenu pour le scanneur dans le Portail Azure. Vous configurez le travail de cluster et d’analyse de contenu pour les paramètres du scanneur et les référentiels de données à analyser.

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche pour ressources, services et docs : commencez à taper les **informations** et sélectionnez **Azure information protection**.
    
2. Recherchez les options du menu **scanner** , puis sélectionnez **clusters**.

3. Dans le volet **Azure information protection-clusters** , sélectionnez **Ajouter**:
    
    ![Ajouter un travail d’analyse de contenu pour le scanneur de Azure Information Protection](./media/scanner-add-profile.png)

4. Dans le volet **Ajouter un nouveau cluster** , spécifiez un nom pour le scanneur utilisé pour identifier les paramètres de configuration et les référentiels de données à analyser. Par exemple, vous pouvez spécifier **Europe** pour identifier l’emplacement géographique des référentiels de données couverts par votre scanneur. Lorsque vous installez ou mettez à niveau ultérieurement le scanneur, vous devez spécifier le même nom de cluster.
   
    
    Si vous le souhaitez, spécifiez une description à des fins administratives pour vous aider à identifier le nom du cluster du scanneur.

    Sélectionnez **Enregistrer**.
5. Recherchez les options du menu **scanner** , puis sélectionnez **travaux d’analyse du contenu**.
6. Dans le volet **Azure information protection-travaux d’analyse de contenu** , sélectionnez **Ajouter**.
 
7. Pour cette configuration initiale, configurez les paramètres suivants, puis sélectionnez **Enregistrer** sans fermer le volet :
    
    Pour la section **paramètres du travail d’analyse du contenu** :
    - **Planifier**: conserver la valeur par défaut **manuelle**
    - **Types d’informations à découvrir**: changer en **stratégie uniquement**
    - **Configurer les référentiels**: ne pas configurer pour l’instant, car le travail d’analyse de contenu doit d’abord être enregistré.
    
    Pour la section application de la **stratégie** :
    - **Appliquer**: sélectionner **désactivé**
    - **Étiqueter les fichiers en fonction du contenu**: conservez la valeur par défaut **activée**
    - **Étiquette par**défaut : conserver la valeur par défaut de la **stratégie** par défaut
    - **Réétiqueter les fichiers**: conserver la valeur par défaut **désactivé**
    
    Pour la section **configurer les paramètres du fichier** :
    - **Conserver les valeurs « date de modification », « dernière modification » et « modifié par »**: conserver la valeur par défaut **activée**
    - **Types de fichiers à analyser**: conserver les types de fichiers par défaut pour l' **exclusion**
    - **Propriétaire par défaut**: conserver la valeur par défaut du **compte de scanneur**

8. Maintenant que le travail d’analyse de contenu est créé et enregistré, vous êtes prêt à revenir à l’option **configurer les référentiels** pour spécifier les magasins de données à analyser. Vous pouvez spécifier les dossiers locaux, les chemins d’accès UNC et les URL du serveur SharePoint pour les dossiers et bibliothèques de documents locaux SharePoint. 
    
    SharePoint Server 2019, SharePoint Server 2016 et SharePoint Server 2013 sont pris en charge pour SharePoint. SharePoint Server 2010 est également pris en charge lorsque vous bénéficiez d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
    Pour ajouter votre premier magasin de données, dans le volet **Ajouter un nouveau travail d’analyse de contenu** , sélectionnez configurer les **référentiels** pour ouvrir le volet **dépôts** :
    
    ![Configurer des référentiels de données pour le scanneur Azure Information Protection](./media/scanner-repositories-bar.png)

9. Dans le volet **Référentiels**, sélectionnez **Ajouter** :
    
    ![Ajouter un référentiel de données pour le scanneur Azure Information Protection](./media/scanner-repository-add.png)

10. Dans le volet **référentiel** , spécifiez le chemin d’accès du référentiel de données. 
    
    Les caractères génériques ne sont pas pris en charge, ni les emplacements WebDav.
    
    Exemples :
      
    - Pour un partage réseau : `\\Server\Folder`
    
    - Pour une bibliothèque SharePoint : `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > Si vous ajoutez un chemin d’accès SharePoint pour « Documents partagés » :
    >
     >- Spécifiez **Documents partagés** dans le chemin d’accès lorsque vous souhaitez analyser tous les documents et tous les dossiers de Documents partagés. Par exemple : `http://sp2013/Shared Documents`
     >
     >- Spécifiez **Documents** dans le chemin d’accès lorsque vous souhaitez analyser tous les documents et tous les dossiers d’un sous-dossier sous Documents partagés. Par exemple : `http://sp2013/Documents/Sales Reports`
    
    Pour les autres paramètres de ce volet, ne les modifiez pas pour cette configuration initiale, mais conservez-les en tant que **travail d’analyse du contenu par défaut**. Cela signifie que le référentiel de données hérite des paramètres du travail d’analyse de contenu. 
    
    Sélectionnez **Enregistrer**.

> [!IMPORTANT]
> Si le système de fichiers local peut être analysé, cette configuration n’est pas recommandée pour les déploiements de production et ne peut être utilisée **que** dans les clusters à nœud unique. L’analyse des dossiers locaux par les clusters à plusieurs nœuds n’est pas prise en charge. Si vous devez analyser un dossier sur le système de fichiers local, nous vous recommandons de créer un partage et de l’analyser à l’aide d’une URL réseau.

10. Si vous souhaitez ajouter un autre référentiel de données, répétez les étapes 8 et 9. 

11. Vous pouvez maintenant fermer le volet **référentiels** et le volet **travail analyse du contenu** . De retour dans le volet du **travail analyse du contenu Azure information protection** , le nom de votre analyse de contenu s’affiche, ainsi que la colonne **planification** qui indique **Manuel** et la colonne **appliquer** est vide.

Vous êtes maintenant prêt à installer le scanneur avec la tâche d’analyse de contenu que vous venez de créer.

## <a name="install-the-scanner"></a>Installer le scanneur

1. Connectez-vous à l’ordinateur Windows Server qui exécutera le scanneur. Utilisez un compte disposant de droits d’administrateur local et qui est autorisé à écrire dans la base de données principale SQL Server.

2. Ouvrez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Exécutez l’applet de commande [install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) , en spécifiant votre SQL Server instance sur laquelle créer une base de données pour le scanneur de Azure information protection, et le nom du cluster du scanneur que vous avez spécifié dans la section précédente : 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```
    
    Exemples utilisant le nom de profil **Europe** :
    
    - Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    Lorsque vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur ( \<domain\user name> ) et du mot de passe.

4. Vérifiez que le service est maintenant installé à l’aide des **Outils d’administration**  >  **services**. 
    
    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie afin de pouvoir exécuter le scanneur sans assistance. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Obtenir un jeton Azure AD pour le scanneur

Le jeton Azure AD permet au scanneur de s’authentifier auprès du service Azure Information Protection.

1. Revenez à la Portail Azure pour créer deux applications Azure AD (une seule Azure AD application pour le scanneur à partir du client d’étiquetage unifié) qui sont nécessaires pour spécifier un jeton d’accès pour l’authentification. Ce jeton permet au scanneur de s’exécuter de manière non interactive.
    
    Pour créer ces applications, suivez les instructions des guides d’administration pour les clients concernés :
    
    - Pour le client classique : [Comment étiqueter des fichiers de manière non interactive pour Azure information protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)
    
    - Pour le client d’étiquetage unifié : [Comment étiqueter des fichiers de manière non interactive pour Azure information protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

2. À partir de l’ordinateur Windows Server, si votre compte de service de scanneur a reçu l’autorisation **Ouvrir une session localement** pour l’installation : connectez-vous avec ce compte et démarrez une session PowerShell. Exécutez [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), en spécifiant les valeurs copiées à partir de l’étape précédente :
    
    **Pour le client classique :**
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    Lorsque vous y êtes invité, spécifiez le mot de passe des informations d’identification de votre compte de service pour Azure AD, puis cliquez sur **Accepter**.

        
    Si votre compte de service de scanneur ne peut pas se voir accorder le droit **ouvrir une session localement** pour l’installation [, consultez spécifier et utiliser le paramètre Token pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) à partir du Guide de l’administrateur du client.


    **Exemple de client classique :**

    ```
    Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip
    Acquired application access token on behalf of the user
    ```
       
    **Pour le client d’étiquetage unifié :**
    
    ```
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
    
    Si votre compte de service de scanneur ne peut pas se voir accorder le droit **ouvrir une session localement** pour l’installation, utilisez le paramètre *OnBehalfOf* avec set-AIPAuthentication, comme décrit dans [Comment étiqueter des fichiers de manière non interactive pour Azure information protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) du Guide de l’administrateur de ce client.

    **Exemple de client d’étiquetage unifié :**

    ```
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

Le scanneur dispose désormais d’un jeton pour s’authentifier auprès de Azure AD, ce qui est valide pendant un an, deux ans ou n’expire jamais, en fonction de votre configuration de l' **application Web/API** (client classique) ou de la clé secrète client (client d’étiquetage unifié) dans Azure ad. Quand le jeton expire, vous devez répéter les étapes 1 et 2.

Vous pouvez maintenant exécuter votre première analyse en mode découverte.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Exécuter un cycle de découverte et afficher les rapports pour le scanneur

1. Dans le Portail Azure, dans le volet **Azure information protection de travaux d’analyse de contenu** , sélectionnez vos travaux d’analyse de contenu, puis l’option **Analyser maintenant** :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)
    
    Dans votre session PowerShell, vous pouvez également exécuter la commande suivante :
    
        Start-AIPScan

2. Attendez que le scanneur termine son cycle. Une fois que le scanneur a parcouru tous les fichiers inclus dans les magasins de données que vous avez spécifiés, le service s’arrête alors que le service du scanneur continue de s’exécuter :
    
    - Dans le volet **travaux d’analyse de contenu Azure information protection** , utilisez l’option **Actualiser** et attendez que les valeurs des colonnes résultats de la **dernière analyse** et **dernière analyse (heure de fin)** s’affichent.
    
    - Dans PowerShell, vous pouvez exécuter `Get-AIPScannerStatus` pour surveiller le changement d’état.
    
    - Scanner du client classique uniquement : Vérifiez le journal des événements des **applications et services** Windows local, **Azure information protection**. Ce journal indique également lorsque le scanneur a terminé l’analyse, avec un résumé des résultats. Recherchez l’ID d’événement d’information **911**.

3. Passez en revue les rapports stockés dans %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Les fichiers de résumé .txt incluent la durée de l’analyse, le nombre de fichiers analysés et le nombre de fichiers correspondants aux types d’informations. Les fichiers .csv offrent plus de détails pour chaque fichier. Ce dossier stocke jusqu’à 60 rapports pour chaque cycle d’analyse et tous, sauf le dernier rapport, sont compressés afin de réduire l’espace disque requis.
    
    > [!NOTE]
    > Vous pouvez modifier le niveau de journalisation à l’aide du paramètre *ReportLevel* avec [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration), mais vous ne pouvez pas modifier l’emplacement ou le nom du dossier de rapport. Envisagez d’utiliser une jointure de répertoire pour le dossier si vous souhaitez stocker les rapports sur un autre volume ou une autre partition.
    >
    > Par exemple, à l’aide de la commande [Mklink](/windows-server/administration/windows-commands/mklink) : `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    Avec notre paramètre **Policy only** (Stratégie uniquement) pour **Info types to be discovered** (Types d’infos à découvrir), seuls les fichiers qui remplissent les conditions que vous avez configurées pour la classification automatique sont inclus dans les rapports détaillés. Si aucune étiquette n’est appliquée, vérifiez que la configuration de votre étiquette comprend la classification automatique plutôt que recommandée, ou activez l' **étiquetage recommandé sur automatique** (disponible dans le scanneur version 2.7. x. x et versions ultérieures).
    
    > [!TIP]
    > Les scanneurs envoient ces informations à Azure Information Protection toutes les cinq minutes, ce qui permet de voir les résultats en quasi temps quasi réel sur le Portail Azure. Pour plus d’informations, consultez [Création de rapports pour Azure Information Protection](reports-aip.md). 
        
    Si les résultats ne correspondent pas à vos attentes, vous devrez peut-être reconfigurer les conditions que vous avez spécifiées pour vos étiquettes. Si tel est le cas, répétez les étapes 1 à 3 jusqu’à ce que vous soyez prêt à modifier la configuration pour appliquer la classification et éventuellement la protection. 

Le portail Azure affiche des informations portant uniquement sur la dernière analyse. Si vous devez consulter les résultats des analyses précédentes, accédez aux rapports qui sont stockés sur l’ordinateur du scanneur, dans le dossier %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

Quand vous êtes prêt à étiqueter automatiquement les fichiers que le scanneur découvre, passez à la procédure suivante. 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurer le scanneur pour appliquer la classification et la protection

Si vous suivez ces instructions, le scanneur s’exécute une seule fois en mode création de rapports uniquement. Pour modifier ces paramètres, modifiez le travail d’analyse du contenu :

1. De retour dans le volet **Azure information protection-travaux d’analyse de contenu** , sélectionnez le travail de cluster et d’analyse de contenu pour le modifier.

2. Dans le \<**content scan job name**> volet, modifiez les deux paramètres suivants, puis sélectionnez **Enregistrer**:
    
   - Dans la section **travail d’analyse du contenu** : modifiez la **planification** pour **toujours**
   - À partir de la section application de la **stratégie** : modifier **appliquer** la valeur **activé**
    
     Il existe d’autres paramètres de configuration que vous pouvez modifier. Par exemple, si les attributs de fichier sont modifiés et que le scanneur peut réétiqueter les fichiers. Utilisez l’aide contextuelle des informations pour plus d’informations sur chaque paramètre de configuration.

3. Prenez note de l’heure actuelle et redémarrez le scanneur à partir du volet **travaux d’analyse de contenu Azure information protection** :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)
    
    Vous pouvez également exécuter la commande suivante dans votre session PowerShell :
    
        Start-AIPScan

4. Scanner du client classique uniquement : Surveillez de nouveau le journal des événements pour le type d’information **911** , avec un horodatage plus tard que lorsque vous avez démarré l’analyse à l’étape précédente.
    
    Puis examinez les rapports pour déterminer quels fichiers ont été étiquetés, quelle classification a été appliquée et si une protection a été appliquée. Ou bien, utilisez le portail Azure pour consulter plus facilement ces informations.

Puisque nous avons configuré la planification pour qu’elle s’exécute en continu, lorsque le scanneur a parcouru tous les fichiers, il démarre automatiquement un nouveau cycle pour découvrir les fichiers nouveaux et modifiés.

## <a name="troubleshooting-using-scanner-diagnostic-tool"></a>Résolution des problèmes à l’aide de l’outil de diagnostic scanner

Pour résoudre les problèmes liés au scanneur, exécutez les commandes suivantes dans votre session PowerShell :

        $scanner_account_creds= Get-Credential 
        Start-AIPScannerDiagnostics -onbehalf $scanner_account_creds


1. Exécutez uniquement la commande-onbehalf% scanner_account% 
2. Notez que cette commande n’est pas un outil de vérification de la configuration requise. L’outil vérifie si le déploiement de l’analyseur actuel est sain. Veillez à exécuter cette commande uniquement une fois que le déploiement du scanneur est terminé et que la configuration de votre profil est terminée. 

L’outil d’analyse des diagnostics effectue, puis exporte les journaux sur les vérifications suivantes :

|Vérification|Résultat possible|
|-----------|----------|
|Vérification de la base de données| est à jour, est accessible|
|Vérification du réseau| Les URL sont accessibles|
|Vérification de l’authentification| jeton, la stratégie peut être acquise|
|Vérification du profil| le profil est défini dans Portail Azure|
|Vérification de la configuration|la configuration hors connexion/en ligne existe et peut être acquise|
|Vérification des règles|sont valides|

## <a name="stop-a-scan"></a>Arrêter une analyse 

Pour arrêter une analyse que vous avez démarrée précédemment avant qu’elle ne soit terminée, utilisez l’option **arrêter l’analyse** à partir de l’interface, ou
 
![Arrêter une analyse pour le scanneur de Azure Information Protection](./media/scanner-stop-scan.png)
    
Vous pouvez également exécuter la commande suivante dans votre session PowerShell :
    
        Stop-AIPScan 

## <a name="how-files-are-scanned"></a>Procédure d’analyse des fichiers

Lors de l’analyse de fichiers, le scanneur effectue les processus suivants.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. déterminer si les fichiers sont inclus ou exclus pour l’analyse 
Le scanneur ignore automatiquement les fichiers qui sont exclus de la classification et de la protection, comme les fichiers exécutables et les fichiers système. Pour plus d’informations, consultez les guides d’administration suivants :

- Pour le client classique : [types de fichiers exclus de la classification et de la protection](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- Pour le client d’étiquetage unifié : [types de fichiers exclus de la classification et de la protection](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

Vous pouvez modifier ce comportement en définissant une liste de types de fichiers à analyser ou à exclure de l’analyse. Vous pouvez spécifier cette liste pour le scanneur à appliquer à tous les référentiels de données par défaut, et vous pouvez spécifier une liste pour chaque référentiel de données. Pour spécifier cette liste, utilisez le paramètre **types de fichiers à analyser** dans le travail d’analyse du contenu :

![Configurer les types de fichiers à analyser pour le scanneur Azure Information Protection](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. Inspectez et étiquetez les fichiers

Le scanneur utilise ensuite des filtres pour analyser les types de fichiers pris en charge. Ces mêmes filtres sont utilisés par le système d’exploitation pour Windows Search et l’indexation. Sans configuration supplémentaire, Windows IFilter permet d’analyser les types de fichiers utilisés par Word, Excel, PowerPoint ansi que les documents PDF et les fichiers texte.

Pour obtenir la liste complète des types de fichiers pris en charge par défaut, ainsi que des informations supplémentaires sur la façon de configurer des filtres existants qui incluent des fichiers. zip et des fichiers. TIFF, consultez les guides d’administration suivants :

- Pour le client classique : [types de fichiers pris en charge pour l’inspection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)
- Pour le client d’étiquetage unifié : [types de fichiers pris en charge pour l’inspection](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)

Après inspection, ces types de fichiers peuvent être étiquetés à l’aide des conditions que vous avez spécifiées pour vos étiquettes. Ou, si vous utilisez le mode de découverte, ces fichiers peuvent être signalés comme contenant les conditions que vous avez spécifiées pour vos étiquettes ou tous les types d’informations sensibles connus. 

Toutefois, le scanneur ne peut pas étiqueter les fichiers dans les cas suivants :

- Si l’étiquette applique la classification et non la protection, et que le type de fichier ne prend pas en charge la classification uniquement par le client [classique](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) ou le [client d’étiquetage unifié](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- L’étiquette applique la classification et la protection, mais le scanneur ne protège pas le type de fichier.
    
    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). D’autres types de fichiers peuvent être protégés lorsque vous [Modifiez les types de fichiers protégés](#change-which-file-types-to-protect) , comme décrit dans la section suivante.

Par exemple, après inspection des fichiers portant l’extension .txt, le scanneur ne peut pas appliquer une étiquette configurée pour la classification mais pas pour la protection, car le type de fichier .txt ne prend pas en charge la classification uniquement. Si l’étiquette est configurée pour la classification et la protection, et si l’extension de nom de fichier. txt est incluse pour le scanneur à protéger, le scanneur peut étiqueter le fichier. 

> [!TIP]
> Pendant ce processus, si le scanneur s’arrête et ne termine pas l’analyse d’un grand nombre de fichiers dans un référentiel :
> 
> - Vous devrez peut-être augmenter le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers. Le renforcement du serveur pour SharePoint peut être l’une des raisons expliquant pourquoi le scanneur dépasse le nombre de connexions réseau autorisées et s’arrête.
>     
>     Pour vérifier s’il s’agit de la cause de l’arrêt du scanneur, regardez si le message d’erreur suivant est enregistré pour le scanneur dans%*LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog (zippé s’il y a plusieurs journaux) : **Impossible de se connecter au serveur distant---> System .net. Sockets. SocketException : une seule utilisation de chaque adresse de socket**
>    
>     Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).
> 
> - Pour les grandes batteries de serveurs SharePoint, vous devrez peut-être augmenter le seuil d’affichage de liste (par défaut, 5 000). Pour plus d’informations, consultez la documentation SharePoint suivante : [gérer les grandes listes et les bibliothèques dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. étiquetez les fichiers qui ne peuvent pas être inspectés
Pour les types de fichiers qui ne peuvent pas être inspectés, le scanneur applique l’étiquette par défaut dans la stratégie Azure Information Protection ou l’étiquette par défaut que vous configurez pour le scanneur.

Comme dans l’étape précédente, le scanneur ne peut pas étiqueter les fichiers dans les cas suivants :

- Si l’étiquette applique la classification et non la protection, et que le type de fichier ne prend pas en charge la classification uniquement par le client [classique](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) ou le [client d’étiquetage unifié](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- L’étiquette applique la classification et la protection, mais le scanneur ne protège pas le type de fichier.
    
    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). D’autres types de fichiers peuvent être protégés lorsque vous modifiez les types de fichiers à protéger, comme décrit ci-après.

## <a name="change-which-file-types-to-protect"></a>Changer les types de fichiers à protéger

Par défaut, le scanneur protège les types de fichiers Office et les fichiers PDF uniquement. Vous pouvez modifier ce comportement de sorte que, par exemple, le scanneur protège tous les types de fichiers, ce qui correspond au même comportement de protection que le client. Ou le scanneur protège les types de fichiers supplémentaires que vous spécifiez, en plus des types de fichiers Office et des fichiers PDF. 

Pour obtenir des instructions de configuration, consultez les sections suivantes.

### <a name="scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected"></a>Analyseur du client classique : utilisez le registre pour changer les types de fichiers protégés.

Cette section s’applique uniquement au scanneur du client classique.

Pour modifier le comportement par défaut de l’analyseur en vue de protéger les types de fichiers autres que les fichiers Office et les PDF, vous devez modifier le registre et spécifier les types de fichiers supplémentaires que vous souhaitez protéger, ainsi que le type de protection (natif ou générique). Pour obtenir des instructions, consultez [Configuration de l’API de fichier](develop/file-api-configuration.md) dans le Guide du développeur. Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ». En outre, spécifiquement pour le scanneur :

- Le scanneur a son propre comportement par défaut : seuls les formats de fichier Office et les documents PDF sont protégés par défaut. Si le Registre n’est pas modifié, aucun des autres types de fichiers ne sera étiqueté ou protégé par le scanneur.

- Si vous souhaitez utiliser le même comportement de protection par défaut que le client Azure Information Protection, où tous les fichiers sont automatiquement protégés par une protection native ou générique : spécifiez le `*` caractère générique comme clé de Registre, `Encryption` comme valeur (REG_SZ) et `Default` comme données de valeur.

Lorsque vous modifiez le Registre, créez manuellement la clé **MSIPC** et la clé **FileProtection** si elles n’existent pas, ainsi qu’une clé pour chaque extension de nom de fichier.

Par exemple, pour que le scanneur protège les fichiers TIFF en plus des fichiers Office et PDF, le Registre devrait ressembler à l’image suivante, une fois que vous l’avez modifié. Les fichiers TIFF, qui sont des fichiers image, prennent en charge la protection native et l’extension de nom de fichier résultante est .ptiff.

![Modification du Registre pour que le scanneur applique une protection](./media/editregistry-scanner.png)

Pour obtenir la liste des types de fichiers texte et image qui prennent en charge de façon similaire la protection native, mais qui doivent être spécifiés dans le registre, consultez [types de fichiers pris en charge pour la classification et la protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection).

Pour les fichiers ne prenant pas en charge la protection native, indiquez l’extension de nom de fichier comme nouvelle clé et **PFile** pour la protection générique. L’extension de nom de fichier résultante pour le fichier protégé est .pfile.

### <a name="scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected"></a>Analyseur du client d’étiquetage unifié : utiliser PowerShell pour modifier les types de fichiers protégés

Cette section s’applique uniquement au scanneur du client d’étiquetage unifié.

Pour une stratégie d’étiquette qui s’applique au compte d’utilisateur qui télécharge des étiquettes pour le scanneur, spécifiez un paramètre avancé PowerShell nommé **PFileSupportedExtensions**. 

> [!NOTE]
> Pour un scanneur qui a accès à Internet, ce compte d’utilisateur est le compte que vous spécifiez pour le paramètre *DelegatedUser* avec la commande Set-AIPAuthentication.

Exemple 1 : commande PowerShell pour le scanneur afin de protéger tous les types de fichiers, où votre stratégie d’étiquette est nommée « scanner » :

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Exemple 2 : commande PowerShell pour le scanneur afin de protéger les fichiers. xml et. TIFF en plus des fichiers Office et des fichiers PDF, où votre stratégie d’étiquette est nommée « scanner » :

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}

Pour obtenir des instructions détaillées, consultez [modifier les types de fichiers à protéger](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) à partir du Guide de l’administrateur.


## <a name="when-files-are-rescanned"></a>Lorsque les fichiers sont réanalysés

Pour le premier cycle d’analyse, le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, il inspecte uniquement les fichiers nouveaux ou modifiés. 

Vous pouvez forcer le scanneur à inspecter à nouveau tous les fichiers à partir du volet de **travaux d’analyse de contenu Azure information protection** de la portail Azure. Sélectionnez votre travail d’analyse de contenu dans la liste, puis sélectionnez l’option **relancer l’analyse de tous les fichiers** :

![Relancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-rescan-files2.png)

La réinspection de tous les fichiers est utile quand vous voulez que les rapports contiennent tous les fichiers. Ce choix de configuration est généralement utilisé lorsque le scanneur s’exécute en mode découverte. Lorsqu’une analyse complète est terminée, le scanneur passe automatiquement en mode incrémentiel pour inspecter uniquement les fichiers nouveaux ou modifiés lors des analyses suivantes.

En outre, tous les fichiers sont inspectés lorsque le scanneur du client classique télécharge une stratégie de Azure Information Protection qui a des conditions nouvelles ou modifiées et que le scanneur du client d’étiquetage unifié présente des paramètres nouveaux ou modifiés pour l’étiquetage automatique et recommandé. 

Le scanneur actualise la stratégie en fonction des déclencheurs suivants :

- Analyseur du client classique : toutes les heures et lorsque le service démarre et que la stratégie est antérieure à une heure. 

- Analyseur du client d’étiquetage unifié : toutes les quatre heures. 

> [!TIP]
> Si vous devez actualiser la stratégie avant l’intervalle par défaut, par exemple, pendant une période de test : 
>
> - Analyseur à partir du client classique : supprimez manuellement le fichier de stratégie, **Policy.msip** de **% LocalAppData% \Microsoft\MSIP\Policy.msip**.
>
> - Analyseur du client d’étiquetage unifié : supprimez manuellement le contenu de **%LocalAppData%\Microsoft\MSIP\mip \\ < *ProcessName*> \mip**.
>
Ensuite, redémarrez le service du scanneur Azure Information Protection. Si vous avez modifié les paramètres de protection de vos étiquettes, attendez 15 minutes à partir de l’enregistrement des paramètres de protection avant de redémarrer le service.


## <a name="editing-in-bulk-for-the-data-repository-settings"></a>Modification en bloc des paramètres de référentiel de données

Pour les référentiels de données que vous avez ajoutés à un travail d’analyse de contenu, vous pouvez utiliser les options d' **exportation** et d' **importation** pour modifier rapidement les paramètres. Par exemple, pour vos référentiels de données SharePoint, vous souhaitez ajouter un nouveau type de fichier à exclure de l’analyse.

Au lieu de modifier chaque référentiel de données dans le Portail Azure, utilisez l’option d' **exportation** à partir du volet **dépôts** :

![Exportation de paramètres de référentiel de données pour le scanneur](./media/export-scanner-repositories.png)

Modifiez manuellement le fichier pour effectuer la modification, puis utilisez l’option d' **importation** dans le même volet.

## <a name="using-the-scanner-with-alternative-configurations"></a>Utilisation du scanneur avec d’autres configurations

Le scanneur Azure Information Protection prend en charge trois autres scénarios où les étiquettes n’ont pas besoin d’être configurées pour les conditions suivantes : 

- Appliquer une étiquette par défaut à tous les fichiers dans un référentiel de données.
    
    Pour cette configuration, affectez la valeur **off**aux **fichiers d’étiquette basés sur le contenu** . Affectez ensuite la valeur **personnalisé**à l' **étiquette par défaut** , puis sélectionnez l’étiquette à utiliser.
    
    Le contenu des fichiers n’est pas inspecté et tous les fichiers sans étiquette dans le référentiel de données sont étiquetés en fonction de l’étiquette par défaut que vous spécifiez pour le référentiel de données ou le travail d’analyse du contenu. 
    
    Pour le scanneur du client d’étiquetage unifié, vous pouvez également sélectionner **appliquer l’étiquette par défaut** si vous souhaitez que l’étiquette par défaut soit appliquée à tous les fichiers, même s’ils sont déjà étiquetés.
    

- Supprimer des étiquettes existantes de tous les fichiers d’un référentiel de données.
    
    Applicable uniquement au scanneur à partir du client d’étiquetage unifié, cette configuration vous permet de supprimer les étiquettes existantes, y compris la protection, si elles ont été appliquées avec cette étiquette. La protection appliquée indépendamment d’une étiquette est conservée. Utilisez cette configuration si vous devez supprimer toutes les étiquettes des fichiers dans un référentiel.
    
    Configurez les paramètres suivants :
    - **Étiqueter les fichiers en fonction du contenu**: **désactivé**
    - **Étiquette par défaut**: **aucune**
    - **Renommer les fichiers**: **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée

- Identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.
    
    Pour cette configuration, définissez les **Info types to be discovered** (Types d’infos à découvrir) sur **Tous**.
    
    Pour le scanneur du client classique : le scanneur utilise toutes les conditions personnalisées que vous avez spécifiées pour les étiquettes dans la stratégie de Azure Information Protection, ainsi que la liste des types d’informations disponibles pour les étiquettes dans la stratégie de Azure Information Protection. 
    
    Pour le scanneur du client d’étiquetage unifié : le scanneur utilise tous les types d’informations sensibles personnalisés que vous avez spécifiés et la liste des types d’informations sensibles intégrés qui peuvent être sélectionnés dans le centre de gestion d’étiquetage.
    
    Ce paramètre vous permet de retrouver des informations sensibles que vous ne pensiez peut-être pas avoir, mais au détriment des taux d’analyse du scanneur.
    
    Le démarrage rapide suivant pour le scanneur utilise cette configuration : [démarrage rapide : Rechercher les informations sensibles dont vous disposez](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Optimisation des performances du scanneur

Utilisez les instructions suivantes pour vous aider à optimiser les performances du scanneur. Toutefois, si votre priorité est la réactivité de l’ordinateur du scanneur plutôt que les performances de l’analyseur, vous pouvez utiliser un paramètre client avancé pour limiter le nombre de threads utilisés par le scanneur :

- Scanneur client classique : [limiter le nombre de threads utilisés par le scanneur](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)

- Analyseur du client d’étiquetage unifié : suivez les instructions ci-dessous pour [limiter le nombre de threads utilisés par le scanneur](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner) .



Options supplémentaires pour optimiser les performances de l’analyseur :

- **Veillez à avoir une connexion haut débit fiable entre l’ordinateur de l’analyseur et le magasin de données analysé**
    
    Par exemple, placez l’ordinateur de l’analyseur dans le même réseau local ou (de préférence) dans le même segment réseau que le magasin de données analysé.
    
    La qualité de la connexion réseau affecte les performances de l’analyseur parce que pour examiner les fichiers, celui-ci transfère le contenu des fichiers à l’ordinateur exécutant son service. Quand vous réduisez (ou supprimez) le nombre de tronçons réseau que ces données doivent traverser, vous réduisez également la charge sur votre réseau. 

- **Assurez-vous que l’ordinateur de l’analyseur dispose de ressources processeur**
    
    L’inspection du contenu des fichiers ainsi que le chiffrement et le déchiffrement des fichiers sont des actions qui sollicitent le processeur de manière intense. Surveillez les cycles d’analyse standard de vos magasins de données spécifiés pour déterminer si un manque de ressources processeur affecte les performances de l’analyseur.
    
- **N’analysez pas les dossiers locaux sur l’ordinateur exécutant le service de l’analyseur**
    
    Si vous avez des dossiers à analyser sur un serveur Windows, installez l’analyseur sur un autre ordinateur et configurez ces dossiers comme partages réseau à analyser. En séparant les deux fonctions d’hébergement des fichiers et d’analyse des fichiers, les ressources informatiques de ces services n’entrent pas en concurrence.

Si nécessaire, installez plusieurs instances du scanneur. Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance de SQL Server lorsque vous spécifiez un nom de cluster personnalisé (profil) pour le scanneur. Pour le scanneur du client d’étiquetage unifié, plusieurs analyseurs peuvent partager le même cluster (profil), ce qui entraîne des temps d’analyse plus rapides.

Autres facteurs qui affectent les performances de l’analyseur :

- La charge actuelle et les temps de réponse des magasins de données qui contiennent les fichiers à analyser

- Si l’analyseur s’exécute en mode découverte ou en mode d’application
    
    Le mode découverte a généralement un taux d’analyse plus élevé que le mode d’application, car la découverte nécessite une seule action de lecture de fichier tandis que le mode d’application nécessite des actions de lecture et d’écriture.

- Vous modifiez les conditions de la stratégie de Azure Information Protection (client classique) ou de l’étiquetage automatique dans la stratégie d’étiquette (client d’étiquetage unifié)
    
    Votre premier cycle d’analyse lorsque le scanneur doit inspecter chaque fichier prend plus temps que les cycles d’analyse suivants qui, par défaut, inspectent uniquement les fichiers nouveaux et modifiés. Toutefois, si vous modifiez les conditions ou les paramètres d’étiquetage automatique, tous les fichiers sont analysés à nouveau, comme décrit dans la [section précédente](#when-files-are-rescanned).

- La construction d’expressions regex pour des conditions personnalisées
    
    Pour éviter une consommation de mémoire importante et le risque de dépassements du délai d’expiration (15 minutes par fichier), passez en revue vos expressions regex pour vérifier que la correspondance des modèles est efficace. Par exemple :
    
    - Évitez les [quantificateurs gourmands](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - Utilisez des groupes sans capture comme `(?:expression)` au lieu de `(expression)`

- Le niveau de journalisation que vous avez choisi
    
    Vous pouvez choisir entre **Déboguer**, **Information**, **Erreur** et **Désactivé** pour les rapports de l’analyseur. Avec **Désactivé**, vous bénéficiez des meilleures performances alors qu’avec **Déboguer**, l’analyseur est considérablement ralenti et doit être utilisé uniquement pour le dépannage. Pour plus d’informations, consultez le paramètre *ReportLevel* de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- Les fichiers eux-mêmes :
    
    - À l’exception des fichiers Excel, les fichiers Office sont analysés plus rapidement que les fichiers PDF.
    
    - Les fichiers non protégés sont plus rapides à analyser que les fichiers protégés.
    
    - Les gros fichiers prennent évidemment plus de temps à analyser que les petits fichiers.

- De plus :
    
    - Vérifiez que le compte de service qui exécute le scanneur dispose uniquement des droits décrits dans la section [conditions préalables du scanneur](#prerequisites-for-the-azure-information-protection-scanner) , puis configurez le [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) pour désactiver le niveau d’intégrité faible pour le scanneur (client classique uniquement).
    
    - Le scanneur s’exécute plus rapidement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour appliquer une étiquette par défaut à tous les fichiers, car le scanneur n’inspecte pas le contenu du fichier.
    
    - Le scanneur s’exécute plus lentement lorsque la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) est utilisée pour identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.
    
    - Vous pouvez diminuer les délais d’attente du scanneur (client classique uniquement) avec des [Paramètres client avancés](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) pour obtenir des taux d’analyse et une consommation de mémoire inférieurs, mais avec l’accusé de réception que certains fichiers peuvent être ignorés.

## <a name="list-of-cmdlets-for-the-scanner"></a>Liste des cmdlets pour le scanneur

Étant donné que le scanneur est maintenant configuré à partir des Portail Azure, les applets de commande des versions précédentes utilisées pour configurer les référentiels de données, et la liste des types de fichiers analysés sont désormais déconseillées. 

Les applets de commande qui restent incluent des applets de commande qui installent et mettez à niveau le scanneur, modifient la base de données de configuration du scanneur et le cluster (profil), modifient le niveau de rapport local et importent les paramètres de configuration d’un ordinateur déconnecté. 

Liste complète des applets de commande pour le scanneur : 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs) -client d’étiquetage unifié uniquement

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
> Cette section s’applique uniquement au scanneur du client classique. Actuellement, le scanneur du client d’étiquetage unifié n’écrit pas d’informations dans le journal des événements.

-----

Informations **910**

**Cycle du scanneur démarré.**

Cet événement est enregistré lorsque le service du scanneur est démarré et qu’il commence à analyser les fichiers inclus dans les dépôts de données que vous avez spécifiés.

----

Informations **911**

**Cycle du scanneur terminé.**

Cet événement est journalisé quand le scanneur termine une analyse manuelle ou un cycle dans le cadre d’une planification continue.

Si le scanneur a été configuré pour s’exécuter manuellement plutôt que en continu, pour analyser de nouveau les fichiers, définissez la **planification** sur **Manuel** ou **toujours** dans le travail d’analyse du contenu, puis redémarrez le service.

----

## <a name="next-steps"></a>Étapes suivantes

Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez les sections suivantes dans les guides d’administration :

- Pour le client classique : [utilisation de PowerShell avec le client Azure information protection](./rms-client/client-admin-guide-powershell.md)

- Pour le client d’étiquetage unifié : [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md)
