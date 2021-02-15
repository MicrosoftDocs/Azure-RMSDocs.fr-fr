---
title: Installer et configurer le scanneur d’Azure Information Protection (AIP)
description: Instructions d’installation et de configuration de l’analyseur de Azure Information Protection pour détecter, classer et protéger des fichiers dans des magasins de données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/01/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 46655ef7da2d8670ef3fced105b3d471bb05a8f9
ms.sourcegitcommit: caf2978ab03e4893b59175ce753791867793dcfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2021
ms.locfileid: "100524759"
---
# <a name="configuring-and-installing-the-azure-information-protection-classic-scanner"></a>Configuration et installation du Azure Information Protection scanneur classique

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [installation et configuration du scanneur d’étiquetage unifié AIP](deploy-aip-scanner-configure-install.md). *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Avant de commencer à configurer et à installer le scanneur Azure Information Protection, vérifiez que votre système est conforme aux [conditions préalables requises](deploy-aip-scanner-prereqs.md).

Lorsque vous êtes prêt, passez aux étapes suivantes :

1. [Configurer le scanneur dans le portail Azure](#configure-the-scanner-in-the-azure-portal)

1. [Installer le scanneur](#install-the-scanner)

1. [Obtenir un jeton Azure AD pour le scanneur](#get-an-azure-ad-token-for-the-scanner)

1. [Configurer le scanneur pour appliquer la classification et la protection](#configure-the-scanner-to-apply-classification-and-protection)

Effectuez les procédures de configuration supplémentaires suivantes selon les besoins de votre système :

|Procédure  |Description  |
|---------|---------|
|[Changer les types de fichiers à protéger](#change-which-file-types-to-protect) |Vous souhaiterez peut-être analyser, classer ou protéger différents types de fichiers par rapport à la valeur par défaut. Pour plus d’informations, consultez [processus d’analyse AIP](deploy-aip-scanner.md#aip-scanning-process). |
|[Mise à niveau de votre scanneur](#upgrading-your-scanner) | Mettez à niveau votre scanneur pour tirer parti des dernières fonctionnalités et améliorations.|
|[Modification des paramètres du référentiel de données en bloc](#editing-data-repository-settings-in-bulk)| Utilisez les options d’importation et d’exportation pour apporter des modifications en bloc pour plusieurs référentiels de données.|
|[Utiliser le scanneur avec d’autres configurations](#using-the-scanner-with-alternative-configurations)| Utiliser le scanneur sans configurer d’étiquettes avec des conditions |
|[Optimiser les performances](#optimizing-scanner-performance)| Conseils pour optimiser les performances de votre scanneur|
| | |

Pour plus d’informations, consultez également [la liste des applets de commande pour le scanneur](#list-of-cmdlets-for-the-scanner).

## <a name="configure-the-scanner-in-the-azure-portal"></a>Configurer le scanneur dans le portail Azure

Avant d’installer le scanneur ou de le mettre à niveau à partir d’une ancienne version de disponibilité générale du scanneur, créez un travail de cluster et d’analyse de contenu pour le scanneur dans le Portail Azure.

Ensuite, configurez le cluster et le travail d’analyse du contenu avec les paramètres du scanneur et les référentiels de données à analyser.

Pour configurer votre scanneur :

1. [Connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)et accédez au volet de **Azure information protection** .

    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

1. Recherchez les options du menu **scanner** , puis sélectionnez **clusters**.

1. Dans le volet **Azure information protection-clusters** , sélectionnez **Ajouter**:

    :::image type="content" source="media/scanner-add-profile.png" alt-text="Ajouter un travail d’analyse de contenu au scanneur Azure Information Protection":::

1. Dans le volet **Ajouter un nouveau cluster** :

    1. Spécifiez un nom explicite pour le scanneur. Ce nom est utilisé pour identifier les paramètres de configuration du scanneur et les référentiels de données à analyser.

        Par exemple, vous pouvez spécifier **Europe** pour identifier l’emplacement géographique des référentiels de données couverts par votre scanneur. Lorsque vous installez ou mettez à niveau ultérieurement le scanneur, vous devez spécifier le même nom de cluster.

    2. Si vous le souhaitez, spécifiez une description à des fins administratives pour vous aider à identifier le nom du cluster du scanneur.

    3. Sélectionnez **Enregistrer**.
1. Recherchez les options du menu **scanner** , puis sélectionnez **travaux d’analyse du contenu**.
1. Dans le volet **Azure information protection-travaux d’analyse de contenu** , sélectionnez **Ajouter**.

1. Pour cette configuration initiale, configurez les paramètres suivants, puis sélectionnez **Enregistrer** sans fermer le volet :

    |Section  |Paramètres  |
    |---------|---------|
    |**Paramètres du travail d’analyse du contenu**     |    - **Planifier**: conserver la valeur par défaut **manuelle** </br>- **Types d’informations à découvrir**: changer en **stratégie uniquement** </br>- **Configurer les référentiels**: ne pas configurer pour l’instant, car le travail d’analyse de contenu doit d’abord être enregistré.         |
    |**Stratégie de sensibilité**     | - **Appliquer**: sélectionner **désactivé** </br>- **Étiqueter les fichiers en fonction du contenu**: conservez la valeur par défaut **activée** </br>- **Étiquette par** défaut : conserver la valeur par défaut de la **stratégie** par défaut </br>- **Réétiqueter les fichiers**: conserver la valeur par défaut **désactivé**        |
    |**Configurer les paramètres du fichier**     | - **Conserver les valeurs « date de modification », « dernière modification » et « modifié par »**: conserver la valeur par défaut **activée** </br>- **Types de fichiers à analyser**: conserver les types de fichiers par défaut pour l' **exclusion** </br>- **Propriétaire par défaut**: conserver la valeur par défaut du **compte de scanneur**        |
    | | |

1. Maintenant que le travail d’analyse de contenu est créé et enregistré, vous êtes prêt à revenir à l’option **configurer les référentiels** pour spécifier les magasins de données à analyser.

    Spécifiez les chemins d’accès UNC et les URL du serveur SharePoint pour les dossiers et bibliothèques de documents locaux SharePoint.

    > [!NOTE]
    > SharePoint Server 2019, SharePoint Server 2016 et SharePoint Server 2013 sont pris en charge pour SharePoint. SharePoint Server 2010 est également pris en charge lorsque vous bénéficiez d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    >
    Pour ajouter votre premier magasin de données, dans le volet **Ajouter un nouveau travail d’analyse de contenu** , sélectionnez configurer les **référentiels** pour ouvrir le volet **dépôts** :

    :::image type="content" source="media/scanner-repositories-bar.png" alt-text="Configuration de référentiels de données pour le scanneur Azure Information Protection":::

1. Dans le volet **Référentiels**, sélectionnez **Ajouter** :

    :::image type="content" source="media/scanner-repository-add.png" alt-text="Ajouter un référentiel de données pour le scanneur Azure Information Protection":::

1. Dans le volet **référentiel** , spécifiez le chemin d’accès du référentiel de données, puis sélectionnez **Enregistrer**.

    Par exemple : 

    - Pour un partage réseau, utilisez `\\Server\Folder` . 
    - Pour une bibliothèque SharePoint, utilisez `http://sharepoint.contoso.com/Shared%20Documents/Folder` .

    > [!NOTE]
    > Les caractères génériques ne sont pas pris en charge, ni les emplacements WebDav.
    >     

    Pour ajouter des chemins d’accès SharePoint, utilisez la syntaxe ci-après :
    
    |Chemin d’accès  |Syntaxe  |
    |---------|---------|
    |**Chemin d’accès racine**     | `http://<SharePoint server name>` </br></br>Analyse tous les sites, y compris les collections de sites autorisées pour l’utilisateur du scanneur. </br>Nécessite [des autorisations supplémentaires](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) pour découvrir automatiquement le contenu racine        |
    |**Sous-site ou regroupement SharePoint spécifique**     | Celui-ci peut avoir l'une des valeurs suivantes : </br>- `http://<SharePoint server name>/<subsite name>` </br>- `http://SharePoint server name>/<site collection name>/<site name>` </br></br>Nécessite [des autorisations supplémentaires](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) pour découvrir automatiquement le contenu de la collection de sites         |
    |**Bibliothèque SharePoint spécifique**     | Celui-ci peut avoir l'une des valeurs suivantes : </br>- `http://<SharePoint server name>/<library name>` </br>- `http://SharePoint server name>/.../<library name>`       |
    |**Dossier SharePoint spécifique**     | `http://<SharePoint server name>/.../<folder name>`        |
    | | |

    Pour les autres paramètres de ce volet, ne les modifiez pas pour cette configuration initiale, mais conservez-les en tant que **travail d’analyse du contenu par défaut**. Le paramètre par défaut signifie que le référentiel de données hérite des paramètres du travail d’analyse de contenu.


1. Si vous souhaitez ajouter un autre référentiel de données, répétez les étapes 8 et 9.

1. Fermez le volet **référentiels** et le volet **travail analyse du contenu** .

De retour dans le volet du **travail analyse du contenu Azure information protection** , le nom de votre analyse de contenu s’affiche, ainsi que la colonne **planification** qui indique **Manuel** et la colonne **appliquer** est vide.

Vous êtes maintenant prêt à installer le scanneur avec la tâche d’analyse de contenu que vous avez créée. Continuez [l’installation du scanneur](#install-the-scanner).

## <a name="install-the-scanner"></a>Installer le scanneur

Une fois que vous avez [configuré le scanneur Azure information protection dans le portail Azure](#configure-the-scanner-in-the-azure-portal), effectuez les étapes ci-dessous pour installer le scanneur :

1. Connectez-vous à l’ordinateur Windows Server qui exécutera le scanneur. Utilisez un compte disposant de droits d’administrateur local et qui est autorisé à écrire dans la base de données principale SQL Server.

    > [!IMPORTANT]
    > Pour plus d’informations, consultez [Configuration requise pour l’installation et le déploiement du scanneur Azure information protection](deploy-aip-scanner-prereqs.md).
    >

1. Ouvrez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

1. Exécutez l’applet de commande [install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) , en spécifiant votre SQL Server instance sur laquelle créer une base de données pour le scanneur de Azure information protection, et le nom du cluster du scanneur que vous avez spécifié dans la section précédente :

    ```PowerShell
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```

    Exemples utilisant le nom de profil **Europe** :

    - Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`

    - Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`

    - Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`

    Lorsque vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur ( `\<domain\user name>` ) et du mot de passe.

1. Vérifiez que le service est maintenant installé à l’aide des **Outils d’administration**  >  **services**.

    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez [obtenir un jeton de Azure AD pour que le compte de service du scanneur](#get-an-azure-ad-token-for-the-scanner) s’authentifie, afin que le scanneur puisse s’exécuter sans assistance.

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Obtenir un jeton Azure AD pour le scanneur

Un jeton de Azure AD permet au scanneur de s’authentifier auprès du service Azure Information Protection.

Pour recevoir un jeton de Azure AD :

1. Revenez à la Portail Azure pour créer deux applications Azure AD pour spécifier un jeton d’accès pour l’authentification. Ce jeton permet au scanneur de s’exécuter de manière non interactive.

    Pour plus d’informations, consultez [Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

2. À partir de l’ordinateur Windows Server, si votre compte de service de scanneur a reçu le droit **ouvrir une session localement** pour l’installation, connectez-vous avec ce compte et démarrez une session PowerShell.

    Exécutez [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), en spécifiant les valeurs copiées à partir de l’étape précédente :

    ```PowerShell
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    Lorsque vous y êtes invité, spécifiez le mot de passe des informations d’identification de votre compte de service pour Azure AD, puis cliquez sur **Accepter**.

    Par exemple :

    ```PowerShell
    Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip
    Acquired application access token on behalf of the user
    ```

> [!TIP]
> Si votre compte de service de scanneur ne peut pas se voir accorder le droit **ouvrir une session localement** , [spécifiez et utilisez le paramètre Token pour Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication).
>

Le scanneur dispose désormais d’un jeton pour s’authentifier auprès de Azure AD, ce qui est valide pendant un an, deux ans ou jamais, en fonction de votre configuration de l' **application Web/API** dans Azure ad.

Quand le jeton expire, vous devez répéter les étapes 1 et 2.

Vous pouvez maintenant exécuter votre première analyse en mode découverte. Pour plus d’informations, consultez [exécuter un cycle de découverte et afficher les rapports du scanneur](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner).

Si vous avez déjà exécuté une analyse de découverte, poursuivez [la configuration du scanneur pour appliquer la classification et la protection](#configure-the-scanner-to-apply-classification-and-protection).

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurer le scanneur pour appliquer la classification et la protection

Les paramètres par défaut configurent le scanneur pour qu’il s’exécute une seule fois et en mode rapport uniquement.

Pour modifier ces paramètres, modifiez le travail d’analyse du contenu :

1. Dans le Portail Azure, dans le volet **Azure information protection de travaux d’analyse de contenu** , sélectionnez le travail de cluster et d’analyse de contenu pour le modifier.

2. Dans le volet du travail analyse du contenu, modifiez les éléments suivants, puis sélectionnez **Enregistrer**:

   - Dans la section **travail d’analyse du contenu** : modifiez la **planification** pour **toujours**
   - À partir de la section **stratégie de sensibilité** : changer **appliquer** à **activé**

    > [!TIP]
    > Vous pouvez modifier d’autres paramètres dans ce volet, par exemple si les attributs de fichier sont modifiés et si le scanneur peut réétiqueter les fichiers. Utilisez l’aide contextuelle des informations pour plus d’informations sur chaque paramètre de configuration.

3. Prenez note de l’heure actuelle et redémarrez le scanneur à partir du volet **travaux d’analyse de contenu Azure information protection** :

    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

    Vous pouvez également exécuter la commande suivante dans votre session PowerShell :

    ```PowerShell
    Start-AIPScan
    ```

4. Pour afficher les rapports des fichiers étiquetés, la classification appliquée et si la protection a été appliquée, surveillez le journal des événements pour connaître le type d’information **911** et l’horodatage le plus récent.

    Pour plus d’informations, consultez les rapports ou utilisez le Portail Azure pour rechercher ces informations.

Le scanneur est maintenant programmé pour s’exécuter en continu. Lorsque le scanneur fonctionne dans tous les fichiers configurés, il démarre automatiquement un nouveau cycle afin que tous les fichiers nouveaux et modifiés soient découverts.

## <a name="change-which-file-types-to-protect"></a>Changer les types de fichiers à protéger

Par défaut, le scanneur AIP protège les types de fichiers Office et les fichiers PDF uniquement. Pour modifier ce comportement, par exemple pour configurer le scanneur afin de protéger tous les types de fichiers, tout comme le fait le client, ou pour protéger des types de fichiers supplémentaires spécifiques, modifiez le registre comme suit :

- Spécifiez les types de fichiers supplémentaires que vous souhaitez protéger.
- Spécifiez le type de protection que vous souhaitez appliquer (natif ou générique)

Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ».

Pour aligner les types de fichiers pris en charge avec le client, où tous les fichiers sont automatiquement protégés par une protection native ou générique :

1. Spécification :

    - `*`Caractère générique en tant que clé de Registre
    - `Encryption` comme valeur (REG_SZ)
    - `Default` en tant que données de valeur

1. Vérifiez si les clés **MSIPC** et **FileProtection** existent. Créez-les manuellement si ce n’est pas le cas, puis créez une sous-clé pour chaque extension de nom de fichier.

    Par exemple, pour que le scanneur protège les images TIFF en plus des fichiers Office et des fichiers PDF, le registre doit ressembler à ce qui suit une fois que vous l’avez modifié :

    ![Modification du Registre pour que le scanneur applique une protection](./media/editregistry-scanner.png)

    > [!NOTE]
    > En tant que fichier image, les fichiers TIFF prennent en charge la protection native et l’extension de nom de fichier résultante est **. ptiff**.
    >

    Pour les fichiers ne prenant pas en charge la protection native, indiquez l’extension de nom de fichier comme nouvelle clé et **PFile** pour la protection générique. L’extension de nom de fichier résultante pour le fichier protégé est **. pfile**.

Pour obtenir la liste des types de fichiers texte et image qui prennent en charge de façon similaire la protection native, mais qui doivent être spécifiés dans le registre, consultez [types de fichiers pris en charge pour la classification et la protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection).

## <a name="upgrading-your-scanner"></a>Mise à niveau de votre scanneur

Si vous avez déjà installé le scanneur et que vous souhaitez effectuer une mise à niveau, consultez [mise à niveau de l’analyseur de Azure information protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

Ensuite, [configurez](deploy-aip-scanner-configure-install-classic.md) et [Utilisez votre scanneur](deploy-aip-scanner-manage-classic.md) comme d’habitude, en ignorant les étapes d’installation de votre scanneur.

>[!NOTE]
> Si vous disposez d’une version du scanneur antérieure à 1.48.204.0 et que vous n’êtes pas prêt à effectuer la mise à niveau, consultez [déploiement de versions antérieures du moteur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner-previousversions.md).

## <a name="editing-data-repository-settings-in-bulk"></a>Modification des paramètres du référentiel de données en bloc

Utilisez les boutons **Exporter** et **Importer** pour apporter des modifications à votre scanneur sur plusieurs dépôts.

De cette façon, vous n’avez pas besoin d’effectuer plusieurs fois les mêmes modifications, manuellement, dans le Portail Azure.

Par exemple, si vous avez un nouveau type de fichier dans plusieurs référentiels de données SharePoint, vous souhaiterez peut-être mettre à jour les paramètres de ces dépôts en bloc.

Pour apporter des modifications en bloc dans les référentiels :

1. Dans le Portail Azure du volet **référentiels** , sélectionnez l’option d' **exportation** . Par exemple :

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="Exportation de paramètres de référentiel de données pour le scanneur":::

1. Modifiez manuellement le fichier exporté pour effectuer votre modification.

1. Utilisez l’option d' **importation** sur la même page pour réimporter les mises à jour dans vos référentiels.

## <a name="using-the-scanner-with-alternative-configurations"></a>Utilisation du scanneur avec d’autres configurations

Le scanneur de Azure Information Protection recherche généralement des conditions spécifiées pour vos étiquettes afin de classer et de protéger votre contenu si nécessaire.

Dans les scénarios suivants, le Azure Information Protection scanner est également en mesure d’analyser votre contenu et de gérer des étiquettes, sans aucune condition configurée :

- [Appliquer une étiquette par défaut à tous les fichiers d’un référentiel de données](#apply-a-default-label-to-all-files-in-a-data-repository)
- [Identifiez toutes les conditions personnalisées et les types d’informations sensibles connus](#identify-all-custom-conditions-and-known-sensitive-information-types)

### <a name="apply-a-default-label-to-all-files-in-a-data-repository"></a>Appliquer une étiquette par défaut à tous les fichiers d’un référentiel de données

Dans cette configuration, tous les fichiers sans étiquette du référentiel sont étiquetés avec l’étiquette par défaut spécifiée pour le référentiel ou le travail d’analyse du contenu. Les fichiers sont étiquetés sans inspection.

Configurez les paramètres suivants :

- **Étiqueter les fichiers en fonction du contenu**: **désactivée**
- **Étiquette par défaut**: définissez sur **personnalisé**, puis sélectionnez l’étiquette à utiliser

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>Identifiez toutes les conditions personnalisées et les types d’informations sensibles connus

Cette configuration vous permet de trouver des informations sensibles que vous n’avez pas pu constater, aux dépens des taux de numérisation pour le scanneur.

Définissez les **types d’informations à découvrir** pour **tous**.

Pour identifier les conditions et les types d’informations pour l’étiquetage, le scanneur utilise des conditions personnalisées spécifiées pour les étiquettes et la liste des types d’informations disponibles à spécifier pour les étiquettes, comme indiqué dans la stratégie de Azure Information Protection.

Pour plus d’informations, consultez [démarrage rapide : trouver les informations sensibles dont vous disposez](quickstart-findsensitiveinfo.md).

## <a name="optimizing-scanner-performance"></a>Optimisation des performances de l’analyseur

> [!NOTE]
> Si vous cherchez à améliorer la réactivité de l’ordinateur du scanneur plutôt que les performances de l’analyseur, utilisez un paramètre client avancé pour [limiter le nombre de threads utilisés par le scanneur](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner).
>

Utilisez les options et les conseils suivants pour vous aider à optimiser les performances de l’analyseur :

|Option  |Description  |
|---------|---------|
|**Veillez à avoir une connexion haut débit fiable entre l’ordinateur de l’analyseur et le magasin de données analysé**     |  Par exemple, placez l’ordinateur du scanneur sur le même réseau local, ou de préférence, dans le même segment de réseau que le magasin de données analysé. </br></br>La qualité de la connexion réseau affecte les performances de l’analyseur car, pour inspecter les fichiers, l’analyseur transfère le contenu des fichiers sur l’ordinateur exécutant le service du scanneur. </br></br>La réduction ou l’élimination des sauts réseau requis pour le déplacement des données réduit également la charge sur votre réseau.      |
|**Assurez-vous que l’ordinateur de l’analyseur dispose de ressources processeur**     | L’inspection du contenu du fichier et le chiffrement et le déchiffrement des fichiers sont des actions nécessitant beaucoup de ressources du processeur. </br></br>Surveillez les cycles d’analyse typiques pour les magasins de données spécifiés pour déterminer si un manque de ressources du processeur affecte les performances de l’analyseur.        |
|**Installer plusieurs instances du scanneur** | Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance de SQL Server lorsque vous spécifiez un nom de cluster personnalisé (profil) pour le scanneur. |
|**Accorder des droits spécifiques et désactiver le niveau d’intégrité faible**|Vérifiez que le compte de service qui exécute le scanneur dispose uniquement des droits décrits dans la [Configuration requise du compte de service](deploy-aip-scanner-prereqs.md#service-account-requirements). </br></br>Ensuite, configurez le [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) pour désactiver le niveau d’intégrité faible pour le scanneur.|
|**Vérifier l’utilisation de la configuration de remplacement** |Le scanneur s’exécute plus rapidement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour appliquer une étiquette par défaut à tous les fichiers, car le scanneur n’inspecte pas le contenu du fichier. <br/></br>Le scanneur s’exécute plus lentement lorsque la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) est utilisée pour identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.|
|**Réduire les délais d’expiration du scanneur** | Diminuez les délais d’attente du scanneur avec les [Paramètres avancés du client](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner). Les délais d’analyse réduits permettent d’obtenir de meilleurs taux d’analyse et une consommation de mémoire inférieure. </br></br>**Remarque**: la diminution du délai d’attente du scanneur signifie que certains fichiers peuvent être ignorés.
| | |


### <a name="additional-factors-that-affect-performance"></a>Facteurs supplémentaires qui affectent les performances

Les facteurs supplémentaires qui affectent les performances du scanneur sont les suivants :

|Factor  |Description  |
|---------|---------|
|**Temps de chargement/réponse**     |Les temps de chargement et de réponse actuels des magasins de données qui contiennent les fichiers à analyser affectent également les performances du scanneur.         |
|**Mode scanneur** (détection/application)    | Le mode de détection a généralement un taux d’analyse plus élevé que le mode d’application. </br></br>La découverte requiert une seule action de lecture de fichier, tandis que le mode d’application requiert des actions de lecture et d’écriture.        |
|**Modifications de stratégie**     |Les performances de votre scanneur peuvent être affectées si vous avez apporté des modifications aux conditions de la stratégie de Azure Information Protection. </br></br>Votre premier cycle d’analyse, lorsque le scanneur doit inspecter chaque fichier, prend plus de temps que les cycles d’analyse suivants qui, par défaut, inspectent uniquement les fichiers nouveaux et modifiés. </br></br>Si vous modifiez les conditions, tous les fichiers sont analysés à nouveau. Pour plus d’informations, consultez [rescaning Files](deploy-aip-scanner-manage-classic.md#rescanning-files).|
|**Constructions Regex**    | Les performances de l’analyseur sont affectées par la manière dont vos expressions Regex pour les conditions personnalisées sont construites. </br></br> Pour éviter une consommation de mémoire importante et le risque de dépassements du délai d’expiration (15 minutes par fichier), passez en revue vos expressions regex pour vérifier que la correspondance des modèles est efficace. </br></br>Par exemple : </br>-Évitez les [quantificateurs gourmands](/dotnet/standard/base-types/quantifiers-in-regular-expressions) </br>-Utiliser des groupes sans capture comme `(?:expression)` au lieu de `(expression)`    |
|**Niveau de journalisation**     |  Les options de niveau de journalisation sont **Debug**, **info**, **Error** et **off** pour les rapports du scanneur.</br></br>- La valeur **off** permet d’obtenir des performances optimales </br>- Le **débogage** ralentit considérablement le scanneur et doit être utilisé uniquement pour la résolution des problèmes. </br></br>Pour plus d’informations, consultez le paramètre *ReportLevel* de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).       |
|**Fichiers en cours d’analyse**     |-À l’exception des fichiers Excel, les fichiers Office sont analysés plus rapidement que les fichiers PDF. </br></br>-Les fichiers non protégés sont plus rapides à analyser que les fichiers protégés. </br></br>-Les fichiers volumineux sont évidemment plus longs à analyser que les petits fichiers.         |
| | |

## <a name="list-of-cmdlets-for-the-scanner"></a>Liste des cmdlets pour le scanneur

Cette section répertorie les applets de commande PowerShell prises en charge pour le scanneur Azure Information Protection.

> [!NOTE]
> Le scanneur de Azure Information Protection est configuré à partir de la Portail Azure. Par conséquent, les applets de commande utilisées dans les versions précédentes pour configurer les référentiels de données et la liste des types de fichiers analysés sont désormais dépréciées.
>

Les applets de commande prises en charge pour le scanneur sont les suivantes :

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScanDiagnostics](/powershell/module/azureinformationprotection/Start-AIPScanDiagnostics)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Stop-AIPScan](/powershell/module/azureinformationprotection/Stop-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez installé et configuré votre scanneur, commencez à [analyser vos fichiers](deploy-aip-scanner-manage.md).

Voir aussi : [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md).

**Plus d’informations**:

Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs-classic.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur tous les scénarios qui utilisent PowerShell, consultez [Utiliser PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).