---
title: Déployer le scanneur de Azure Information Protection-versions précédentes
description: Instructions de déploiement pour les versions de l’analyseur de Azure Information Protection antérieures à la version de disponibilité générale actuelle.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b0fc60219636412feaf3f1558da2d229201f0154
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809565"
---
# <a name="deploying-previous-versions-of-the-azure-information-protection-classic-client-scanner"></a>Déploiement des versions précédentes du scanneur du client Azure Information Protection Classic

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le scanneur à partir du client d’étiquetage Unfied, consultez [qu’est-ce que le scanneur d’étiquetage unifié AIP ?](deploy-aip-scanner.md). *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>
> Cet article est destiné aux versions du Azure Information Protection scanner antérieures à la version **1.48.204.0** , mais qui sont toujours prises en charge. Pour mettre à niveau des versions antérieures vers la version actuelle, consultez [mise à niveau de l’analyseur de Azure information protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

Utilisez ces informations pour en savoir plus sur le scanneur Azure Information Protection, puis sur la manière de l’installer, de le configurer et de l’exécuter correctement.

Ce scanneur s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les magasins de données suivants :

- Chemins UNC pour les partages réseau qui utilisent le protocole SMB (Server Message Block).

- Bibliothèques de documents et dossiers pour SharePoint Server 2019 via SharePoint Server 2013. SharePoint 2010 est également pris en charge pour les clients disposant de la [prise en charge étendue de cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Pour analyser et étiqueter des fichiers sur des référentiels cloud, utilisez [Cloud App Security](/cloud-app-security/) au lieu du scanneur.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Présentation du scanneur Azure Information Protection

Quand vous avez configuré votre [stratégie Azure Information Protection](configure-policy.md) pour les étiquettes qui appliquent une classification automatique, vous pouvez étiqueter les fichiers découverts par ce scanneur. Les étiquettes appliquent une classification et elles appliquent ou suppriment éventuellement la protection :

![Présentation de l’architecture du scanneur Azure Information Protection](./media/infoprotect-scanner.png)

Le scanneur peut inspecter tous les fichiers que Windows est capable d’indexer à l’aide de filtres IFilter installés sur l’ordinateur. Ensuite, pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise Microsoft 365 les types d’informations de sensibilité de protection contre la perte de données (DLP) intégrés et la détection de modèle, ou Microsoft 365 des modèles Regex. Étant donné que le scanneur utilise le client Azure Information Protection, il peut classifier et protéger les mêmes [types de fichiers](./rms-client/client-admin-guide-file-types.md).

Vous pouvez exécuter le scanneur en mode découverte uniquement, dans lequel vous utilisez les rapports pour vérifier ce qui se passerait si les fichiers étaient étiquetés. Ou bien, vous pouvez exécuter le scanneur pour appliquer automatiquement les étiquettes. Vous pouvez également exécuter le scanneur pour découvrir les fichiers contenant des types d’informations sensibles, sans configurer d’étiquettes pour les conditions qui appliquent la classification automatique.

Notez que le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers dans les magasins de données que vous spécifiez. Vous pouvez configurer ce cycle pour s’exécuter une ou plusieurs fois.

Vous pouvez indiquer quels types de fichiers analyser ou exclure de l’analyse. Pour limiter les fichiers inspectés par le scanneur, définissez une liste de types de fichiers à l’aide de l’applet de commande **Set-AIPScannerScannedFileTypes**.

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prérequis pour le scanneur Azure Information Protection

Avant d’installer le scanneur Azure Information Protection, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Informations complémentaires|
|---------------|--------------------|
|Ordinateur Windows Server pour exécuter le service du scanneur :<br /><br />- Processeurs 4 cœurs<br /><br />- 8 Go de RAM<br /><br />- 10 Go d’espace libre (en moyenne) pour les fichiers temporaires|Windows Server 2019, Windows Server 2016 ou Windows Server 2012 R2. <br /><br />**Remarque**: à des fins de test ou d’évaluation dans un environnement hors production, vous pouvez utiliser un système d’exploitation client Windows [pris en charge par le client Azure information protection](requirements.md#client-devices).<br /><br />Il peut s’agir d’un ordinateur physique ou virtuel doté d’une connexion réseau rapide et fiable aux magasins de données à scanner.<br /><br /> Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo. <br /><br />Si la connexion Internet n’est pas possible en raison des stratégies de votre organisation, consultez la section [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations) . Dans le cas contraire, assurez-vous que cet ordinateur dispose d’une connectivité Internet qui autorise les URL suivantes sur HTTPs (port 443) :<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|Compte de service pour exécuter le service du scanneur |En plus d’exécuter le service du scanneur sur l’ordinateur Windows Server, ce compte Windows s’authentifie auprès d’Azure AD, puis télécharge la stratégie Azure Information Protection. Ce compte doit être un compte Active Directory et synchronisé avec Azure AD. Si vous ne pouvez pas synchroniser ce compte en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />Ce compte de service a la configuration suivante :<br /><br />- **Ouvrir une session localement**, attribution des droits utilisateur. Ce droit est exigé pour l’installation et la configuration du scanneur, mais pas pour son fonctionnement. Vous devez accorder ce droit au compte de service, mais vous pouvez le supprimer après avoir vérifié que le scanneur peut détecter, classifier et protéger des fichiers. Si l’attribution de ce droit, même pendant une courte période, n’est pas possible en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />- **Ouvrir une session en tant que service**, attribution des droits utilisateur. Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur. <br /><br />-Autorisations sur les référentiels de données : pour les référentiels de données sur SharePoint en local, accordez toujours l’autorisation **modifier** si l’option **Ajouter et personnaliser des pages** est sélectionnée pour le site, ou accordez l’autorisation **concevoir** . Pour les autres référentiels de données, accordez des autorisations **en lecture et en** **écriture** pour analyser les fichiers, puis appliquez la classification et la protection aux fichiers qui remplissent les conditions de la stratégie de Azure information protection. Pour exécuter le scanneur en mode détection uniquement pour les autres référentiels de données, l’autorisation de **lecture** est suffisante.<br /><br />- Pour les étiquettes qui reprotègent ou retire la protection : pour veiller à ce que le scanneur ait toujours accès aux fichiers protégés, faites de ce compte un [super utilisateur](configure-super-users.md) du service Azure Rights Management et vérifiez que la fonctionnalité de super utilisateur est activée. Pour plus d’informations sur la configuration requise des comptes pour appliquer la protection, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md). En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que ce compte est inclus dans les contrôles d’intégration que vous avez configurés.|
|SQL Server pour stocker la configuration du scanneur :<br /><br />- Instance locale ou distante<br /><br />- [Classement non sensible à la casse](/sql/relational-databases/collations/collation-and-unicode-support) <br /><br />-Rôle sysadmin pour installer le scanneur|SQL Server 2012 est la version minimale pour les éditions suivantes :<br /><br />- SQL Server Entreprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Si vous installez plusieurs instances du scanneur, chacune nécessite sa propre instance SQL Server.<br /><br />Lorsque vous installez le scanneur et si votre compte a le rôle Sysadmin, le processus d’installation crée automatiquement la base de données AzInfoProtectionScanner et accorde le rôle db_owner requis au compte de service qui exécute le scanneur. Si vous ne pouvez pas disposer du rôle Sysadmin ou si les stratégies de votre organisation requièrent que les bases de données soient créées et configurées manuellement, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />La taille de la base de données de configuration varie pour chaque déploiement, mais nous vous recommandons d’allouer 500 Mo pour chaque lot de 1 000 000 fichiers que vous souhaitez analyser. |
|Le client Azure Information Protection Classic est installé sur l’ordinateur Windows Server|Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.<br /><br />Pour obtenir des instructions d’installation du client, consultez le [guide de l’administrateur](./rms-client/client-admin-guide.md). Si vous avez déjà installé le scanneur et que vous devez maintenant le mettre à niveau vers une version ultérieure, consultez [Mise à niveau du scanneur Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|
|Étiquettes configurées qui appliquent une classification automatique et éventuellement une protection|Pour plus d’informations sur la configuration d’une étiquette de conditions et pour appliquer la protection :<br /> - [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)<br /> - [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md) <br /><br />**Conseil**: vous pouvez utiliser les instructions du [didacticiel](infoprotect-quick-start-tutorial.md) pour tester le scanneur avec une étiquette qui recherche des numéros de carte de crédit dans un document Word préparé. Vous devez toutefois modifier la configuration de l’étiquette afin que **Sélectionner comment cette étiquette est appliquée** soit défini sur **Automatique** plutôt que sur **Recommandé**. Supprimez ensuite l’étiquette du document (si elle est appliquée), puis copiez le fichier dans un référentiel de données pour le scanneur. <br /><br /> Bien que vous puissiez exécuter le scanneur même si vous n’avez pas configuré les étiquettes qui appliquent la classification automatique, ce scénario n’est pas abordé dans ces instructions. [Plus d’informations](#using-the-scanner-with-alternative-configurations)|
|Pour les bibliothèques de documents et les dossiers SharePoint à analyser :<br /><br />-SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|D’autres versions de SharePoint ne sont pas prises en charge pour le scanneur.<br /><br />Lorsque vous utilisez le contrôle de [version](/sharepoint/governance/versioning-content-approval-and-check-out-planning), le scanneur inspecte et étiquette la dernière version publiée. Si le scanneur étiquette une approbation de fichier et de [contenu](/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) est requise, ce fichier doit être approuvé pour être disponible pour les utilisateurs. <br /><br />Pour les grandes batteries de serveurs SharePoint, regardez si vous devez augmenter le seuil d’affichage de liste (par défaut, 5 000) pour le scanneur pour accéder à tous les fichiers. Pour plus d’informations, consultez la documentation SharePoint suivante : [gérer les grandes listes et les bibliothèques dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Pour scanner des documents Office :<br /><br />- formats de fichier 97-2003 et formats Office Open XML pour Word, Excel et PowerPoint|Pour plus d’informations sur les types de fichiers pris en charge par le scanneur pour ces formats de fichiers, consultez [Types de fichiers pris en charge par le client Azure Information Protection](./rms-client/client-admin-guide-file-types.md).|
|Pour les chemins longs :<br /><br />- 260 caractères maximum, sauf si le scanneur est installé sur Windows 2016 et que l’ordinateur est configuré pour prendre en charge les chemins longs.|Windows 10 et Windows Server 2016 prennent en charge des longueurs de chemin de plus de 260 caractères avec le [paramètre de stratégie de groupe](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)suivant : stratégie de l' **ordinateur local**  >  **Configuration ordinateur**  >  **modèles d’administration**  >  **tous les paramètres**  >  **activer les chemins longs Win32**<br /><br /> Pour plus d’informations sur la prise en charge des chemins de fichiers longs, consultez la section consacrée à la [longueur maximale des chemins](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

Si vous ne pouvez pas respecter toutes les conditions dans la table, car votre organisation l’interdit, consultez la section suivante pour obtenir des alternatives.

Si toutes les conditions requises sont remplies, passez directement à la [section sur l’installation](#install-the-scanner).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Déploiement du scanneur avec d’autres configurations

Les prérequis répertoriés dans la table correspondent aux exigences par défaut pour le scanneur et sont recommandés pour obtenir la configuration la plus simple pour le déploiement du scanneur. Ils doivent être adaptés aux tests initiaux, afin que vous puissiez vérifier les fonctionnalités du scanneur. Toutefois, dans un environnement de produit, les stratégies de votre organisation peuvent interdire ces exigences par défaut en raison d’une ou plusieurs des restrictions suivantes :

- Les serveurs ne sont pas autorisés à se connecter à Internet

- Sysadmin ne peut pas vous être accordé ou vous devez créer des bases de données et les configurer manuellement

- Les comptes de service ne peuvent pas se voir accorder le droit **ouvrir une session localement**

- Les comptes de service ne peuvent pas être synchronisés avec Azure Active Directory mais les serveurs ont une connectivité Internet

Le scanneur peut prendre en charge ces restrictions, mais celles-ci nécessitent une configuration supplémentaire.

#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction : le serveur de scanneur ne peut pas disposer d’une connexion Internet

Suivez les instructions pour un [ordinateur déconnecté](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers).

Notez que dans cette configuration, le scanneur ne peut pas appliquer la protection (ou supprimer la protection) à l’aide de la clé cloud de votre organisation. Au lieu de cela, le scanneur est limité à l’utilisation d’étiquettes qui appliquent la classification uniquement, ou la protection qui utilise [HYOK](configure-adrms-restrictions.md).

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

Si le rôle Sysadmin peut vous être attribué temporairement pour installer le scanneur, vous pouvez supprimer ce rôle lorsque l’installation du scanneur est terminée. Lorsque vous utilisez cette configuration, la base de données est automatiquement créée pour vous et le compte de service du scanneur obtient automatiquement les autorisations nécessaires. Toutefois, le compte utilisateur qui configure le scanneur nécessite le rôle db_owner pour la base de données AzInfoProtectionScanner, et vous devez attribuer manuellement ce rôle au compte utilisateur.

Si vous ne pouvez pas recevoir le rôle sysadmin même temporairement, vous devez demander à un utilisateur disposant des droits d’administrateur système de créer manuellement une base de données nommée AzInfoProtectionScanner avant d’installer le scanneur. Pour cette configuration, les rôles suivants doivent être attribués :

|Compte|Rôle au niveau de la base de données|
|--------------------------------|---------------------|
|Compte de service pour le scanneur|db_owner|
|Compte utilisateur pour l’installation du scanneur|db_owner|
|Compte utilisateur pour la configuration du scanneur |db_owner|

En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Mais si vous utilisez des comptes différents, ils ont tous les deux besoin du rôle db_owner pour la base de données AzInfoProtectionScanner.

Pour créer un utilisateur et accorder des droits de db_owner sur cette base de données, demandez à l’administrateur système d’exécuter le script SQL suivant deux fois. La première fois, pour le compte de service qui exécute le scanneur, et la seconde fois pour installer et gérer le scanneur. Avant d’exécuter le script, remplacez *domaine\utilisateur* par le nom de domaine et le nom de compte d’utilisateur du compte de service ou du compte d’utilisateur :

```sql
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
USE AzInfoProtectionScanner IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
```

En outre :

- Vous devez être un administrateur local sur le serveur qui exécutera le scanneur.
- Le compte de service qui exécutera le scanneur doit disposer des autorisations contrôle total sur les clés de Registre suivantes :

    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

Si, après avoir configuré ces autorisations, vous voyez une erreur lors de l’installation du scanneur, l’erreur peut être ignorée et vous pouvez démarrer manuellement le service du scanneur.

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restriction : le compte de service pour le scanneur ne peut pas obtenir le droit **Ouvrir une session localement**

Si les stratégies de votre organisation interdisent le droit **Ouvrir une session localement** pour les comptes de service, mais autorisent le droit **Se connecter en tant que traitement par lots**, suivez les instructions sous [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) dans le guide de l’administrateur.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory mais le serveur dispose d’une connexion Internet

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- Pour le compte de service du scanneur, vous pouvez utiliser un compte Windows local ou un compte Active Directory.

- Pour le compte Azure Active Directory, suivez les instructions sous [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) dans le guide de l’administrateur.

## <a name="install-the-scanner"></a>Installer le scanneur

1. Connectez-vous à l’ordinateur Windows Server qui exécutera le scanneur. Utilisez un compte disposant de droits d’administrateur local et qui est autorisé à écrire dans la base de données principale SQL Server.

2. Ouvrez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Exécutez l’applet de commande **install-AIPScanner** , en spécifiant votre SQL Server instance sur laquelle créer une base de données pour le scanneur de Azure information protection :

    ```ps
    Install-AIPScanner -SqlServerInstance <name>
    ```

    Par exemple :

    - Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1`

    - Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`

    - Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`

    Lorsque vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur ( \<domain\user name> ) et du mot de passe.

4. Vérifiez que le service est maintenant installé à l’aide des **Outils d’administration**  >  **services**.

    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie afin de pouvoir s’exécuter sans assistance.

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Obtenir un jeton Azure AD pour le scanneur

Le jeton Azure AD permet au compte de service du scanneur de s’authentifier auprès du service Azure Information Protection.

1. À partir du même ordinateur Windows Server ou à partir de votre bureau, connectez-vous au portail Azure pour créer deux applications Azure AD nécessaires pour spécifier un jeton d’accès à des fins d’authentification. Après une connexion interactive initiale, ce jeton permet au scanneur de s’exécuter de manière non interactive.

    Pour créer ces applications, suivez les instructions données dans [Guide pratique pour étiqueter des fichiers de manière non interactive pour Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) dans le guide de l’administrateur.

2. À partir de l’ordinateur Windows Server, si votre compte de service de scanneur a reçu l’autorisation **Ouvrir une session localement** pour l’installation : connectez-vous avec ce compte et démarrez une session PowerShell. Exécutez **Set-AIPAuthentication**, en spécifiant les valeurs copiées à partir de l’étape précédente :

    ```ps
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    Lorsque vous y êtes invité, spécifiez le mot de passe des informations d’identification de votre compte de service pour Azure AD, puis cliquez sur **Accepter**.

    Si l’autorisation **Ouvrir une session localement** ne peut pas être accordée à votre compte de service de scanneur pour l’installation : suivez les instructions de la section [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) du guide de l’administrateur.

Le scanneur a maintenant un jeton pour s’authentifier auprès d’Azure AD, lequel jeton est valide pendant un an, deux ans, ou définitivement (il n’expire jamais), selon votre configuration de l’**application web/API** dans Azure AD. Quand le jeton expire, vous devez répéter les étapes 1 et 2.

Vous êtes maintenant prêt à spécifier les magasins de données à analyser.

## <a name="specify-data-stores-for-the-scanner"></a>Spécifier les magasins de données pour le scanneur

Utilisez l’applet de commande **Add-AIPScannerRepository** pour spécifier les magasins de données à analyser à l’aide du scanneur Azure Information Protection. Vous pouvez spécifier des chemins d’accès UNC et des URL de serveur SharePoint pour les dossiers et bibliothèques de documents SharePoint.

Versions prises en charge pour SharePoint : SharePoint Server 2019, SharePoint Server 2016 et SharePoint Server 2013. SharePoint Server 2010 est également pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

1. À partir du même ordinateur Windows Server, dans votre session PowerShell, ajoutez votre premier magasin de données en exécutant la commande suivante :

    ```ps
    Add-AIPScannerRepository -Path <path>
    ```

    Par exemple : `Add-AIPScannerRepository -Path \\NAS\Documents`

    Pour obtenir d’autres exemples, utilisez la commande PowerShell Help `Get-Help Add-AIPScannerRepository -examples` pour cette applet de commande.

2. Répétez cette commande pour tous les magasins de données à analyser. Si vous avez besoin de supprimer un magasin de données que vous avez ajouté, utilisez l’applet de commande **Remove-AIPScannerRepository**.

3. Vérifiez que vous avez spécifié tous les magasins de données correctement en exécutant l’applet de commande **Get-AIPScannerRepository** :
    
    ```ps
    Get-AIPScannerRepository
    ```

Avec la configuration par défaut du scanneur, vous êtes maintenant prêt à exécuter votre première analyse en mode découverte.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Exécuter un cycle de découverte et afficher les rapports pour le scanneur

1. Dans votre session PowerShell, démarrez le scanneur en exécutant la commande suivante :

    ```ps
    Start-AIPScan
    ```

    Vous pouvez également démarrer le scanneur à partir du portail Azure. Dans le volet **Azure information protection-nœuds** , sélectionnez le nœud de votre scanneur, puis l’option **Analyser maintenant** :

    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

2. Attendez que le scanneur termine son cycle en exécutant la commande suivante :

    ```ps
    Get-AIPScannerStatus
    ```

    Vous pouvez également afficher l’État à partir du volet **Azure information protection-Nodes** dans le portail Azure, en vérifiant la colonne **État** .

    Recherchez l’état pour afficher **Idle** (Inactif) plutôt que **Scanning** (Analyse).

    Une fois que le scanneur a parcouru tous les fichiers inclus dans les magasins de données que vous avez spécifiés, le service s’arrête alors que le service du scanneur continue de s’exécuter.

    Consultez le journal des événements **Applications et services** Windows local, **Azure Information Protection**. Ce journal indique également lorsque le scanneur a terminé l’analyse, avec un résumé des résultats. Recherchez l’ID d’événement d’information **911**.

3. Passez en revue les rapports stockés dans %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Les fichiers de résumé .txt incluent la durée de l’analyse, le nombre de fichiers analysés et le nombre de fichiers correspondants aux types d’informations. Les fichiers .csv offrent plus de détails pour chaque fichier. Ce dossier stocke jusqu’à 60 rapports pour chaque cycle d’analyse et tous, sauf le dernier rapport, sont compressés afin de réduire l’espace disque requis.

    > [!NOTE]
    > Vous pouvez modifier le niveau de journalisation à l’aide du paramètre *ReportLevel* avec **Set-AIPScannerConfiguration**, mais vous ne pouvez pas modifier l’emplacement ou le nom du dossier de rapport. Envisagez d’utiliser une jointure de répertoire pour le dossier si vous souhaitez stocker les rapports sur un autre volume ou une autre partition.
    >
    > Par exemple, à l’aide de la commande [Mklink](/windows-server/administration/windows-commands/mklink) : `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

    Avec le paramètre par défaut, seuls les fichiers qui remplissent les conditions que vous avez configurées pour la classification automatique sont inclus dans les rapports détaillés. Si vous ne voyez pas les étiquettes appliquées dans ces rapports, vérifiez que la configuration de votre étiquette inclut la classification automatique au lieu de la classification recommandée.

    > [!TIP]
    > Les scanneurs envoient ces informations à Azure Information Protection toutes les cinq minutes, ce qui permet de voir les résultats en quasi temps quasi réel sur le Portail Azure. Pour plus d’informations, consultez [Création de rapports pour Azure Information Protection](reports-aip.md).

    Si les résultats ne correspondent pas à ce que vous attendez, vous devez peut-être ajuster les conditions que vous avez spécifiées dans votre stratégie Azure Information Protection. Si tel est le cas, répétez les étapes 1 à 3 jusqu’à ce que vous soyez prêt à modifier la configuration pour appliquer la classification et éventuellement la protection.

Le portail Azure affiche des informations portant uniquement sur la dernière analyse. Si vous devez consulter les résultats des analyses précédentes, accédez aux rapports qui sont stockés sur l’ordinateur du scanneur, dans le dossier %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

Quand vous êtes prêt à étiqueter automatiquement les fichiers que le scanneur découvre, passez à la procédure suivante.

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurer le scanneur pour appliquer la classification et la protection

Dans son paramétrage par défaut, le scanneur s’exécute une seule fois en mode création de rapports uniquement. Pour modifier ces paramètres, utilisez **Set-AIPScannerConfiguration**:

1. Sur l’ordinateur Windows Server, dans la session PowerShell, exécutez la commande suivante :

    ```ps
    Set-AIPScannerConfiguration -Enforce On -Schedule Always
    ```

    Il existe d’autres paramètres de configuration que vous pouvez modifier. Par exemple, si les attributs de fichier sont modifiés et ce qui est enregistré dans les rapports. De plus, si votre stratégie Azure Information Protection inclut le paramètre qui exige un message de justification pour diminuer le niveau de classification ou supprimer la protection, spécifiez ce message à l’aide de cette applet de commande. Pour plus d’informations sur chaque paramètre de configuration, utilisez la commande d’aide PowerShell suivante : `Get-Help Set-AIPScannerConfiguration -detailed`

2. Notez l’heure actuelle et redémarrez le scanneur en exécutant la commande suivante :
    
    ```ps
    Start-AIPScan
    ```

    Vous pouvez également démarrer le scanneur à partir du portail Azure. Dans le volet **Azure information protection-nœuds** , sélectionnez le nœud de votre scanneur, puis l’option **Analyser maintenant** :

    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

3. Recherchez dans le journal des événements le type d’information **911** dont l’heure horodatée est ultérieure à l’heure du démarrage du scanneur à l’étape précédente.

    Puis examinez les rapports pour déterminer quels fichiers ont été étiquetés, quelle classification a été appliquée et si une protection a été appliquée. Ou bien, utilisez le portail Azure pour consulter plus facilement ces informations.

Puisque nous avons configuré la planification pour qu’elle s’exécute en continu, quand le scanneur a parcouru tous les fichiers, il démarre un nouveau cycle pour découvrir les fichiers nouveaux et modifiés.

## <a name="how-files-are-scanned"></a>Procédure d’analyse des fichiers

Lors de l’analyse de fichiers, le scanneur effectue les processus suivants.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. déterminer si les fichiers sont inclus ou exclus pour l’analyse

Le scanneur ignore automatiquement les fichiers qui sont [exclus de la classification et de la protection](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection), comme les fichiers exécutables et les fichiers système.

Vous pouvez modifier ce comportement en définissant une liste de types de fichiers à analyser ou à exclure de l’analyse. Lorsque vous définissez cette liste sans spécifier de référentiel de données, la liste s’applique à tous les référentiels de données qui n’ont pas leur propre liste spécifiée. Pour établir cette liste, utilisez **Set-AIPScannerScannedFileTypes**.

Après avoir spécifié votre liste de types de fichiers, vous pouvez ajouter un nouveau type de fichier à l’aide de **Add-AIPScannerScannedFileTypes** et en supprimer un à l’aide de **Remove-AIPScannerScannedFileTypes**.

### <a name="2-inspect-and-label-files"></a>2. Inspectez et étiquetez les fichiers

Le scanneur utilise ensuite des filtres pour analyser les types de fichiers pris en charge. Ces mêmes filtres sont utilisés par le système d’exploitation pour Windows Search et l’indexation. Sans configuration supplémentaire, Windows IFilter permet d’analyser les types de fichiers utilisés par Word, Excel, PowerPoint ansi que les documents PDF et les fichiers texte.

Pour obtenir la liste complète des types de fichiers pris en charge par défaut et des informations supplémentaires sur la configuration de filtres existants qui incluent les fichiers .zip et .tiff, consultez [Types de fichiers pris en charge pour l’inspection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection).

Après inspection, ces types de fichiers peuvent être étiquetés à l’aide des conditions que vous avez spécifiées pour vos étiquettes. Ou, si vous utilisez le mode de découverte, ces fichiers peuvent être signalés comme contenant les conditions que vous avez spécifiées pour vos étiquettes ou tous les types d’informations sensibles connus.

Toutefois, le scanneur ne peut pas étiqueter les fichiers dans les cas suivants :

- L’étiquette applique la classification mais pas la protection, et le type de fichier [ne prend pas en charge la classification uniquement](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- L’étiquette applique la classification et la protection, mais le scanneur ne protège pas le type de fichier.

    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Il est possible de protéger d’autres types de fichiers quand vous [modifiez le Registre](#editing-the-registry-for-the-scanner), comme décrit dans la section suivante.

Par exemple, après inspection des fichiers portant l’extension .txt, le scanneur ne peut pas appliquer une étiquette configurée pour la classification mais pas pour la protection, car le type de fichier .txt ne prend pas en charge la classification uniquement. Si l’étiquette est configurée pour la classification et la protection et que le Registre est modifié pour le type de fichier .txt, le scanneur peut étiqueter le fichier.

> [!TIP]
> Pendant ce processus, si le scanneur s’arrête et ne termine pas l’analyse d’un grand nombre de fichiers dans un référentiel :
>
> - Vous devrez peut-être augmenter le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers. Le renforcement du serveur pour SharePoint peut être l’une des raisons expliquant pourquoi le scanneur dépasse le nombre de connexions réseau autorisées et s’arrête.
>  
>     Pour vérifier s’il s’agit de la cause de l’arrêt du scanneur, regardez si le message d’erreur suivant est enregistré pour le scanneur dans%*LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog (zippé s’il y a plusieurs journaux) : **Impossible de se connecter au serveur distant---> System .net. Sockets. SocketException : une seule utilisation de chaque adresse de socket**
>  
>     Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).
>
> - Pour les grandes batteries de serveurs SharePoint, vous devrez peut-être augmenter le seuil d’affichage de liste (par défaut, 5 000). Pour plus d’informations, consultez la documentation SharePoint suivante : [gérer les grandes listes et les bibliothèques dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. étiquetez les fichiers qui ne peuvent pas être inspectés

Pour les types de fichiers qui ne peuvent pas être inspectés, le scanneur applique l’étiquette par défaut dans la stratégie Azure Information Protection ou l’étiquette par défaut que vous configurez pour le scanneur.

Comme dans l’étape précédente, le scanneur ne peut pas étiqueter les fichiers dans les cas suivants :

- L’étiquette applique la classification mais pas la protection, et le type de fichier [ne prend pas en charge la classification uniquement](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- L’étiquette applique la classification et la protection, mais le scanneur ne protège pas le type de fichier.

    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Il est possible de protéger d’autres types de fichiers quand vous [modifiez le Registre](#editing-the-registry-for-the-scanner), comme décrit ci-après.

### <a name="editing-the-registry-for-the-scanner"></a>Modification du Registre pour le scanneur

Pour changer le comportement par défaut du scanneur pour protéger d’autres types de fichiers que les fichiers Office et PDF, vous devez modifier manuellement le Registre et indiquer les types de fichiers supplémentaires qui doivent être protégés ainsi que le type de protection (native ou générique). Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ». En outre, spécifiquement pour le scanneur :

- Le scanneur a son propre comportement par défaut : seuls les formats de fichier Office et les documents PDF sont protégés par défaut. Si le Registre n’est pas modifié, aucun des autres types de fichiers ne sera étiqueté ou protégé par le scanneur.

- Si vous souhaitez utiliser le même comportement de protection par défaut que le client Azure Information Protection, où tous les fichiers sont automatiquement protégés par une protection native ou générique : spécifiez le `*` caractère générique comme clé de Registre, `Encryption` comme valeur (REG_SZ) et `Default` comme données de valeur.

Lorsque vous modifiez le Registre, créez manuellement la clé **MSIPC** et la clé **FileProtection** si elles n’existent pas, ainsi qu’une clé pour chaque extension de nom de fichier.

Par exemple, pour que le scanneur protège les fichiers TIFF en plus des fichiers Office et PDF, le Registre devrait se présenter comme dans l’image suivante, une fois que vous l’avez modifié. Les fichiers TIFF, qui sont des fichiers image, prennent en charge la protection native et l’extension de nom de fichier résultante est .ptiff.

![Modification du Registre pour que le scanneur applique une protection](./media/editregistry-scanner.png)

Pour obtenir la liste des types de fichiers texte et image qui prennent en charge de manière similaire la protection native mais qui doivent être spécifiés dans le Registre, consultez [Types de fichiers pris en charge pour la classification et la protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) dans le guide de l’administrateur.

Pour les fichiers ne prenant pas en charge la protection native, indiquez l’extension de nom de fichier comme nouvelle clé et **PFile** pour la protection générique. L’extension de nom de fichier résultante pour le fichier protégé est .pfile.

## <a name="when-files-are-rescanned"></a>Lorsque les fichiers sont réanalysés

Pour le premier cycle d’analyse, le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, il inspecte uniquement les fichiers nouveaux ou modifiés.

Vous pouvez forcer le scanneur à inspecter à nouveau tous les fichiers en exécutant **Start-AIPScan** avec le paramètre *Reset* . Le scanneur doit être configuré pour une planification manuelle, ce qui nécessite que le paramètre de *planification* soit défini sur **Manuel** avec **Set-AIPScannerConfiguration**.

Vous pouvez également forcer le scanneur à inspecter à nouveau tous les fichiers à partir du volet **Azure information protection-nœuds** du portail Azure. Sélectionnez votre scanneur dans la liste, puis l’option **Rescan all files** (Relancer l’analyse de tous les fichiers) :

![Relancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-rescan-files.png)

La réinspection de tous les fichiers est utile quand vous voulez que les rapports contiennent tous les fichiers. Ce choix de configuration est généralement utilisé lorsque le scanneur s’exécute en mode découverte. Lorsqu’une analyse complète est terminée, le scanneur passe automatiquement en mode incrémentiel pour inspecter uniquement les fichiers nouveaux ou modifiés lors des analyses suivantes.

De plus, tous les fichiers sont inspectés quand le scanneur télécharge une stratégie Azure Information Protection qui présente des conditions nouvelles ou modifiées. Le scanneur actualise la stratégie toutes les heures, quand le service démarre et que la stratégie remonte à plus d’une heure.  

> [!TIP]
> Si vous avez besoin d’actualiser la stratégie avant cet intervalle d’une heure, par exemple, pendant une période de test : supprimez manuellement le fichier de stratégie **Policy.msip** de **%LocalAppData%\Microsoft\MSIP\Policy.msip** et de **%LocalAppData%\Microsoft\MSIP\Scanner**. Ensuite, redémarrez le service du scanneur Azure Information Protection.
>
> Si vous avez changé les paramètres de protection de la stratégie, attendez 15 minutes après l’enregistrement des paramètres de protection avant de redémarrer le service.

Si le scanneur a téléchargé une stratégie sans conditions automatiques, la copie du fichier de stratégie dans le dossier du scanneur n’est pas mise à jour. Dans ce scénario, vous devez supprimer le fichier de stratégie **Policy.msip** dans **%LocalAppData%\Microsoft\MSIP\Policy.msip** et dans **%LocalAppData%\Microsoft\MSIP\Scanner** pour que le scanneur puisse utiliser un fichier de stratégie récemment téléchargé avec des étiquettes correctement configurées pour les conditions automatiques.

## <a name="using-the-scanner-with-alternative-configurations"></a>Utilisation du scanneur avec d’autres configurations

Il existe deux scénarios pris en charge par le scanneur Azure Information Protection dans lesquels il n’est pas nécessaire que des étiquettes soient configurées pour des conditions quelles qu’elles soient :

- Appliquer une étiquette par défaut à tous les fichiers dans un référentiel de données.

    Pour cette configuration, utilisez l’applet de commande **Set-AIPScannerRepository** et définissez le paramètre *MatchPolicy* sur **Off**.

    Le contenu des fichiers n’est pas inspecté et tous les fichiers du référentiel de données sont étiquetés avec l’étiquette par défaut que vous spécifiez pour le référentiel de données (avec le paramètre *SetDefaultLabel*) ou si celle-ci n’est pas spécifié, l’étiquette par défaut qui est spécifiée comme paramètre de stratégie pour le compte d’analyse.

- Identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.

    Pour cette configuration, utilisez l’applet de commande **Set-AIPScannerConfiguration** et définissez le paramètre *DiscoverInformationTypes* sur **All**.

    Le scanneur utilise toute condition personnalisée que vous avez spécifiée pour les étiquettes dans la stratégie Azure Information Protection et la liste des types d’informations qui sont disponibles pour les étiquettes dans la stratégie Azure Information Protection.

    Le démarrage rapide suivant utilise cette configuration, bien qu’il s’agisse de la version actuelle du scanneur : [démarrage rapide : Découvrez les informations sensibles dont vous disposez](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Optimisation des performances du scanneur

Utilisez les instructions suivantes pour vous aider à optimiser les performances du scanneur. Toutefois, si votre priorité est la réactivité de l’ordinateur du scanneur plutôt que les performances de l’analyseur, vous pouvez utiliser un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner) pour limiter le nombre de threads utilisés par le scanneur.

Pour optimiser les performances de l’analyseur :

- **Veillez à avoir une connexion haut débit fiable entre l’ordinateur de l’analyseur et le magasin de données analysé**

    Par exemple, placez l’ordinateur de l’analyseur dans le même réseau local ou (de préférence) dans le même segment réseau que le magasin de données analysé.

    La qualité de la connexion réseau affecte les performances de l’analyseur parce que pour examiner les fichiers, celui-ci transfère le contenu des fichiers à l’ordinateur exécutant son service. Quand vous réduisez (ou supprimez) le nombre de tronçons réseau que ces données doivent traverser, vous réduisez également la charge sur votre réseau.

- **Assurez-vous que l’ordinateur de l’analyseur dispose de ressources processeur**

    L’inspection du contenu des fichiers à la recherche d’une correspondance avec vos conditions de configuration ainsi que le chiffrement et le déchiffrement des fichiers sont des actions qui sollicitent le processeur de manière intense. Surveillez les cycles d’analyse standard de vos magasins de données spécifiés pour déterminer si un manque de ressources processeur affecte les performances de l’analyseur.


Autres facteurs qui affectent les performances de l’analyseur :

- La charge actuelle et les temps de réponse des magasins de données qui contiennent les fichiers à analyser

- Si l’analyseur s’exécute en mode découverte ou en mode d’application

    Le mode découverte a généralement un taux d’analyse plus élevé que le mode d’application, car la découverte nécessite une seule action de lecture de fichier tandis que le mode d’application nécessite des actions de lecture et d’écriture.

- Le changement des conditions d’Azure Information Protection

    Votre premier cycle d’analyse quand l’analyseur doit inspecter chaque fichier prend bien évidemment plus temps que les cycles d’analyse suivants qui, par défaut, inspectent uniquement les fichiers nouveaux et modifiés. Toutefois, si vous changez les conditions dans la stratégie Azure Information Protection, tous les fichiers sont réanalysés, comme décrit dans la [section précédente](#when-files-are-rescanned).

- La construction d’expressions regex pour des conditions personnalisées

    Pour éviter une consommation de mémoire importante et le risque de dépassements du délai d’expiration (15 minutes par fichier), passez en revue vos expressions regex pour vérifier que la correspondance des modèles est efficace. Par exemple :

    - Évitez les [quantificateurs gourmands](/dotnet/standard/base-types/quantifiers-in-regular-expressions)

    - Utilisez des groupes sans capture comme `(?:expression)` au lieu de `(expression)`

- Le niveau de journalisation que vous avez choisi

    Vous pouvez choisir entre **Déboguer**, **Information**, **Erreur** et **Désactivé** pour les rapports de l’analyseur. Avec **Désactivé**, vous bénéficiez des meilleures performances alors qu’avec **Déboguer**, l’analyseur est considérablement ralenti et doit être utilisé uniquement pour le dépannage. Pour plus d’informations, consultez le paramètre *ReportLevel* pour l’applet de commande Set-AIPScannerConfiguration en exécutant `Get-Help Set-AIPScannerConfiguration -detailed` .

- Les fichiers eux-mêmes :

    - À l’exception des fichiers Excel, les fichiers Office sont analysés plus rapidement que les fichiers PDF.

    - Les fichiers non protégés sont plus rapides à analyser que les fichiers protégés.

    - Les gros fichiers prennent évidemment plus de temps à analyser que les petits fichiers.

- En outre :

    - Vérifiez que le compte de service qui exécute le scanneur dispose uniquement des droits décrits dans la section [conditions préalables du scanneur](#prerequisites-for-the-azure-information-protection-scanner) , puis configurez le [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) pour désactiver le niveau d’intégrité faible du scanneur.

    - Le scanneur s’exécute plus rapidement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour appliquer une étiquette par défaut à tous les fichiers, car le scanneur n’inspecte pas le contenu du fichier.

    - Le scanneur s’exécute plus lentement lorsque la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) est utilisée pour identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.

    - Vous pouvez diminuer les délais d’attente du scanneur avec les [Paramètres avancés du client](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) pour obtenir des taux d’analyse et une consommation de mémoire inférieurs, mais avec l’accusé de réception que certains fichiers peuvent être ignorés.

## <a name="list-of-cmdlets-for-the-scanner"></a>Liste des cmdlets pour le scanneur

D’autres applets de commande propres au scanneur vous permettent de modifier son compte de service et sa base de données, d’obtenir ses paramètres actuels et de désinstaller son service. Le scanneur utilise les applets de commande suivantes :

- Add-AIPScannerScannedFileTypes

- Add-AIPScannerRepository

- Get-AIPScannerConfiguration

- Get-AIPScannerRepository

- Get-AIPScannerStatus

- Install-AIPScanner

- Remove-AIPScannerRepository

- Remove-AIPScannerScannedFileTypes

- Set-AIPScanner

- Set-AIPScannerConfiguration

- Set-AIPScannerScannedFileTypes

- Set-AIPScannerRepository

- Start-AIPScan

- Uninstall-AIPScanner

- Update-AIPScanner

> [!NOTE]
> La plupart de ces applets de commande sont désormais dépréciées dans la version actuelle du scanneur, et l’aide en ligne pour les applets de commande du scanneur reflète cette modification. Pour obtenir une aide sur les applets de commande antérieures à la version 1.48.204.0 du scanneur, utilisez la `Get-Help <cmdlet name>` commande intégrée dans votre session PowerShell.

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>ID du journal des événements et descriptions pour le scanneur

Utilisez les sections suivantes pour identifier les ID d’événement possibles et les descriptions du scanneur. Ces événements sont journalisés sur le serveur qui exécute le service de scanneur, dans le journal des événements **Applications et services** Windows, **Azure Information Protection**.

-----

Informations **910**

**Cycle du scanneur démarré.**

Cet événement est enregistré lorsque le service du scanneur est démarré et qu’il commence à analyser les fichiers inclus dans les dépôts de données que vous avez spécifiés.

----

Informations **911**

**Cycle du scanneur terminé.**

Cet événement est journalisé quand le scanneur termine une analyse manuelle ou un cycle dans le cadre d’une planification continue.

Si le scanneur a été configuré pour une exécution manuelle et non continue, utilisez l’applet de commande **Start-AIPScan** pour exécuter une nouvelle analyse. Pour changer la planification, utilisez l’applet de commande **Set-AIPScannerConfiguration** et le paramètre *Schedule*.

----

## <a name="next-steps"></a>Étapes suivantes

Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs-classic.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur tous les scénarios qui utilisent PowerShell, consultez [Utiliser PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).