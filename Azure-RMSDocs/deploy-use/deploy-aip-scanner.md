---
title: "Déployer le scanneur Azure Information Protection"
description: "Instructions pour installer, configurer et exécuter le scanneur Azure Information Protection qui permet de découvrir, classifier et protéger des fichiers sur des magasins de données."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 5df68e177d9e3d77a4fd9441e07f1779fa714b23
ms.sourcegitcommit: a63b3ac3949e66cc38e20d7f14ac129b8e3224c3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/09/2017
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers

>*S’applique à : Azure Information Protection, Windows Server 2016, Windows Server 2012 R2*

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et susceptible d’être modifiée.

Utilisez ces informations pour en savoir plus sur le scanneur Azure Information Protection, puis sur la manière de l’installer, de le configurer et de l’exécuter correctement. 

Ce scanneur s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les magasins de données suivants :

- Dossiers locaux sur l’ordinateur Windows Server qui exécute le scanneur.

- Chemins UNC des partages réseau qui utilisent le protocole CIFS (Common Internet File System).

- Sites et bibliothèques pour SharePoint Server 2016 et SharePoint Server 2013.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Présentation du scanneur Azure Information Protection

Quand vous avez configuré votre [stratégie Azure Information Protection](configure-policy.md) pour les étiquettes qui appliquent une classification automatique, vous pouvez étiqueter les fichiers découverts par ce scanneur. Les étiquettes appliquent une classification et elles appliquent ou suppriment éventuellement la protection :

![Présentation du scanneur Azure Information Protection](../media/infoprotect-scanner.png)

Le scanneur peut inspecter les fichiers que Windows peut indexer à l’aide des iFilters installés sur l’ordinateur. Ensuite, pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise la détection de modèles et les types d’informations sensibles de protection contre la perte de données intégrée à Office 365 ou les modèles regex Office 365. Étant donné que le scanneur utilise le client Azure Information Protection, il peut classifier et protéger les mêmes [types de fichiers](../rms-client/client-admin-guide-file-types.md).

Vous pouvez exécuter le scanneur en mode découverte uniquement, dans lequel vous utilisez les rapports pour vérifier ce qui se passerait si les fichiers étaient étiquetés. Ou bien, vous pouvez exécuter le scanneur pour appliquer automatiquement les étiquettes.

Notez que le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers dans les magasins de données que vous spécifiez. Vous pouvez configurer ce cycle pour s’exécuter une ou plusieurs fois.

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prérequis pour le scanneur Azure Information Protection
Avant d’installer le scanneur Azure Information Protection, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Plus d'informations|
|---------------|--------------------|
|Ordinateur Windows Server pour exécuter le service du scanneur :<br /><br />- 4 processus<br /><br />- 4 Go de RAM|Windows Server 2016 ou Windows Server 2012 R2. <br /><br />Remarque : À des fins de test ou d’évaluation dans un environnement hors production, vous pouvez utiliser un système d’exploitation client Windows qui est [pris en charge par le client Azure Information Protection](../get-started/requirements.md#client-devices).<br /><br />Il peut s’agir d’un ordinateur physique ou virtuel doté d’une connexion réseau rapide et fiable aux magasins de données à scanner. <br /><br />Vérifiez que cet ordinateur dispose de la [connectivité Internet](../get-started/requirements.md#firewalls-and-network-infrastructure) dont il a besoin pour Azure Information Protection. Ou bien, vous devez le configurer en tant qu’[ordinateur déconnecté](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). |
|SQL Server pour stocker la configuration du scanneur :<br /><br />- Instance locale ou distante|SQL Server 2012 R2 est la version minimale pour les éditions suivantes :<br /><br />- SQL Server Entreprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express|
|Compte de service pour exécuter le service du scanneur|Ce compte doit être un compte Active Directory synchronisé sur Azure AD, avec les conditions supplémentaires suivantes :<br /><br />Droit d’- **ouverture de session locale**. Ce droit est exigé pour l’installation et la configuration du scanneur, mais pas pour son fonctionnement. Vous devez accorder ce droit au compte de service, mais vous pouvez le supprimer après avoir vérifié que le scanneur peut détecter, classifier et protéger des fichiers.<br /><br />Droit d’- **ouverture de session en tant que service**. Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur. <br /><br />- Autorisations d’accès aux dépôts de données : vous devez accorder des autorisations de **Lecture** et **Écriture** pour l’analyse des fichiers, puis l’application d’une classification et d’une protection aux fichiers qui remplissent les conditions stipulées dans la stratégie Azure Information Protection. Pour exécuter le scanneur en mode découverte uniquement, l’autorisation **Lecture** suffit.<br /><br />- Pour les étiquettes qui reprotègent ou retire la protection : pour veiller à ce que le scanneur ait toujours accès aux fichiers protégés, faites de ce compte un [super utilisateur](configure-super-users.md) du service Azure Rights Management et vérifiez que la fonctionnalité de super utilisateur est activée. Pour plus d’informations sur la configuration requise des comptes pour appliquer la protection, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](../plan-design/prepare.md).|
|Le client Azure Information Protection est installé sur l’ordinateur Windows Server|Actuellement, le scanneur Azure Information Protection exige la préversion du client Azure Information Protection.<br /><br />Si vous préférez, vous pouvez installer le client uniquement avec le module PowerShell (AzureInformationProtection) utilisé pour installer et configurer le scanneur.<br /><br />Pour obtenir des instructions d’installation du client, consultez le [guide de l’administrateur](../rms-client/client-admin-guide.md).|
|Étiquettes configurées qui appliquent une classification automatique et éventuellement une protection|Pour plus d’informations sur la manière de configurer les conditions, consultez [Guide pratique pour configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](/deploy-use/configure-policy-classification.md).<br /><br />Pour plus d’informations sur la façon de configurer les étiquettes pour appliquer une protection aux fichiers, consultez [Guide pratique pour configurer une étiquette pour la protection Rights Management](../deploy-use/configure-policy-protection.md). |


## <a name="install-the-azure-information-protection-scanner"></a>Guide pratique pour installer le scanneur Azure Information Protection

1. En utilisant le compte de service que vous avez créé pour exécuter le scanneur, connectez-vous à l’ordinateur Windows Server qui va exécuter le scanneur.

2. Ouvrez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Exécutez l’applet de commande [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), en spécifiant l’instance de SQL Server sur laquelle créer une base de données pour le scanneur Azure Information Protection. Lorsque vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur (\<domaine\nom d’utilisateur>) et le mot de passe : 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    Exemples :
        
    - Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    - Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    - Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`

4. Vérifiez que le service est maintenant installé en utilisant **Outils d’administration** > **Services**. 
    
    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie afin de pouvoir s’exécuter sans assistance. 

## <a name="get-an-azure-ad-token-for-the-scanner-service-account-to-authenticate-to-the-azure-information-protection-service"></a>Obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie auprès du service Azure Information Protection

1. À partir du même ordinateur Windows Server ou à partir de votre bureau, connectez-vous au portail Azure pour créer deux applications Azure AD nécessaires pour spécifier un jeton d’accès à des fins d’authentification. Après une connexion interactive initiale, ce jeton permet au scanneur de s’exécuter de manière non interactive.
    
    Pour créer ces applications, suivez les instructions données dans [Guide pratique pour étiqueter des fichiers de manière non interactive pour Azure Information Protection](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) dans le guide de l’administrateur.

2. À partir de l’ordinateur Windows Server, toujours connecté avec le compte de service du scanneur, exécutez [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), en spécifiant les valeurs que vous avez copiées de l’étape précédente :
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```

3. Lorsque vous y êtes invité, spécifiez le mot de passe des informations d’identification de votre compte de service pour Azure AD, puis cliquez sur **Accepter**.

Le scanneur a maintenant un jeton pour s’authentifier auprès d’Azure AD, lequel jeton est valide pendant un an, deux ans, ou définitivement (il n’expire jamais), selon votre configuration de l’**application web/API** dans Azure AD. Quand le jeton expire, vous devez répéter les étapes 1 à 3.

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
    
        Set-AIPScannerConfiguration -ScanMode Enforce -Schedule Continuous
    
    Il existe d’autres paramètres de configuration que vous pouvez modifier. Par exemple, si les attributs de fichier sont modifiés et ce qui est enregistré dans les rapports. De plus, si votre stratégie Azure Information Protection inclut le paramètre qui exige un message de justification pour diminuer le niveau de classification ou supprimer la protection, spécifiez ce message à l’aide de cette applet de commande. Utilisez l’[aide en ligne](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters) pour plus d’informations sur chaque paramètre de configuration. 

2. En utilisant **Outils d’administration** > **Services**, redémarrez le service **Scanneur Azure Information Protection**.

3. Comme avant, examinez le journal des événements et les rapports pour déterminer quels fichiers ont été étiquetés, quelle classification a été appliquée et si une protection a été appliquée.

Puisque nous avons configuré la planification pour qu’elle s’exécute en continu, quand le scanneur a parcouru tous les fichiers, il démarre un nouveau cycle pour découvrir les fichiers nouveaux et modifiés.

## <a name="list-of-cmdlets-for-the-azure-information-protection-scanner"></a>Liste des applets de commande pour le scanneur Azure Information Protection 

D’autres applets de commande propres au scanneur vous permettent de modifier son compte de service et sa base de données, d’obtenir ses paramètres actuels et de désinstaller son service. Le scanneur utilise les applets de commande suivantes :

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

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

----

Informations **913**

**Le scanneur est arrêté car il a la valeur Jamais.**

Cet événement est journalisé quand le scanneur est configuré pour s’exécuter une seule fois plutôt qu’en continu. Le service du scanneur Azure Information Protection a donc été redémarré manuellement depuis le démarrage de l’ordinateur.  

Pour rescanner les fichiers, vous devez définir une planification **Une fois** ou **Continue**, puis redémarrer manuellement le service. Pour changer la planification, utilisez l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) et le paramètre **Schedule**.

----

Erreur **912**

**Une erreur inconnue s’est produite.**

Des informations supplémentaires sont enregistrées dans le rapport détaillé stocké dans %localappdata%\Microsoft\MSIP\Scanner\Reports\DetailedReport_AAAA_MM_JJ_HH_MM.csv.

Contact le [Support Microsoft](../get-started/information-support.md#to-contact-microsoft-support) si cet événement persiste à s’enregistrer. 

----

Erreur **914**

**Le service a été automatiquement arrêté en raison d’une configuration incorrecte : le fichier de stratégie est manquant ou endommagé.**

Cet événement est enregistré lorsque le client Azure Information Protection ne dispose pas d’un fichier de stratégie valide que le scanneur peut exécuter.

La stratégie Azure Information Protection est stockée dans %localappdata%\Microsoft\MSIP. Vous devez la configurer avec des étiquettes qui comprennent des conditions pour appliquer une classification automatique. Ou la stratégie doit être configurée pour une étiquette par défaut.

Vérifiez que les pare-feu ne bloquent pas la connexion à Internet nécessaire. Pour plus d’informations, consultez la configuration requise pour les [Pare-feu et infrastructure réseau](../get-started/requirements.md#firewalls-and-network-infrastructure) pour Azure Information Protection. Si aucune connexion Internet n’est possible, suivez les instructions de prise en charge des [ordinateurs déconnectés](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers).


## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur tous les scénarios qui utilisent PowerShell, consultez [Utiliser PowerShell avec le client Azure Information Protection](../rms-client/client-admin-guide-powershell.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]