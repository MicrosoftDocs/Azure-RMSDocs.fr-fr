---
title: Déployer le scanneur Azure Information Protection - AIP
description: Instructions pour installer, configurer et exécuter la version actuelle du scanneur Azure Information Protection pour découvrir, classifier et protéger des fichiers sur des magasins de données.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 9fcc7f157ef5fa562993b70a4b30db1556921272
ms.sourcegitcommit: 1218fad71850f3ea81cd12062544cfbc5a094764
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263991"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Cet article concerne la version en disponibilité générale actuelle du scanneur Azure Information Protection.
> 
> Pour mettre à niveau à partir d’une version en disponibilité générale du scanneur est antérieure à 1.48.204.0, consultez [la mise à niveau le scanneur Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner). Vous pouvez ensuite utiliser les instructions dans cette page, en omettant l’étape pour installer le scanneur.
> 
> Si vous n’êtes pas prêt à mettre à niveau à partir d’une version antérieure, consultez [déploiement de versions précédentes du scanneur Azure Information Protection pour classifier et protéger les fichiers automatiquement](deploy-aip-scanner-previousversions.md).


Utilisez ces informations pour en savoir plus sur le scanneur Azure Information Protection, puis sur la manière de l’installer, de le configurer et de l’exécuter correctement.

Ce scanneur s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les magasins de données suivants :

- Dossiers locaux sur l’ordinateur Windows Server qui exécute le scanneur.

- Chemins UNC pour les partages réseau qui utilisent le protocole SMB (Server Message Block).

- Sites et bibliothèques pour SharePoint Server 2019 via SharePoint Server 2013. SharePoint 2010 est également pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Pour analyser et étiqueter des fichiers sur des référentiels cloud, utilisez [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) au lieu du scanneur.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Présentation du scanneur Azure Information Protection

Quand vous avez configuré votre [stratégie Azure Information Protection](configure-policy.md) pour les étiquettes qui appliquent une classification automatique, vous pouvez étiqueter les fichiers découverts par ce scanneur. Les étiquettes appliquent une classification et elles appliquent ou suppriment éventuellement la protection :

![Présentation de l’architecture du scanneur Azure Information Protection](./media/infoprotect-scanner.png)

Le scanneur peut inspecter tous les fichiers que Windows est capable d’indexer à l’aide de filtres IFilter installés sur l’ordinateur. Ensuite, pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise la détection de modèles et les types d’informations sensibles de protection contre la perte de données intégrée à Office 365 ou les modèles regex Office 365. Étant donné que le scanneur utilise le client Azure Information Protection, il peut classifier et protéger les mêmes [types de fichiers](./rms-client/client-admin-guide-file-types.md).

Vous pouvez exécuter le scanneur en mode découverte uniquement, dans lequel vous utilisez les rapports pour vérifier ce qui se passerait si les fichiers étaient étiquetés. Ou bien, vous pouvez exécuter le scanneur pour appliquer automatiquement les étiquettes. Vous pouvez également exécuter le scanneur pour découvrir les fichiers contenant des types d’informations sensibles, sans configurer d’étiquettes pour les conditions qui appliquent la classification automatique.

Notez que le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers dans les magasins de données que vous spécifiez. Vous pouvez configurer ce cycle pour s’exécuter une ou plusieurs fois.

Vous pouvez spécifier les types de fichiers à analyser, ou à exclure de l’analyse, en définissant une liste de types de fichiers dans le cadre de la configuration du scanneur.


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prérequis pour le scanneur Azure Information Protection
Avant d’installer le scanneur Azure Information Protection, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Ordinateur Windows Server pour exécuter le service du scanneur :<br /><br />- Processeurs 4 cœurs<br /><br />- 8 Go de RAM<br /><br />- 10 Go d’espace libre (en moyenne) pour les fichiers temporaires|Windows Server 2019, Windows Server 2016 ou Windows Server 2012 R2. <br /><br />Remarque : À des fins de test ou d’évaluation dans un environnement hors production, vous pouvez utiliser un système d’exploitation client Windows qui est [pris en charge par le client Azure Information Protection](requirements.md#client-devices).<br /><br />Il peut s’agir d’un ordinateur physique ou virtuel doté d’une connexion réseau rapide et fiable aux magasins de données à scanner.<br /><br /> Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo. <br /><br />Si une connexion Internet n’est pas possible en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations). Sinon, assurez-vous que cet ordinateur dispose d’une connectivité Internet qui autorise les URL suivantes sur HTTPS (port 443) :<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|Compte de service pour exécuter le service du scanneur|En plus d’exécuter le service du scanneur sur l’ordinateur Windows Server, ce compte Windows s’authentifie auprès d’Azure AD, puis télécharge la stratégie Azure Information Protection. Ce compte doit être un compte Active Directory et synchronisé avec Azure AD. Si vous ne pouvez pas synchroniser ce compte en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />Ce compte de service a la configuration suivante :<br /><br />- **Ouvrir une session localement**, attribution des droits utilisateur. Ce droit est exigé pour l’installation et la configuration du scanneur, mais pas pour son fonctionnement. Vous devez accorder ce droit au compte de service, mais vous pouvez le supprimer après avoir vérifié que le scanneur peut détecter, classifier et protéger des fichiers. Si l’attribution de ce droit, même pendant une courte période, n’est pas possible en raison des stratégies de votre organisation, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />- **Ouvrir une session en tant que service**, attribution des droits utilisateur. Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur. <br /><br />- Autorisations sur les référentiels de données : Vous devez accorder les autorisations **Lecture** et **Écriture** pour l’analyse des fichiers, puis pour l’application d’une classification et d’une protection aux fichiers qui remplissent les conditions spécifiées dans la stratégie Azure Information Protection. Pour exécuter le scanneur en mode découverte uniquement, l’autorisation **Lecture** suffit.<br /><br />- Pour les étiquettes qui reprotègent ou suppriment la protection : Pour que le scanneur ait toujours accès aux fichiers protégés, faites de ce compte un [super utilisateur](configure-super-users.md) du service Azure Rights Management et vérifiez que la fonctionnalité de super utilisateur est activée. Pour plus d’informations sur la configuration requise des comptes pour appliquer la protection, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md). En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que ce compte est inclus dans les contrôles d’intégration que vous avez configurés.|
|SQL Server pour stocker la configuration du scanneur :<br /><br />- Instance locale ou distante<br /><br />-Rôle sysadmin pour installer le scanneur|SQL Server 2012 est la version minimale pour les éditions suivantes :<br /><br />- SQL Server Entreprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance SQL Server lorsque vous spécifiez un nom de profil personnalisé pour le scanneur.<br /><br />Lorsque vous installez le scanneur et si votre compte a le rôle Sysadmin, le processus d’installation crée automatiquement la base de données de configuration du scanneur et accorde le rôle db_owner requis au compte de service qui exécute le scanneur. Si vous ne pouvez pas disposer du rôle Sysadmin ou si les stratégies de votre organisation requièrent que les bases de données soient créées et configurées manuellement, consultez la section [Déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).<br /><br />La taille de la base de données de configuration varie pour chaque déploiement, mais nous vous recommandons d’allouer 500 Mo pour chaque lot de 1 000 000 fichiers que vous souhaitez analyser. |
|Le client Azure Information Protection est installé sur l’ordinateur Windows Server|Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.<br /><br />Pour obtenir des instructions d’installation du client, consultez le [guide de l’administrateur](./rms-client/client-admin-guide.md). Si vous avez déjà installé le scanneur et que vous devez maintenant le mettre à niveau vers une version ultérieure, consultez [Mise à niveau du scanneur Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|
|Étiquettes configurées qui appliquent une classification automatique et éventuellement une protection|Pour plus d’informations sur la configuration d’une étiquette de conditions et pour appliquer la protection :<br /> - [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)<br /> - [Comment configurer une étiquette pour la protection Rights Management](configure-policy-protection.md) <br /><br />Conseil : Vous pouvez utiliser les instructions du [didacticiel](infoprotect-quick-start-tutorial.md) pour tester le scanneur avec une étiquette qui recherche des numéros de carte de crédit dans un document Word préparé. Vous devez toutefois modifier la configuration de l’étiquette afin que **Sélectionner comment cette étiquette est appliquée** soit défini sur **Automatique** plutôt que sur **Recommandé**. Supprimez ensuite l’étiquette du document (si elle est appliquée), puis copiez le fichier dans un référentiel de données pour le scanneur. Pour effectuer un test rapide, il peut s’agir d’un dossier local sur l’ordinateur du scanneur.<br /><br /> Bien que vous puissiez exécuter le scanneur même si vous n’avez pas configuré les étiquettes qui appliquent la classification automatique, ce scénario n’est pas abordé dans ces instructions. [Plus d’informations](#using-the-scanner-with-alternative-configurations)|
|Pour les sites et bibliothèques SharePoint à analyser :<br /><br />-SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|D’autres versions de SharePoint ne sont pas prises en charge pour le scanneur.<br /><br />Pour les grandes batteries de serveurs SharePoint, regardez si vous devez augmenter le seuil d’affichage de liste (par défaut, 5 000) pour le scanneur pour accéder à tous les fichiers. Pour plus d’informations, consultez la documentation suivante de SharePoint : [Gérer des listes et bibliothèques de grande taille dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Pour scanner des documents Office :<br /><br />- formats de fichier 97-2003 et formats Office Open XML pour Word, Excel et PowerPoint|Pour plus d’informations sur les types de fichiers pris en charge par le scanneur pour ces formats de fichiers, consultez [Types de fichiers pris en charge par le client Azure Information Protection](./rms-client/client-admin-guide-file-types.md).|
|Pour les chemins longs :<br /><br />- 260 caractères maximum, sauf si le scanneur est installé sur Windows 2016 et que l’ordinateur est configuré pour prendre en charge les chemins longs.|Windows 10 et Windows Server 2016 prennent en charge les chemins de plus de 260 caractères avec le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) suivant : **Stratégie de l’ordinateur local** > **Configuration ordinateur** > **modèles d’administration** > **tous les paramètres**  >  **Win32 activer les chemins d’accès longs**<br /><br /> Pour plus d’informations sur la prise en charge des chemins de fichiers longs, consultez la section consacrée à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

Si vous ne pouvez pas respecter toutes les conditions dans la table, car votre organisation l’interdit, consultez la section suivante pour obtenir des alternatives.

Si toutes les conditions requises sont remplies, passez directement à la [section sur la configuration du scanneur](#configure-the-scanner-in-the-azure-portal).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Déploiement du scanneur avec d’autres configurations

Les prérequis répertoriés dans la table correspondent aux exigences par défaut pour le scanneur et sont recommandés pour obtenir la configuration la plus simple pour le déploiement du scanneur. Ils doivent être adaptés aux tests initiaux, afin que vous puissiez vérifier les fonctionnalités du scanneur. Toutefois, dans un environnement de produit, les stratégies de votre organisation peuvent interdire ces exigences par défaut en raison d’une ou plusieurs des restrictions suivantes :

- Les serveurs ne sont pas autorisés à se connecter à Internet

- Vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

- Les comptes de service ne peut pas obtenir le droit **Ouvrir une session localement**

- Les comptes de service ne peuvent pas être synchronisés avec Azure Active Directory, mais les serveurs ont accès à Internet

Le scanneur peut prendre en charge ces restrictions, mais celles-ci nécessitent une configuration supplémentaire.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction : Le serveur du scanneur n’est pas autorisé à se connecter à Internet

Suivez les instructions pour un [ordinateur déconnecté](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). Ensuite, procédez comme suit :

1. Configurez le scanneur dans le portail Azure, en créant un profil de scanneur. Si vous avez besoin d’aide pour cette étape, consultez [Configurer le scanneur dans le portail Azure](#configure-the-scanner-in-the-azure-portal).

2. Exportez votre profil de scanneur à partir du panneau **Azure Information Protection - Profils (préversion)**, à l’aide de l’option **Exporter**.

3. Pour finir, dans une session PowerShell, exécutez [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) et spécifiez le fichier qui contient les paramètres exportés.

Notez que dans cette configuration, le scanneur ne peut pas appliquer la protection (ou supprimer la protection) à l’aide de la clé cloud de votre organisation. Au lieu de cela, le scanneur est limité à l’utilisation d’étiquettes qui appliquent la classification uniquement, ou la protection qui utilise [HYOK](configure-adrms-restrictions.md). 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restriction : Vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

Si le rôle Sysadmin peut vous être attribué temporairement pour installer le scanneur, vous pouvez supprimer ce rôle lorsque l’installation du scanneur est terminée. Lorsque vous utilisez cette configuration, la base de données est automatiquement créée pour vous et le compte de service du scanneur obtient automatiquement les autorisations nécessaires. Toutefois, le compte d’utilisateur qui configure le scanneur nécessite le rôle db_owner pour la base de données de configuration du scanneur, et vous devez attribuer manuellement ce rôle au compte d’utilisateur.

Si vous ne pouvez pas obtenir le rôle Sysadmin même temporairement, vous devez créer manuellement une base de données avant d’installer le scanneur. Lorsque vous utilisez cette configuration, attribuez les rôles suivants :
    
|Compte|Rôle au niveau de la base de données|
|--------------------------------|---------------------|
|Compte de service pour le scanneur|db_owner|
|Compte utilisateur pour l’installation du scanneur|db_owner|
|Compte utilisateur pour la configuration du scanneur |db_owner|

En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Mais si vous utilisez des comptes différents, ils ont tous les deux besoin du rôle db_owner pour la base de données de configuration du scanneur :

- Si vous ne spécifiez pas votre propre nom de profil pour le scanneur, la base de données de configuration est nommée **AIPScanner_\<nom_ordinateur>**. 

- Si vous spécifiez votre propre nom de profil, la base de données de configuration est nommée **AIPScanner_\<nom_profil>**.

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restriction : Le compte de service pour le scanneur ne peut pas avoir le droit **Ouvrir une session localement**

Si les stratégies de votre organisation interdisent le droit **Ouvrir une session localement** pour les comptes de service, mais autorisent le droit **Se connecter en tant que traitement par lots**, suivez les instructions sous [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) dans le guide de l’administrateur.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction : Le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory, mais le serveur a accès à Internet

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- Pour le compte de service du scanneur, vous pouvez utiliser un compte Windows local ou un compte Active Directory.

- Pour le compte Azure Active Directory, suivez les instructions sous [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) dans le guide de l’administrateur.


## <a name="configure-the-scanner-in-the-azure-portal"></a>Configurer le scanneur dans le portail Azure

Avant d’installer le scanneur, ou de le mettre à niveau à partir de la version en disponibilité générale du scanneur, créez un profil pour le scanneur dans le portail Azure. Vous configurez le profil pour définir les paramètres du scanneur et les référentiels de données à analyser.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
2. Recherchez les options de menu **Scanneur**, puis sélectionnez **Profils**.

3. Dans le panneau **Azure Information Protection - Profils**, sélectionnez **Ajouter** :
    
    ![Ajouter un profil pour le scanneur Azure Information Protection](./media/scanner-add-profile.png)

4. Dans le panneau **Ajouter un nouveau profil**, donnez un nom au scanneur utilisé pour identifier ses paramètres de configuration et référentiels de données à analyser. Par exemple, vous pouvez spécifier **Europe** pour identifier l’emplacement géographique des référentiels de données couverts par votre scanneur. Lorsque vous installerez ou mettrez à niveau le scanneur ultérieurement, vous devrez spécifier le même nom de profil.
    
    Si vous le souhaitez, entrez une description des raisons administratives, pour vous aider à identifier le nom de profil du scanneur.

5. Pour cette configuration initiale, configurez les paramètres suivants, puis sélectionnez **Enregistrer** mais ne fermez pas le panneau :
    
    - **Planification**: Conservez la valeur **Manuel** par défaut
    - **Info types to be discovered** (Types d’infos à découvrir) : Définissez sur **Policy only** (Stratégie uniquement)
    - **Configure repositories** (Configurer des référentiels) : Ne configurez pas pour l’instant, car le profil doit tout d’abord être enregistré.
    - **Appliquer** : Sélectionnez **Désactivé**
    - **Label files based on content** (Étiqueter les fichiers en fonction du contenu) : Conservez la valeur **Activé** par défaut
    - **Étiquette par défaut** : Conservez la valeur **Stratégie par défaut** par défaut
    - **Relabel files** (Réétiqueter les fichiers) : Conservez la valeur **Désactivé** par défaut
    - **Conservez les valeurs de « Date de modification », « Dernière modification » et « Modifié par »** : Conservez la valeur **Activé** par défaut
    - **File types to scan** (Types de fichiers à analyser) : Conservez les types de fichiers par défaut pour **Exclure**
    - **Propriétaire par défaut** : Conservez la valeur **Scanner Account** (Compte du scanneur) par défaut

6. Maintenant que le profil est créé et enregistré, vous pouvez revenir à l’option **Configure repositories** (Configurer des référentiels) pour spécifier les magasins de données à analyser. Vous pouvez spécifier des dossiers locaux, des chemins d’accès UNC et des URL SharePoint Server pour les bibliothèques et sites locaux de SharePoint. 
    
    SharePoint Server 2019, SharePoint Server 2016 et SharePoint Server 2013 sont prises en charge pour SharePoint. SharePoint Server 2010 est également pris en charge lorsque vous bénéficiez d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
    Pour ajouter votre premier magasin de données, toujours dans le panneau **Ajouter un nouveau profil**, sélectionnez **Configure repositories** (Configurer des référentiels) pour ouvrir le panneau **Référentiels** :
    
    ![Configurer des référentiels de données pour le scanneur Azure Information Protection](./media/scanner-repositories-bar.png)

7. Dans le panneau **Référentiels**, sélectionnez **Ajouter** :
    
    ![Ajouter un référentiel de données pour le scanneur Azure Information Protection](./media/scanner-repository-add.png)

8. Dans le panneau **Référentiel**, spécifiez le chemin d’accès du référentiel de données. 
    
    Les caractères génériques ne sont pas pris en charge, ni les emplacements WebDav.
    
    Exemples :
    
    Pour un chemin d’accès local : `C:\Folder`
    
    Pour un partage réseau : `C:\Folder\Filename`
    
    Pour un chemin d’accès UNC : `\\Server\Folder`
    
    Pour une bibliothèque SharePoint : `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > Si vous ajoutez un chemin d’accès SharePoint pour « Documents partagés » :
    >
     >- Spécifiez **Documents partagés** dans le chemin d’accès lorsque vous souhaitez analyser tous les documents et tous les dossiers de Documents partagés. Par exemple : `http://sp2013/Shared Documents`
     >
     >- Spécifiez **Documents** dans le chemin d’accès lorsque vous souhaitez analyser tous les documents et tous les dossiers d’un sous-dossier sous Documents partagés. Par exemple : `http://sp2013/Documents/Sales Reports`
    
    Pour les autres paramètres de ce panneau, ne les modifiez pas pour cette configuration initiale, mais conservez-les comme **profil par défaut**. Cela signifie que le référentiel de données hérite des paramètres du profil de scanneur. 
    
    Sélectionnez **Enregistrer**.

9. Si vous souhaitez ajouter un autre référentiel de données, répétez les étapes 7 et 8.

10. Vous pouvez maintenant fermer le panneau **Ajouter un nouveau profil**. Votre nom de profil apparaît dans le panneau **Azure Information Protection - Profils**, la colonne **Planification** affichant **Manuel** et la colonne **Appliquer** étant vide.

Vous pouvez maintenant installer le scanneur avec le profil de scanneur que vous venez de créer.

## <a name="install-the-scanner"></a>Installer le scanneur

1. Connectez-vous à l’ordinateur Windows Server qui exécutera le scanneur. Utilisez un compte disposant de droits d’administrateur local et qui est autorisé à écrire dans la base de données principale SQL Server.

2. Ouvrez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Exécutez la cmdlet [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), en spécifiant l’instance SQL Server où créer une base de données pour le scanneur Azure Information Protection et le nom du profil de scanneur que vous avez spécifié dans la section précédente : 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    Exemples utilisant le nom de profil **Europe** :
    
    Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    Quand vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur (\<domaine\nom d’utilisateur>) et le mot de passe.

4. Vérifiez que le service est maintenant installé en utilisant **Outils d’administration** > **Services**. 
    
    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez obtenir un jeton Azure AD pour que le compte de service du scanneur s’authentifie afin de pouvoir exécuter le scanneur sans assistance. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Obtenir un jeton Azure AD pour le scanneur

Le jeton Azure AD permet au compte de service du scanneur de s’authentifier auprès du service Azure Information Protection.

1. Revenez au portail Azure pour créer deux applications Azure AD nécessaires pour spécifier un jeton d’accès à des fins d’authentification. Après une connexion interactive initiale, ce jeton permet au scanneur de s’exécuter de manière non interactive.
    
    Pour créer ces applications, suivez les instructions données dans [Guide pratique pour étiqueter des fichiers de manière non interactive pour Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) dans le guide de l’administrateur.

2. À partir de l’ordinateur Windows Server, si votre compte de service de scanneur a reçu l’autorisation **Ouvrir une session localement** pour l’installation : Connectez-vous avec ce compte et démarrez une session PowerShell. Exécutez [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), en spécifiant les valeurs copiées à partir de l’étape précédente :
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```
    
    Lorsque vous y êtes invité, spécifiez le mot de passe des informations d’identification de votre compte de service pour Azure AD, puis cliquez sur **Accepter**.
    
    Le compte de service pour le scanneur ne peut pas obtenir le droit **Ouvrir une session localement** pour l’installation : Suivez les instructions de la section [Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) du guide de l’administrateur. 

Le scanneur a maintenant un jeton pour s’authentifier auprès d’Azure AD, lequel jeton est valide pendant un an, deux ans, ou définitivement (il n’expire jamais), selon votre configuration de l’**application web/API** dans Azure AD. Quand le jeton expire, vous devez répéter les étapes 1 et 2.

Vous pouvez maintenant exécuter votre première analyse en mode découverte.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Exécuter un cycle de découverte et afficher les rapports pour le scanneur

1. Dans le portail Azure, revenez à Azure Information Protection pour démarrer le scanneur. Dans l’option de menu **Scanneur**, sélectionnez **Nœuds**. Sélectionnez le nœud de votre scanner, puis l’option **Scan now** (Analyser maintenant) :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)
    
    Dans votre session PowerShell, vous pouvez également exécuter la commande suivante :
    
        Start-AIPScan

2. Attendez que le scanneur termine son cycle. Une fois que le scanneur a parcouru tous les fichiers inclus dans les magasins de données que vous avez spécifiés, le service s’arrête alors que le service du scanneur continue de s’exécuter :
    
    - Dans le panneau **Azure Information Protection - Nœuds**, la valeur de la colonne **ÉTAT** passe de **Analyse** à **Inactif**.
    
    - Dans PowerShell, vous pouvez exécuter `Get-AIPScannerStatus` pour surveiller le changement d’état.
    
    - Consultez le journal des événements **Applications et services** Windows local, **Azure Information Protection**. Ce journal indique également lorsque le scanneur a terminé l’analyse, avec un résumé des résultats. Recherchez l’ID d’événement d’information **911**.

3. Passez en revue les rapports stockés dans %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Les fichiers de résumé .txt incluent la durée de l’analyse, le nombre de fichiers analysés et le nombre de fichiers correspondants aux types d’informations. Les fichiers .csv offrent plus de détails pour chaque fichier. Ce dossier stocke jusqu’à 60 rapports pour chaque cycle d’analyse et tous, sauf le dernier rapport, sont compressés afin de réduire l’espace disque requis.
    
    > [!NOTE]
    > Vous pouvez modifier le niveau de journalisation à l’aide du paramètre *ReportLevel* avec [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration), mais vous ne pouvez pas modifier l’emplacement ou le nom du dossier de rapport. Envisagez d’utiliser une jointure de répertoire pour le dossier si vous souhaitez stocker les rapports sur un autre volume ou une autre partition.
    >
    > Par exemple, à l’aide de la commande [Mklink](/windows-server/administration/windows-commands/mklink) : `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    Avec notre paramètre **Policy only** (Stratégie uniquement) pour **Info types to be discovered** (Types d’infos à découvrir), seuls les fichiers qui remplissent les conditions que vous avez configurées pour la classification automatique sont inclus dans les rapports détaillés. Si vous ne voyez pas les étiquettes appliquées, vérifiez que la configuration de votre étiquette inclut la classification automatique au lieu de la classification recommandée.
    
    > [!TIP]
    > Les scanneurs envoient ces informations à Azure Information Protection toutes les cinq minutes, ce qui permet de voir les résultats en quasi temps quasi réel sur le Portail Azure. Pour plus d’informations, consultez [Création de rapports pour Azure Information Protection](reports-aip.md). 
        
    Si les résultats ne correspondent pas à ce que vous attendez, vous devez peut-être reconfigurer les conditions que vous avez spécifiées pour vos étiquettes dans votre stratégie Azure Information Protection. Si tel est le cas, répétez les étapes 1 à 3 jusqu’à ce que vous soyez prêt à modifier la configuration pour appliquer la classification et éventuellement la protection. 

Le portail Azure affiche des informations portant uniquement sur la dernière analyse. Si vous devez consulter les résultats des analyses précédentes, accédez aux rapports qui sont stockés sur l’ordinateur du scanneur, dans le dossier %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

Quand vous êtes prêt à étiqueter automatiquement les fichiers que le scanneur découvre, passez à la procédure suivante. 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurer le scanneur pour appliquer la classification et la protection

Si vous suivez ces instructions, le scanneur s’exécute une seule fois en mode création de rapports uniquement. Pour modifier ces paramètres, modifiez le profil du scanneur :

1. Sur le **Azure Information Protection - profils** panneau, sélectionnez le profil de l’analyseur pour le modifier.

2. Dans le panneau \<**nom du profil**>, modifiez les deux paramètres suivants, puis sélectionnez **Enregistrer** :
    
   - **Planification**: Définissez sur **Toujours**
   - **Appliquer** : Sélectionnez **Activé**
    
     Il existe d’autres paramètres de configuration que vous pouvez modifier. Par exemple, si les attributs de fichier sont modifiés et que le scanneur peut réétiqueter les fichiers. Utilisez l’aide contextuelle des informations pour plus d’informations sur chaque paramètre de configuration.

3. Notez l’heure actuelle et le démarrage du scanneur indiqués dans le panneau **Azure Information Protection - Nœuds** :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)
    
    Vous pouvez également exécuter la commande suivante dans votre session PowerShell :
    
        Start-AIPScan

4. Recherchez dans le journal des événements le type d’information **911** dont l’heure horodatée est ultérieure à l’heure du démarrage du scanneur à l’étape précédente. 
    
    Puis examinez les rapports pour déterminer quels fichiers ont été étiquetés, quelle classification a été appliquée et si une protection a été appliquée. Ou bien, utilisez le portail Azure pour consulter plus facilement ces informations.

Puisque nous avons configuré la planification pour qu’elle s’exécute en continu, lorsque le scanneur a parcouru tous les fichiers, il démarre automatiquement un nouveau cycle pour découvrir les fichiers nouveaux et modifiés.


## <a name="how-files-are-scanned"></a>Procédure d’analyse des fichiers

Lors de l’analyse de fichiers, le scanneur effectue les processus suivants.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Déterminer les fichiers à inclure dans l’analyse ou à exclure de celle-ci 
Le scanneur ignore automatiquement les fichiers qui sont [exclus de la classification et de la protection](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection), comme les fichiers exécutables et les fichiers système.

Vous pouvez modifier ce comportement en définissant une liste de types de fichiers à analyser ou à exclure de l’analyse. Vous pouvez spécifier cette liste pour le scanneur à appliquer à tous les référentiels de données par défaut, et vous pouvez spécifier une liste pour chaque référentiel de données. Pour spécifier cette liste, utilisez le paramètre **Files types to scan** (Types de fichiers à analyser) dans le profil du scanneur :

![Configurer les types de fichiers à analyser pour le scanneur Azure Information Protection](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. Inspecter et étiqueter les fichiers

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
>     Pour vérifier qu’il s’agit bien de la cause de l’arrêt du scanneur, examinez si le message d’erreur suivant est consigné pour le scanneur dans %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (zippé s’il existe plusieurs journaux) : **Impossible de se connecter au serveur distant ---> System.Net.Sockets.SocketException: Une seule utilisation de chaque adresse de socket (protocole/adresse réseau/port) est habituellement autorisée IP:port**
>    
>     Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).
> 
> - Pour les grandes batteries de serveurs SharePoint, vous devrez peut-être augmenter le seuil d’affichage de liste (par défaut, 5 000). Pour plus d’informations, consultez la documentation suivante de SharePoint : [Gérer des listes et bibliothèques de grande taille dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. Étiqueter les fichiers qui ne peuvent pas être inspectés
Pour les types de fichiers qui ne peuvent pas être inspectés, le scanneur applique l’étiquette par défaut dans la stratégie Azure Information Protection ou l’étiquette par défaut que vous configurez pour le scanneur.

Comme dans l’étape précédente, le scanneur ne peut pas étiqueter les fichiers dans les cas suivants :

- L’étiquette applique la classification mais pas la protection, et le type de fichier [ne prend pas en charge la classification uniquement](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- L’étiquette applique la classification et la protection, mais le scanneur ne protège pas le type de fichier.
    
    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Il est possible de protéger d’autres types de fichiers quand vous [modifiez le Registre](#editing-the-registry-for-the-scanner), comme décrit ci-après.


### <a name="editing-the-registry-for-the-scanner"></a>Modification du Registre pour le scanneur

Pour changer le comportement par défaut du scanneur pour protéger d’autres types de fichiers que les fichiers Office et PDF, vous devez modifier manuellement le Registre et indiquer les types de fichiers supplémentaires qui doivent être protégés ainsi que le type de protection (native ou générique). Pour obtenir des instructions, consultez [Configuration de l’API de fichier](develop/file-api-configuration.md) dans le Guide du développeur. Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ». En outre, spécifiquement pour le scanneur :

- Le scanneur a son propre comportement par défaut : Seuls les formats de fichier Office et les documents PDF sont protégés par défaut. Si le Registre n’est pas modifié, aucun des autres types de fichiers ne sera étiqueté ou protégé par le scanneur.

- Si vous souhaitez que le même comportement de protection par défaut que le client Azure Information Protection, où tous les fichiers sont automatiquement protégés avec la protection native ou générique : Spécifiez le `*` génériques comme une clé de Registre `Encryption` comme valeur (REG_SZ), et `Default` que les données de valeur.

Lorsque vous modifiez le Registre, créez manuellement la clé **MSIPC** et la clé **FileProtection** si elles n’existent pas, ainsi qu’une clé pour chaque extension de nom de fichier.

Par exemple, pour que le scanneur protège les fichiers TIFF en plus des fichiers Office et PDF, le Registre devrait ressembler à l’image suivante, une fois que vous l’avez modifié. Les fichiers TIFF, qui sont des fichiers image, prennent en charge la protection native et l’extension de nom de fichier résultante est .ptiff.

![Modification du Registre pour que le scanneur applique une protection](./media/editregistry-scanner.png)

Pour obtenir la liste des types de fichiers texte et image qui prennent en charge de manière similaire la protection native mais qui doivent être spécifiés dans le Registre, consultez [Types de fichiers pris en charge pour la classification et la protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) dans le guide de l’administrateur.

Pour les fichiers ne prenant pas en charge la protection native, indiquez l’extension de nom de fichier comme nouvelle clé et **PFile** pour la protection générique. L’extension de nom de fichier résultante pour le fichier protégé est .pfile.


## <a name="when-files-are-rescanned"></a>Lorsque les fichiers sont réanalysés

Pour le premier cycle d’analyse, le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, il inspecte uniquement les fichiers nouveaux ou modifiés. 

Vous pouvez forcer le scanneur à inspecter à nouveau tous les fichiers à partir du panneau **Azure Information Protection - Nœuds** dans le portail Azure. Sélectionnez votre scanneur dans la liste, puis l’option **Rescan all files** (Relancer l’analyse de tous les fichiers) :

![Relancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-rescan-files.png)

La réinspection de tous les fichiers est utile quand vous voulez que les rapports contiennent tous les fichiers. Ce choix de configuration est généralement utilisé lorsque le scanneur s’exécute en mode découverte. Lorsqu’une analyse complète est terminée, le scanneur passe automatiquement en mode incrémentiel pour inspecter uniquement les fichiers nouveaux ou modifiés lors des analyses suivantes.

De plus, tous les fichiers sont inspectés quand le scanneur télécharge une stratégie Azure Information Protection qui présente des conditions nouvelles ou modifiées. Le scanneur actualise la stratégie toutes les heures, quand le service démarre et que la stratégie remonte à plus d’une heure.  

> [!TIP]
> Si vous avez besoin d’actualiser la stratégie avant cet intervalle d’une heure, par exemple pendant une période de test : Supprimez manuellement le fichier de stratégie **Policy.msip** dans **%LocalAppData%\Microsoft\MSIP\Policy.msip** et dans **%LocalAppData%\Microsoft\MSIP\Scanner**. Ensuite, redémarrez le service du scanneur Azure Information Protection.
> 
> Si vous avez changé les paramètres de protection de la stratégie, attendez 15 minutes après l’enregistrement des paramètres de protection avant de redémarrer le service.

Si le scanneur a téléchargé une stratégie sans conditions automatiques, la copie du fichier de stratégie dans le dossier du scanneur n’est pas mise à jour. Dans ce scénario, vous devez supprimer le fichier de stratégie **Policy.msip** dans **%LocalAppData%\Microsoft\MSIP\Policy.msip** et dans **%LocalAppData%\Microsoft\MSIP\Scanner** pour que le scanneur puisse utiliser un fichier de stratégie récemment téléchargé avec des étiquettes correctement configurées pour les conditions automatiques.

## <a name="editing-in-bulk-for-the-data-repository-settings"></a>Modification en bloc des paramètres de référentiel de données

Pour les référentiels de données que vous avez ajoutés à un profil de scanneur, vous pouvez utiliser les options **Exporter** et **Importer** pour modifier rapidement les paramètres. Par exemple, pour vos référentiels de données SharePoint, vous souhaitez ajouter un nouveau type de fichier à exclure de l’analyse.

Plutôt que de modifier chaque référentiel de données dans le portail Azure, utilisez l’option **Exporter** dans le panneau **Référentiels** :

![Exportation de paramètres de référentiel de données pour le scanneur](./media/export-scanner-repositories.png)

Modifiez manuellement le fichier pour apporter la modification, puis utilisez l’option **Importer** du même panneau.

## <a name="using-the-scanner-with-alternative-configurations"></a>Utilisation du scanneur avec d’autres configurations

Il existe deux scénarios pris en charge par le scanneur Azure Information Protection dans lesquels il n’est pas nécessaire que des étiquettes soient configurées pour des conditions quelles qu’elles soient : 

- Appliquer une étiquette par défaut à tous les fichiers dans un référentiel de données.
    
    Pour cette configuration, définissez l’**Étiquette par défaut** sur **Personnalisé**, puis sélectionnez l’étiquette à utiliser.
    
    Le contenu des fichiers n’est pas inspecté et tous les fichiers dans le référentiel de données sont nommés en fonction de l’étiquette par défaut que vous spécifiez pour le référentiel de données ou le profil du scanneur.
    

- Identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.
    
    Pour cette configuration, définissez les **Info types to be discovered** (Types d’infos à découvrir) sur **Tous**.
    
    Le scanneur utilise toute condition personnalisée que vous avez spécifiée pour les étiquettes dans la stratégie Azure Information Protection et la liste des types d’informations qui sont disponibles pour les étiquettes dans la stratégie Azure Information Protection. Ce paramètre vous permet de retrouver des informations sensibles que vous ne pensiez peut-être pas avoir, mais au détriment des taux d’analyse du scanneur.
    
    Le démarrage rapide suivant pour la version en disponibilité générale du scanneur utilise cette configuration : [Démarrage rapide : Trouver quelles sont vos informations sensibles](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Optimisation des performances du scanneur

Utilisez les instructions suivantes pour vous aider à optimiser les performances du scanneur. Toutefois, si votre priorité est la réactivité de l’ordinateur du scanneur plutôt que les performances du scanneur, vous pouvez utiliser un paramètre client avancé pour limiter le nombre de threads utilisés par le scanneur.

Pour optimiser les performances de l’analyseur :

- **Veillez à avoir une connexion haut débit fiable entre l’ordinateur de l’analyseur et le magasin de données analysé**
    
    Par exemple, placez l’ordinateur de l’analyseur dans le même réseau local ou (de préférence) dans le même segment réseau que le magasin de données analysé.
    
    La qualité de la connexion réseau affecte les performances de l’analyseur parce que pour examiner les fichiers, celui-ci transfère le contenu des fichiers à l’ordinateur exécutant son service. Quand vous réduisez (ou supprimez) le nombre de tronçons réseau que ces données doivent traverser, vous réduisez également la charge sur votre réseau. 

- **Assurez-vous que l’ordinateur de l’analyseur dispose de ressources processeur**
    
    L’inspection du contenu des fichiers ainsi que le chiffrement et le déchiffrement des fichiers sont des actions qui sollicitent le processeur de manière intense. Surveillez les cycles d’analyse standard de vos magasins de données spécifiés pour déterminer si un manque de ressources processeur affecte les performances de l’analyseur.
    
- **N’analysez pas les dossiers locaux sur l’ordinateur exécutant le service de l’analyseur**
    
    Si vous avez des dossiers à analyser sur un serveur Windows, installez l’analyseur sur un autre ordinateur et configurez ces dossiers comme partages réseau à analyser. En séparant les deux fonctions d’hébergement des fichiers et d’analyse des fichiers, les ressources informatiques de ces services n’entrent pas en concurrence.

Si nécessaire, installez plusieurs instances du scanneur. Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance SQL Server lorsque vous spécifiez un nom de profil personnalisé pour le scanneur.

Autres facteurs qui affectent les performances de l’analyseur :

- La charge actuelle et les temps de réponse des magasins de données qui contiennent les fichiers à analyser

- Si l’analyseur s’exécute en mode découverte ou en mode d’application
    
    Le mode découverte a généralement un taux d’analyse plus élevé que le mode d’application, car la découverte nécessite une seule action de lecture de fichier tandis que le mode d’application nécessite des actions de lecture et d’écriture.

- Le changement des conditions d’Azure Information Protection
    
    Votre premier cycle d’analyse lorsque le scanneur doit inspecter chaque fichier prend plus temps que les cycles d’analyse suivants qui, par défaut, inspectent uniquement les fichiers nouveaux et modifiés. Toutefois, si vous changez les conditions dans la stratégie Azure Information Protection, tous les fichiers sont réanalysés, comme décrit dans la [section précédente](#when-files-are-rescanned).

- La construction d’expressions regex pour des conditions personnalisées
    
    Pour éviter une consommation de mémoire importante et le risque de dépassements du délai d’expiration (15 minutes par fichier), passez en revue vos expressions regex pour vérifier que la correspondance des modèles est efficace. Exemple :
    
    - Évitez les [quantificateurs gourmands](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - Utilisez des groupes sans capture comme `(?:expression)` au lieu de `(expression)`

- Le niveau de journalisation que vous avez choisi
    
    Vous pouvez choisir entre **Déboguer**, **Information**, **Erreur** et **Désactivé** pour les rapports de l’analyseur. Avec **Désactivé**, vous bénéficiez des meilleures performances alors qu’avec **Déboguer**, l’analyseur est considérablement ralenti et doit être utilisé uniquement pour le dépannage. Pour plus d’informations, consultez le paramètre *ReportLevel* de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- Les fichiers eux-mêmes :
    
    - Les fichiers Office sont analysés plus rapidement que les fichiers PDF.
    
    - Les fichiers non protégés sont plus rapides à analyser que les fichiers protégés.
    
    - Les gros fichiers prennent évidemment plus de temps à analyser que les petits fichiers.

- En outre :
    
    - Vérifiez que le compte de service qui exécute le scanneur dispose seulement des droits documentés dans la section [prérequis du scanneur](#prerequisites-for-the-azure-information-protection-scanner), puis configurez la [propriété client avancée](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) de manière à désactiver le niveau d’intégrité faible pour le scanneur.
    
    - Le scanneur s’exécute plus rapidement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour appliquer une étiquette par défaut à tous les fichiers, car le scanneur n’inspecte pas le contenu du fichier.
    
    - Le scanneur s’exécute plus lentement lorsque la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) est utilisée pour identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.
    

## <a name="list-of-cmdlets-for-the-scanner"></a>Liste des cmdlets pour le scanneur

Étant donné que vous configurez maintenant le scanneur à partir du portail Azure, les cmdlets de versions précédentes qui configuraient des référentiels de données et la liste de types de fichiers analysés sont désormais déconseillées. 

Les cmdlets conservées incluent des cmdlets qui installent et mettent à niveau le scanneur, modifient la base de données de configuration du scanneur et le profil, modifient le niveau de rapport local et importent des paramètres de configuration pour un ordinateur déconnecté. 

La liste complète des applets de commande qui prend en charge de la version actuelle du scanneur : 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


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

Si le scanneur a été configuré pour s’exécuter manuellement plutôt que de manière continue, pour relancer l’analyse des fichiers, définissez la **Planification** sur **Manuel** ou **Toujours** dans le profil du scanneur, puis redémarrez le service.

----

## <a name="next-steps"></a>Étapes suivantes

Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

Vous vous demandez peut-être : [Quelle différence y a-t-il entre l’ICF de Windows Server et le scanneur d’Azure Information Protection ?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur tous les scénarios qui utilisent PowerShell, consultez [Utiliser PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

