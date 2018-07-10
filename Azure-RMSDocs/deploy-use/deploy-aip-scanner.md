---
title: Déployer le scanneur Azure Information Protection
description: Instructions pour installer, configurer et exécuter le scanneur Azure Information Protection qui permet de découvrir, classifier et protéger des fichiers sur des magasins de données.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 0b663f8f514aadf51b0ad549761d90d30e07811d
ms.sourcegitcommit: 92bb6d3163e455250a84281dac62b5af82f8c4f1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37042879"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2*

Utilisez ces informations pour en savoir plus sur le scanneur Azure Information Protection, puis sur la manière de l’installer, de le configurer et de l’exécuter correctement. 

Ce scanneur s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les magasins de données suivants :

- Dossiers locaux sur l’ordinateur Windows Server qui exécute le scanneur.

- Chemins UNC pour les partages réseau qui utilisent le protocole SMB (Server Message Block).

- Sites et bibliothèques pour SharePoint Server 2016 et SharePoint Server 2013.

Pour analyser et étiqueter des fichiers sur des référentiels cloud, utilisez [Cloud App Security](https://docs.microsoft.com/cloud-app-security/).

## <a name="overview-of-the-azure-information-protection-scanner"></a>Présentation du scanneur Azure Information Protection

Quand vous avez configuré votre [stratégie Azure Information Protection](configure-policy.md) pour les étiquettes qui appliquent une classification automatique, vous pouvez étiqueter les fichiers découverts par ce scanneur. Les étiquettes appliquent une classification et elles appliquent ou suppriment éventuellement la protection :

![Présentation de l’architecture du scanneur Azure Information Protection](../media/infoprotect-scanner.png)

Le scanneur peut inspecter les fichiers que Windows peut indexer à l’aide des iFilters installés sur l’ordinateur. Ensuite, pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise la détection de modèles et les types d’informations sensibles de protection contre la perte de données intégrée à Office 365 ou les modèles regex Office 365. Étant donné que le scanneur utilise le client Azure Information Protection, il peut classifier et protéger les mêmes [types de fichiers](../rms-client/client-admin-guide-file-types.md).

Vous pouvez exécuter le scanneur en mode découverte uniquement, dans lequel vous utilisez les rapports pour vérifier ce qui se passerait si les fichiers étaient étiquetés. Ou bien, vous pouvez exécuter le scanneur pour appliquer automatiquement les étiquettes. Vous pouvez également exécuter le scanneur pour découvrir les fichiers contenant des types d’informations sensibles, sans configurer d’étiquettes pour les conditions qui appliquent la classification automatique.

Notez que le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers dans les magasins de données que vous spécifiez. Vous pouvez configurer ce cycle pour s’exécuter une ou plusieurs fois.

Vous pouvez indiquer quels types de fichiers analyser ou exclure de l’analyse. Pour limiter les fichiers inspectés par le scanneur, définissez une liste de types de fichiers à l’aide de l’applet de commande [Set-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileType).


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prérequis pour le scanneur Azure Information Protection
Avant d’installer le scanneur Azure Information Protection, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Ordinateur Windows Server pour exécuter le service du scanneur :<br /><br />- Processeurs 4 cœurs<br /><br />- 4 Go de RAM<br /><br />- 10 Go d’espace libre (en moyenne) pour les fichiers temporaires|Windows Server 2016 ou Windows Server 2012 R2. <br /><br />Remarque : À des fins de test ou d’évaluation dans un environnement hors production, vous pouvez utiliser un système d’exploitation client Windows qui est [pris en charge par le client Azure Information Protection](../get-started/requirements.md#client-devices).<br /><br />Il peut s’agir d’un ordinateur physique ou virtuel doté d’une connexion réseau rapide et fiable aux magasins de données à scanner.<br /><br /> Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo. <br /><br />Vérifiez que cet ordinateur dispose de la [connectivité Internet](../get-started/requirements.md#firewalls-and-network-infrastructure) dont il a besoin pour Azure Information Protection. Si une connexion Internet n’est pas possible en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).|
|SQL Server pour stocker la configuration du scanneur :<br /><br />- Instance locale ou distante<br /><br />-Rôle sysadmin pour installer le scanneur|SQL Server 2012 est la version minimale pour les éditions suivantes :<br /><br />- SQL Server Entreprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Lorsque vous installez le scanneur et si votre compte a le rôle Sysadmin, le processus d’installation crée automatiquement la base de données AzInfoProtectionScanner et accorde le rôle db_owner requis au compte de service qui exécute le scanneur.  Si vous ne pouvez pas disposer du rôle Sysadmin ou si les stratégies de votre organisation requièrent que les bases de données soient créées et configurées manuellement, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).|
|Compte de service pour exécuter le service du scanneur|En plus d’exécuter le service du scanneur, ce compte s’authentifie auprès d’Azure AD, puis télécharge la stratégie Azure Information Protection. Ce compte doit être un compte Active Directory et synchronisé avec Azure AD. Si vous ne pouvez pas synchroniser ce compte en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />Ce compte de service a la configuration suivante :<br /><br />Droit d’- **ouverture de session locale**. Ce droit est exigé pour l’installation et la configuration du scanneur, mais pas pour son fonctionnement. Vous devez accorder ce droit au compte de service, mais vous pouvez le supprimer après avoir vérifié que le scanneur peut détecter, classifier et protéger des fichiers. Si l’attribution de ce droit, même pendant une courte période, n’est pas possible en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />Droit d’- **ouverture de session en tant que service**. Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur. <br /><br />- Autorisations d’accès aux dépôts de données : vous devez accorder des autorisations de **Lecture** et **Écriture** pour l’analyse des fichiers, puis l’application d’une classification et d’une protection aux fichiers qui remplissent les conditions stipulées dans la stratégie Azure Information Protection. Pour exécuter le scanneur en mode découverte uniquement, l’autorisation **Lecture** suffit.<br /><br />- Pour les étiquettes qui reprotègent ou retire la protection : pour veiller à ce que le scanneur ait toujours accès aux fichiers protégés, faites de ce compte un [super utilisateur](configure-super-users.md) du service Azure Rights Management et vérifiez que la fonctionnalité de super utilisateur est activée. Pour plus d’informations sur la configuration requise des comptes pour appliquer la protection, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](../plan-design/prepare.md). En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que ce compte est inclus dans les contrôles d’intégration que vous avez configurés.|
|Le client Azure Information Protection est installé sur l’ordinateur Windows Server|Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.<br /><br />Pour obtenir des instructions d’installation du client, consultez le [guide de l’administrateur](../rms-client/client-admin-guide.md). Si vous avez déjà installé le scanneur et que vous devez maintenant le mettre à niveau vers une version ultérieure, consultez [Mise à niveau du scanneur Azure Information Protection](../rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|
|Étiquettes configurées qui appliquent une classification automatique et éventuellement une protection|Pour plus d’informations sur la manière de configurer les conditions dans la stratégie Azure Information Protection, consultez [Guide pratique pour configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md).<br /><br />Pour plus d’informations sur la façon de configurer les étiquettes pour appliquer une protection aux fichiers, consultez [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md).<br /><br />Ces étiquettes peuvent être dans la stratégie globale, ou dans une ou plusieurs [stratégies délimitées](configure-policy-scope.md).<br /><br />Remarque : bien que vous puissiez exécuter le scanneur même si vous n’avez pas configuré les étiquettes qui appliquent la classification automatique, ce scénario n’est pas abordé dans ces instructions. [Plus d’informations](#using-the-scanner-with-alternative-configurations)| 

Si vous ne pouvez pas respecter toutes les conditions dans la table, car votre organisation l’interdit, consultez la section suivante pour obtenir des alternatives.

Si toutes les conditions requises sont remplies, passez directement à la [section sur l’installation](#install-the-azure-information-protection-scanner).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Déploiement du scanneur avec d’autres configurations

Les prérequis répertoriés dans la table correspondent aux exigences par défaut pour le scanneur et sont recommandés pour obtenir la configuration la plus simple pour le déploiement du scanneur. Ils doivent être adaptés aux tests initiaux, afin que vous puissiez vérifier les fonctionnalités du scanneur. Toutefois, dans un environnement de produit, les stratégies de votre organisation peuvent interdire ces exigences par défaut en raison d’une ou plusieurs des restrictions suivantes :

- Les serveurs ne sont pas autorisés à se connecter à Internet

- Vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

- Les comptes de service ne peut pas obtenir le droit **Ouvrir une session localement**

- Les comptes de service ne peuvent pas être synchronisés avec Azure Active Directory, mais les serveurs ont accès à Internet

Le scanneur peut prendre en charge ces restrictions, mais celles-ci nécessitent une configuration supplémentaire.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction : le serveur du scanneur n’est pas autorisé à se connecter à Internet

Suivez les instructions pour un [ordinateur déconnecté](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). 

Notez que dans cette configuration, le scanneur ne peut pas appliquer la protection (ou supprimer la protection) à l’aide de la clé cloud de votre organisation. Au lieu de cela, le scanneur est limité à l’utilisation d’étiquettes qui appliquent la classification uniquement, ou la protection qui utilise [HYOK](configure-adrms-restrictions.md). 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

Si le rôle Sysadmin peut vous être attribué temporairement pour installer le scanneur, vous pouvez supprimer ce rôle lorsque l’installation du scanneur est terminée. Lorsque vous utilisez cette configuration, la base de données est automatiquement créée pour vous et le compte de service du scanneur obtient automatiquement les autorisations nécessaires. Toutefois, le compte utilisateur qui configure le scanneur nécessite le rôle db_owner pour la base de données AzInfoProtectionScanner, et vous devez attribuer manuellement ce rôle au compte utilisateur.

Si vous ne pouvez pas obtenir le rôle Sysadmin même temporairement, vous devez créer manuellement une base de données nommée AzInfoProtectionScanner avant d’installer le scanneur. Lorsque vous utilisez cette configuration, attribuez les rôles suivants :
    
|Compte|Rôle au niveau de la base de données|
|--------------------------------|---------------------|
|Compte de service pour le scanneur|db_owner|
|Compte utilisateur pour l’installation du scanneur|db_owner|
|Compte utilisateur pour la configuration du scanneur |db_owner|

En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Mais si vous utilisez des comptes différents, ils ont tous les deux besoin du rôle db_owner pour la base de données AzInfoProtectionScanner.

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restriction : le compte de service pour le scanneur ne peut pas obtenir le droit **Ouvrir une session localement**

Si les stratégies de votre organisation interdisent le droit **Ouvrir une session localement** pour les comptes de service, mais autorisent le droit **Se connecter en tant que traitement par lots**, suivez les instructions sous [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) dans le guide de l’administrateur.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory, mais le serveur a accès à Internet

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- Pour le compte de service du scanneur, vous pouvez utiliser un compte Windows local ou un compte Active Directory.

- Pour le compte Azure Active Directory, suivez les instructions sous [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) dans le guide de l’administrateur.


## <a name="install-the-azure-information-protection-scanner"></a>Guide pratique pour installer le scanneur Azure Information Protection

1. Connectez-vous à l’ordinateur Windows Server qui exécutera le scanneur. Utilisez un compte disposant de droits d’administrateur local et qui est autorisé à écrire dans la base de données principale SQL Server.

2. Ouvrez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Exécutez l’applet de commande [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), en spécifiant l’instance de SQL Server où créer une base de données pour le scanneur Azure Information Protection : 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    Exemples :
    
    Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`
    
    Utilisez l’aide en ligne de cette applet de commande si vous avez besoin d’autres [exemples détaillés](/powershell/module/azureinformationprotection/install-aipscanner#examples).
    
    Quand vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur (\<domaine\nom d’utilisateur>) et le mot de passe.

4. Vérifiez que le service est maintenant installé en utilisant **Outils d’administration** > **Services**. 
    
    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie afin de pouvoir s’exécuter sans assistance. 

## <a name="get-an-azure-ad-token-for-the-scanner-service-account-to-authenticate-to-the-azure-information-protection-service"></a>Obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie auprès du service Azure Information Protection

1. À partir du même ordinateur Windows Server ou à partir de votre bureau, connectez-vous au portail Azure pour créer deux applications Azure AD nécessaires pour spécifier un jeton d’accès à des fins d’authentification. Après une connexion interactive initiale, ce jeton permet au scanneur de s’exécuter de manière non interactive.
    
    Pour créer ces applications, suivez les instructions données dans [Guide pratique pour étiqueter des fichiers de manière non interactive pour Azure Information Protection](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) dans le guide de l’administrateur.

2. À partir de l’ordinateur Windows Server, si votre compte de service de scanneur a reçu l’autorisation **Ouvrir une session localement** pour l’installation : connectez-vous avec ce compte et démarrez une session PowerShell. Exécutez [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), en spécifiant les valeurs copiées à partir de l’étape précédente :
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```
    
    Lorsque vous y êtes invité, spécifiez le mot de passe des informations d’identification de votre compte de service pour Azure AD, puis cliquez sur **Accepter**.
    
    Si l’autorisation **Ouvrir une session localement** ne peut pas être accordée à votre compte de service de scanneur pour l’installation : suivez les instructions de la section [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) du guide de l’administrateur. 

Le scanneur a maintenant un jeton pour s’authentifier auprès d’Azure AD, lequel jeton est valide pendant un an, deux ans, ou définitivement (il n’expire jamais), selon votre configuration de l’**application web/API** dans Azure AD. Quand le jeton expire, vous devez répéter les étapes 1 et 2.

Vous êtes maintenant prêt à spécifier les magasins de données à analyser. 

## <a name="specify-data-stores-for-the-azure-information-protection-scanner"></a>Spécifier des magasins de données pour le scanneur Azure Information Protection

Utilisez l’applet de commande [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository) pour spécifier les magasins de données à analyser à l’aide du scanneur Azure Information Protection. Vous pouvez spécifier des dossiers locaux, des chemins UNC et des URL SharePoint Server de sites et bibliothèques SharePoint. 

Versions prises en charge pour SharePoint : SharePoint Server 2016 et SharePoint Server 2013.

1. À partir du même ordinateur Windows Server, dans votre session PowerShell, ajoutez votre premier magasin de données en exécutant la commande suivante :
    
        Add-AIPScannerRepository -Path <path>
    
    Par exemple : `Add-AIPScannerRepository -Path \\NAS\Documents`
    
    Pour obtenir d’autres exemples, consultez l’[aide en ligne](/powershell/module/azureinformationprotection/Add-AIPScannerRepository#examples) de cette applet de commande.

2. Répétez cette commande pour tous les magasins de données à analyser. Si vous avez besoin de supprimer un magasin de données que vous avez ajouté, utilisez l’applet de commande [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository).

3. Vérifiez que vous avez spécifié tous les magasins de données correctement en exécutant l’applet de commande [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository) :
    
        Get-AIPScannerRepository

Avec la configuration par défaut du scanneur, vous êtes maintenant prêt à exécuter votre première analyse en mode découverte.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-azure-information-protection-scanner"></a>Exécuter un cycle de découverte et afficher les rapports du scanneur Azure Information Protection

1. En utilisant **Outils d’administration** > **Services**, démarrez le service **Scanneur Azure Information Protection**.

2. Attendez que le scanneur termine son cycle. Une fois que le scanneur a parcouru tous les fichiers inclus dans les magasins de données que vous avez spécifiés, le service s’arrête. Vous pouvez utiliser le journal des événements **Applications et service** Windows local, **Azure Information Protection**, pour vérifier que le service est arrêté. Recherchez l’ID d’événement d’information **911**.

3. Passez en revue les rapports stockés dans %*localappdata*%\Microsoft\MSIP\Scanner\Reports et dont le format de fichier est .csv. Avec la configuration par défaut du scanneur, seuls les fichiers qui remplissent les conditions de la classification automatique sont inclus dans ces rapports.
    
    Si les résultats ne correspondent pas à ce que vous attendez, vous devez peut-être ajuster les conditions que vous avez spécifiées dans votre stratégie Azure Information Protection. Si tel est le cas, répétez les étapes 1 à 3 jusqu’à ce que vous soyez prêt à modifier la configuration pour appliquer la classification et éventuellement la protection. Chaque fois que vous répétez ces étapes, commencez par exécuter la commande PowerShell suivante sur l’ordinateur Windows Server :
    
        Set-AIPScannerConfiguration -Schedule OneTime

Quand vous êtes prêt à étiqueter automatiquement les fichiers que le scanneur découvre, passez à la procédure suivante. 

## <a name="configure-the-azure-information-protection-scanner-to-apply-classification-and-protection-to-discovered-files"></a>Configurer le scanneur Azure Information Protection pour appliquer une classification et une protection aux fichiers découverts

Dans son paramétrage par défaut, le scanneur s’exécute une seule fois en mode création de rapports uniquement. Pour modifier ces paramètres, exécutez l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

1. Sur l’ordinateur Windows Server, dans la session PowerShell, exécutez la commande suivante :
       
        Set-AIPScannerConfiguration -Enforce On -Schedule Continuous
    
    Il existe d’autres paramètres de configuration que vous pouvez modifier. Par exemple, si les attributs de fichier sont modifiés et ce qui est enregistré dans les rapports. De plus, si votre stratégie Azure Information Protection inclut le paramètre qui exige un message de justification pour diminuer le niveau de classification ou supprimer la protection, spécifiez ce message à l’aide de cette applet de commande. Utilisez l’[aide en ligne](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters) pour plus d’informations sur chaque paramètre de configuration. 

2. En utilisant **Outils d’administration** > **Services**, redémarrez le service **Scanneur Azure Information Protection**.

3. Comme avant, examinez le journal des événements et les rapports pour déterminer quels fichiers ont été étiquetés, quelle classification a été appliquée et si une protection a été appliquée.

Puisque nous avons configuré la planification pour qu’elle s’exécute en continu, quand le scanneur a parcouru tous les fichiers, il démarre un nouveau cycle pour découvrir les fichiers nouveaux et modifiés.


## <a name="how-files-are-scanned-by-the-azure-information-protection-scanner"></a>Analyse des fichiers par le scanneur Azure Information Protection

Le scanneur ignore automatiquement les fichiers qui sont [exclus de la classification et de la protection](../rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-client), comme les fichiers exécutables et les fichiers système.

Vous pouvez modifier ce comportement en définissant une liste de types de fichiers à analyser ou à exclure de l’analyse. Lorsque vous définissez cette liste sans spécifier de référentiel de données, la liste s’applique à tous les référentiels de données qui n’ont pas leur propre liste spécifiée. Pour définir cette liste, utilisez l’applet de commande [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileType). Après avoir spécifié votre liste de types de fichiers, vous pouvez ajouter un nouveau type de fichier à l’aide de l’applet de commande [Add-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileType) et en supprimer un à l’aide de l’applet de commande [Remove-AIPScannerScannedFileType](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileType).

Puis le scanneur utilise Windows iFilter pour analyser les types de fichiers suivants. Pour ces types de fichiers, le document est étiqueté selon les conditions que vous avez spécifiées pour vos étiquettes.

|Type d'application|Type de fichier|
|--------------------------------|-------------------------------------|
|Word|.docx ; .docm ; .dotm ; .dotx|
|Excel|.xls ; .xlt ; .xlsx ; .xltx ; .xltm ; .xlsm ; .xlsb|
|PowerPoint|.ppt ; .pps ; .pot ; .pptx ; .ppsx ; .pptm ; .ppsm ; .potx ; .potm|
|Projet|.mpp ; .mpt|
|PDF|.pdf|
|Text|.txt ; .xml ; .csv|


Enfin, pour les autres types de fichiers, le scanneur applique l’étiquette par défaut de la stratégie Azure Information Protection, ou l’étiquette par défaut que vous configurez pour le scanneur.

|Type d'application|Type de fichier|
|--------------------------------|-------------------------------------|
|Projet|.mpp ; .mpt|
|Éditeur|.pub|
|Visio|.vsd ; .vdw ; .vst ; .vss ; .vsdx ; .vsdm ; .vssx ; .vssm ; .vstx ; .vstm|
|XPS|.xps ; .oxps ; .dwfx|
|SolidWorks|.sldprt ; .slddrw ; .sldasm|
|JPEG |.jpg ; .jpeg ; .jpe ; .jif ; .jfif ; .jfi|
|PNG |.png|
|GIF|.gif|
|Bitmap|.bmp ; .giff|
|TIFF|.tif ; .tiff|
|Photoshop|.psdv|
|DigitalNegative|.dng|
|Pfile|.pfile|

Lorsque le scanneur applique une étiquette avec une protection, par défaut, seuls les types de fichiers Office sont protégés. Vous pouvez modifier ce comportement afin que les autres types de fichiers soient protégés. Toutefois, lorsqu’une étiquette applique une protection générique à des documents, l’extension de nom de fichier devient .pfile. En outre, le fichier est en lecture seule jusqu’à ce qu’il soit ouvert par un utilisateur autorisé et enregistré dans son format natif. Les fichiers texte et les images peuvent également modifier leur extension de nom de fichier et passer en lecture seule. 

Pour modifier le comportement par défaut du scanneur, par exemple, afin de protéger de façon générique d’autres types de fichiers, vous devez modifier manuellement le Registre et indiquer les types de fichiers supplémentaires qui doivent être protégés. Pour obtenir des instructions, consultez [Configuration de l’API de fichier](../develop/file-api-configuration.md) dans le Guide du développeur. Dans cette documentation pour les développeurs, la protection générique est appelée « PFile »

## <a name="when-files-are-rescanned-by-the-azure-information-protection-scanner"></a>Quand les fichiers sont rescannés par le scanneur Azure Information Protection

Pour le premier cycle d’analyse, le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, il inspecte uniquement les fichiers nouveaux ou modifiés. 

Vous pouvez forcer le scanneur à réinspecter tous les fichiers en exécutant [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) avec le paramètre `-Type` défini sur **Complet**. Cette configuration est utile quand vous voulez que les rapports contiennent tous les fichiers. Elle est généralement utilisée lorsque le scanneur s’exécute en mode découverte. Lorsqu’une analyse complète est terminée, le scanneur passe automatiquement en mode incrémentiel pour inspecter uniquement les fichiers nouveaux ou modifiés lors des analyses suivantes.

De plus, tous les fichiers sont inspectés quand le scanneur télécharge une stratégie Azure Information Protection qui présente des conditions nouvelles ou modifiées. Le scanneur actualise la stratégie toutes les heures, quand le service démarre et que la stratégie remonte à plus d’une heure.  

> [!TIP]
> Si vous avez besoin d’actualiser la stratégie avant cet intervalle d’une heure, par exemple, pendant une période de test : supprimez manuellement le fichier de stratégie **Policy.msip** de **%LocalAppData%\Microsoft\MSIP\Policy.msip** et de **%LocalAppData%\Microsoft\MSIP\Scanner**. Ensuite, redémarrez le service du scanneur Azure Information Protection.
> 
> Si vous avez changé les paramètres de protection de la stratégie, attendez 15 minutes après l’enregistrement des paramètres de protection avant de redémarrer le service.

Si le scanneur a téléchargé une stratégie sans conditions automatiques, la copie du fichier de stratégie dans le dossier du scanneur n’est pas mise à jour. Dans ce scénario, vous devez supprimer le fichier de stratégie **Policy.msip** dans **%LocalAppData%\Microsoft\MSIP\Policy.msip** et dans **%LocalAppData%\Microsoft\MSIP\Scanner** pour que le scanneur puisse utiliser un fichier de stratégie récemment téléchargé avec des étiquettes correctement configurées pour les conditions automatiques.

## <a name="using-the-scanner-with-alternative-configurations"></a>Utilisation du scanneur avec d’autres configurations

Il existe deux scénarios pris en charge par le scanneur dans lesquels il n’est pas nécessaire que des étiquettes soient configurées pour des conditions quelles qu’elles soient : 

- Appliquer une étiquette par défaut à tous les fichiers dans un référentiel de données.
    
    Pour cette configuration, utilisez l’applet de commande [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) et définissez le paramètre *MatchPolicy* sur **Off**. 
    
    Le contenu des fichiers n’est pas inspecté et tous les fichiers du référentiel de données sont étiquetés avec l’étiquette par défaut que vous spécifiez pour le référentiel de données (avec le paramètre *SetDefaultLabel*) ou si celle-ci n’est pas spécifié, l’étiquette par défaut qui est spécifiée comme paramètre de stratégie pour le compte d’analyse.
    

- Identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.
    
    Pour cette configuration, utilisez l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) et définissez le paramètre *DiscoverInformationTypes* sur **All**.
    
    Le scanneur utilise toute condition personnalisée que vous avez spécifiée pour les étiquettes dans la stratégie Azure Information Protection et la liste des types d’informations qui sont disponibles pour les étiquettes dans la stratégie Azure Information Protection. 

## <a name="optimizing-the-performance-of-the-azure-information-protection-scanner"></a>Optimisation des performances de l’analyseur Azure Information Protection

Pour optimiser les performances de l’analyseur :

- **Veillez à avoir une connexion haut débit fiable entre l’ordinateur de l’analyseur et le magasin de données analysé**
    
    Par exemple, placez l’ordinateur de l’analyseur dans le même réseau local ou (de préférence) dans le même segment réseau que le magasin de données analysé.
    
    La qualité de la connexion réseau affecte les performances de l’analyseur parce que pour examiner les fichiers, celui-ci transfère le contenu des fichiers à l’ordinateur exécutant son service. Quand vous réduisez (ou supprimez) le nombre de tronçons réseau que ces données doivent traverser, vous réduisez également la charge sur votre réseau. 

- **Assurez-vous que l’ordinateur de l’analyseur dispose de ressources processeur**
    
    L’inspection du contenu des fichiers à la recherche d’une correspondance avec vos conditions de configuration ainsi que le chiffrement et le déchiffrement des fichiers sont des actions qui sollicitent le processeur de manière intense. Surveillez les cycles d’analyse standard de vos magasins de données spécifiés pour déterminer si un manque de ressources processeur affecte les performances de l’analyseur.
    
- **N’analysez pas les dossiers locaux sur l’ordinateur exécutant le service de l’analyseur**
    
    Si vous avez des dossiers à analyser sur un serveur Windows, installez l’analyseur sur un autre ordinateur et configurez ces dossiers comme partages réseau à analyser. En séparant les deux fonctions d’hébergement des fichiers et d’analyse des fichiers, les ressources informatiques de ces services n’entrent pas en concurrence.

Autres facteurs qui affectent les performances de l’analyseur :

- La charge actuelle et les temps de réponse des magasins de données qui contiennent les fichiers à analyser

- Si l’analyseur s’exécute en mode découverte ou en mode d’application
    
    Le mode découverte a généralement un taux d’analyse plus élevé que le mode d’application, car la découverte nécessite une seule action de lecture de fichier tandis que le mode d’application nécessite des actions de lecture et d’écriture.

- Le changement des conditions d’Azure Information Protection
    
    Votre premier cycle d’analyse quand l’analyseur doit inspecter chaque fichier prend bien évidemment plus temps que les cycles d’analyse suivants qui, par défaut, inspectent uniquement les fichiers nouveaux et modifiés. Toutefois, si vous changez les conditions dans la stratégie Azure Information Protection, tous les fichiers sont réanalysés, comme décrit dans la [section précédente](#when-files-are-rescanned-by-the-azure-information-protection-scanner).

- Le niveau de journalisation que vous avez choisi
    
    Vous pouvez choisir entre **Déboguer**, **Information**, **Erreur** et **Désactivé** pour les rapports de l’analyseur. Avec **Désactivé**, vous bénéficiez des meilleures performances alors qu’avec **Déboguer**, l’analyseur est considérablement ralenti et doit être utilisé uniquement pour le dépannage. Pour plus d’informations, consultez le paramètre *ReportLevel* de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- Les fichiers eux-mêmes :
    
    - Les fichiers Office sont analysés plus rapidement que les fichiers PDF.
    
    - Les fichiers non protégés sont plus rapides à analyser que les fichiers protégés.
    
    - Les gros fichiers prennent évidemment plus de temps à analyser que les petits fichiers.

- En outre :
    
    - Vérifiez que le compte de service qui exécute le scanneur dispose seulement des droits documentés dans la section [prérequis du scanneur](#prerequisites-for-the-azure-information-protection-scanner), puis configurez la [propriété client avancée](../rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) de manière à désactiver le niveau d’intégrité faible pour le scanneur.
    
    - Le scanneur s’exécute plus rapidement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour appliquer une étiquette par défaut à tous les fichiers, car le scanneur n’inspecte pas le contenu du fichier.
    
    - Le scanneur s’exécute plus lentement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour identifier toutes les conditions personnalisées et les types d’informations sensibles connus.
    

## <a name="list-of-cmdlets-for-the-azure-information-protection-scanner"></a>Liste des applets de commande pour le scanneur Azure Information Protection 

D’autres applets de commande propres au scanneur vous permettent de modifier son compte de service et sa base de données, d’obtenir ses paramètres actuels et de désinstaller son service. Le scanneur utilise les applets de commande suivantes :

- [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes)

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes)

- [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)


## <a name="event-log-ids-and-descriptions"></a>ID du journal des événements et descriptions

Utilisez les sections suivantes pour identifier les ID d’événement possibles et les descriptions du scanneur. Ces événements sont journalisés sur le serveur qui exécute le service de scanneur, dans le journal des événements **Applications et services** Windows, **Azure Information Protection**.

-----

Informations **910**

**Cycle du scanneur démarré.**

Cet événement est enregistré lorsque le service du scanneur est démarré et qu’il commence à analyser les fichiers inclus dans les dépôts de données que vous avez spécifiés.

----

Informations **911**

**Cycle du scanneur terminé.**

Cet événement est enregistré lorsque le scanneur a terminé son analyse ponctuelle depuis le démarrage du serveur ou qu’il a terminé un cycle dans le cadre d’une planification continue.

Si le scanneur a été configuré pour s’exécuter une seule fois, plutôt que de manière continue, pour rescanner les fichiers, vous devez définir une planification **Une fois** ou **Continue**, puis redémarrer manuellement le service. Pour changer la planification, utilisez l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) et le paramètre **Schedule**.

----

## <a name="next-steps"></a>Étapes suivantes

Vous vous demandez peut-être : [Quelle différence y a-t-il entre l’ICF de Windows Server et le scanneur d’Azure Information Protection ?](../get-started/faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur tous les scénarios qui utilisent PowerShell, consultez [Utiliser PowerShell avec le client Azure Information Protection](../rms-client/client-admin-guide-powershell.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
