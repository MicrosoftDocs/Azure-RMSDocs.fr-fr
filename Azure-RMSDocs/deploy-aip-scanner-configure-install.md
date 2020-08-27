---
title: Installer et configurer le scanneur d’étiquetage unifiée de l’Azure Information Protection (AIP)
description: Instructions d’installation et de configuration du Azure Information Protection scanneur d’étiquetage unifié pour la détection, la classification et la protection des fichiers sur les banques de données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/24/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fcc798a8b9b4a2e0472aad77123571ab03070324
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953148"
---
# <a name="configuring-and-installing-the--azure-information-protection-unified-labeling-scanner"></a>Configuration et installation du scanneur d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows server 2012 R2*

>[!NOTE] 
> Si vous utilisez le scanneur classique AIP, consultez [installation et configuration du Azure information protection scanneur classique](deploy-aip-scanner-configure-install-classic.md).

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

Avant d’installer le scanneur ou de le mettre à niveau à partir d’une ancienne version de disponibilité générale, configurez ou vérifiez les paramètres de votre scanneur dans la zone Azure Information Protection du Portail Azure.

Pour configurer votre scanneur : 

1. [Connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)et accédez au volet de **Azure information protection** . 
    
    Par exemple, dans la zone de recherche des ressources, services et documents, commencez à taper **Information** et sélectionnez **Azure Information Protection**.

1. [Créez un cluster de scanneur](#create-a-scanner-cluster). Ce cluster définit votre scanneur et est utilisé pour identifier l’instance de l’analyseur, par exemple lors de l’installation, des mises à niveau et d’autres processus.

1. Facultatif [Analysez votre réseau à la recherche de référentiels risqués](#create-a-network-scan-job-public-preview). Créer un travail d’analyse réseau pour analyser une adresse IP ou une plage spécifiée, et fournir une liste des dépôts risqués pouvant contenir du contenu sensible que vous souhaitez sécuriser.  

    Exécutez votre travail d’analyse réseau, puis [Analysez tous les dépôts risqués détectés](#analyze-risky-repositories-found-public-preview).

1. [Créez un travail d’analyse de contenu](#create-a-content-scan-job) pour définir les référentiels que vous souhaitez analyser.

### <a name="create-a-scanner-cluster"></a>Créer un cluster de scanneur  

1. Dans le menu du **scanneur** situé à gauche, sélectionnez **clusters** clusters ![icône](media/i-clusters.png "icône clusters").

1. Dans le volet **Azure information protection-clusters** , sélectionnez **Ajouter** une ![icône](media/i-add.png "icône d’ajout").
    
1. Dans le volet **Ajouter un nouveau cluster** , entrez un nom explicite pour le scanneur et une description facultative. 
    
    Le nom du cluster est utilisé pour identifier les configurations et les référentiels du scanneur. Par exemple, vous pouvez entrer en **Europe** pour identifier les emplacements géographiques des référentiels de données que vous souhaitez analyser. 

    Vous utiliserez ce nom ultérieurement pour identifier l’emplacement où vous souhaitez installer ou mettre à niveau votre scanneur.

1. Sélectionnez **Enregistrer** l' ![icône Enregistrer](media/qs-tutor/save-icon.png "icône Enregistrer") pour enregistrer vos modifications.

### <a name="create-a-network-scan-job-public-preview"></a>Créer un travail d’analyse réseau (préversion publique)

À partir de la version 2.8.83, vous pouvez analyser votre réseau à la recherche de référentiels risqués. Ajoutez un ou plusieurs référentiels trouvés à un travail d’analyse de contenu pour les analyser à la recherche de contenu sensible.

> [!NOTE]
> L’interface de **découverte du réseau** est actuellement en cours de déploiement progressif et sera disponible dans toutes les régions du 15 septembre 2020. 

- [Conditions préalables pour la découverte du réseau](#network-discovery-prerequisites)
- [Création d’un travail d’analyse réseau](#creating-a-network-scan-job)

#### <a name="network-discovery-prerequisites"></a>Conditions préalables pour la découverte du réseau

|Configuration requise  |Description  |
|---------|---------|
|**Installation du service de découverte du réseau**     |   Si vous avez récemment mis à niveau votre scanneur, vous devrez peut-être tout de même installer le service de découverte du réseau. </br></br>Exécutez l’applet de commande [**install-MIPNetworkDiscovery**](https://docs.microsoft.com/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) pour activer les travaux d’analyse réseau.      |
|**Azure Information Protection Analytics**     | Assurez-vous que Azure Information Protection Analytics est activé. </br></br>Dans la Portail Azure, accédez à **Azure Information Protection > gérer > configurer Analytics (** préversion). </br></br>Pour plus d’informations, consultez [central Reporting for Azure information protection (version préliminaire publique)](reports-aip.md).|
| | |

#### <a name="creating-a-network-scan-job"></a>Création d’un travail d’analyse réseau

1. Connectez-vous au Portail Azure et accédez à **Azure information protection.** Dans le menu du **scanneur** situé à gauche, sélectionnez **travaux d’analyse réseau (** préversion) ![icône travaux d’analyse réseau](media/i-network-scan-jobs.png "icône de travaux d’analyse réseau").
    
1. Dans le volet **Azure information protection-travaux d’analyse réseau** , sélectionnez **Ajouter** une ![icône](media/i-add.png "icône d’ajout").
    
1. Sur la page **Ajouter un nouveau travail d’analyse réseau** , définissez les paramètres suivants :
        
    |Paramètre  |Description  |
    |---------|---------|
    |**Nom du travail d’analyse réseau**     |Entrez un nom explicite pour ce travail.  Ce champ doit obligatoirement être renseigné.       |
    |**Description**     |   Entrez une description explicite.      |
    |**Sélectionner le cluster.**     |Dans la liste déroulante, sélectionnez le cluster que vous souhaitez utiliser pour analyser les emplacements réseau configurés.  </br></br>**Conseil :** Lorsque vous sélectionnez un cluster, assurez-vous que les nœuds du cluster que vous affectez peuvent accéder aux plages d’adresses IP configurées via SMB.      |
    |**Configurer des plages d’adresses IP à découvrir**     |   Cliquez pour définir une adresse IP ou une plage. </br></br>Dans le volet **choisir des plages** d’adresses IP, entrez un nom facultatif, puis une adresse IP de début et une adresse IP de fin pour votre plage. </br></br>**Conseil :** Pour analyser uniquement une adresse IP spécifique, entrez l’adresse IP identique dans les champs adresse IP de **début** et adresse IP de **fin** .      |
    |**Définir la planification**     | Définissez la fréquence à laquelle vous souhaitez que ce travail d’analyse de réseau s’exécute.  </br></br>Si vous sélectionnez **hebdomadaire**, le paramètre **exécuter le travail d’analyse du réseau sur** s’affiche. Sélectionnez les jours de la semaine où vous souhaitez que le travail d’analyse du réseau s’exécute.       |
    |**Définir l’heure de début (UTC)**     |Définissez la date et l’heure de début de l’exécution de ce travail d’analyse de réseau. Si vous avez choisi d’exécuter le travail tous les jours, toutes les semaines ou tous les mois, le travail s’exécutera à l’heure définie, à la périodicité que vous avez sélectionnée. </br></br>**Remarque**: Soyez prudent lors de la définition de la date sur un jour à la fin du mois. Si vous sélectionnez **31,** le travail d’analyse du réseau ne s’exécutera pas dans un mois de 30 jours ou moins.    |
    | | |

1. Sélectionnez **Enregistrer** l' ![icône Enregistrer](media/qs-tutor/save-icon.png "icône Enregistrer") pour enregistrer vos modifications.

> [!TIP]
> Si vous souhaitez exécuter la même analyse réseau à l’aide d’un autre scanneur, modifiez le cluster défini dans le travail d’analyse réseau.
> 
> Revenez au volet **travaux d’analyse réseau** et sélectionnez **attribuer au cluster** pour sélectionner un autre cluster maintenant, ou annuler l' **affectation du cluster** pour apporter des modifications ultérieures. 
>     

### <a name="analyze-risky-repositories-found-public-preview"></a>Analyser les référentiels à risque trouvés (version préliminaire publique)

Les référentiels trouvés, par un travail d’analyse réseau, un travail d’analyse de contenu ou un accès utilisateur détecté dans les fichiers journaux, sont agrégés et répertoriés dans le volet de l' [icône](media/i-repositories.png "icône dépôts") du **scanneur >** référentiels dépôts.

Si vous avez [défini un travail d’analyse réseau](#create-a-network-scan-job-public-preview) et que vous l’avez configuré pour qu’il s’exécute à une date et une heure spécifiques, patientez jusqu’à la fin de l’exécution pour vérifier les résultats. Vous pouvez également revenir ici après avoir exécuté un [travail d’analyse de contenu](#create-a-content-scan-job) pour afficher les données mises à jour.

1. Dans le menu du **scanneur** situé à gauche, sélectionnez **référentiels** dépôts ![icône](media/i-repositories.png "icône dépôts").
    
    Les référentiels trouvés sont présentés comme suit :
    - Le graphique des **dépôts par État** indique le nombre de référentiels déjà configurés pour un travail d’analyse de contenu, ainsi que le nombre de référentiels non.
    - Les **10 principaux dépôts non gérés par Access** Graph répertorient les 10 principaux dépôts qui ne sont pas actuellement affectés à un travail d’analyse de contenu, ainsi que des détails sur leur niveau d’accès. Les niveaux d’accès peuvent indiquer le niveau de risque de vos référentiels.
    - Le tableau sous les graphiques répertorie chaque référentiel trouvé et les détails correspondants.

1. Faites ce qui suit :
    
    |Option  |Description  |
    |---------|---------|
    |![icône colonnes](media/i-columns.png "icône colonnes")    | Sélectionnez **colonnes** pour modifier les colonnes de table affichées.        |
    |![icône d’actualisation](media/i-refresh.png "icône d’actualisation")   | Si votre scanneur a récemment exécuté des résultats d’analyse réseau, sélectionnez **Actualiser** pour actualiser la page.      |
    |![icône d’ajout](media/i-add.png "icône d’ajout")   | Sélectionnez un ou plusieurs référentiels listés dans le tableau, puis sélectionnez **assigner les éléments sélectionnés** pour les affecter à un travail d’analyse de contenu.          |
    |**Filter**     |   La ligne de filtre indique les critères de filtrage actuellement appliqués. Sélectionnez l’un des critères affichés pour modifier ses paramètres, ou sélectionnez **Ajouter un filtre** pour ajouter de nouveaux critères de filtrage. </br></br>Sélectionnez **filtre** pour appliquer vos modifications et actualiser la table avec le filtre mis à jour.       |
    |![Icône Log Analytics](media/i-log-analytics.png "Icône Log Analytics") |Dans le coin supérieur droit du graphique dépôts non managés, cliquez sur l’icône **log Analytics** pour accéder à log Analytics données de ces dépôts. |
    | | |

#### <a name="repositories-with-public-access"></a>Dépôts avec accès public

Les référentiels pour lesquels un **accès public** est accessible **en lecture** ou **en lecture/écriture** peuvent avoir un contenu sensible qui doit être sécurisé. Si l' **accès public** a la valeur false, le référentiel n’est pas accessible par le public.

L’accès public à un référentiel est signalé uniquement si vous avez défini un compte faible dans le paramètre **StandardDomainsUserAccount** des applets de commande [**install-MIPNetworkDiscovery**](https://docs.microsoft.com/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) ou [**Set-MIPNetworkDiscovery**](https://docs.microsoft.com/powershell/module/azureinformationprotection/Set-MIPNetworkDiscovery) .

- Les comptes définis dans ces paramètres sont utilisés pour simuler l’accès d’un utilisateur faible au référentiel. Si l’utilisateur faible défini peut accéder au référentiel, cela signifie que le référentiel est accessible publiquement. 

- Pour vous assurer que l’accès public est correctement signalé, assurez-vous que l’utilisateur spécifié dans ces paramètres est membre du groupe **utilisateurs du domaine** uniquement.
       
### <a name="create-a-content-scan-job"></a>Créer un travail d’analyse de contenu

Explorez en profondeur votre contenu pour analyser des référentiels spécifiques pour obtenir du contenu sensible. 

Vous pouvez effectuer cette opération uniquement après avoir exécuté un travail d’analyse réseau pour analyser les référentiels de votre réseau, mais vous pouvez également définir vos référentiels vous-même.
 
1. Dans le menu du **scanneur** situé à gauche, sélectionnez **travaux d’analyse du contenu**. 
   
1. Dans le volet **Azure information protection-travaux d’analyse de contenu** , sélectionnez **Ajouter** une ![icône](media/i-add.png "icône Enregistrer").
 
1. Pour cette configuration initiale, configurez les paramètres suivants, puis sélectionnez **Enregistrer** sans fermer le volet.
    
    |Paramètre  |Description  |
    |---------|---------|
    |**Paramètres du travail d’analyse du contenu**     |    - **Planifier**: conserver la valeur par défaut **manuelle** </br>- **Types d’informations à découvrir**: changer en **stratégie uniquement** </br>- **Configurer les référentiels**: ne pas configurer pour l’instant, car le travail d’analyse de contenu doit d’abord être enregistré.         |
    |**Application de la stratégie**     | - **Appliquer**: sélectionner **désactivé** </br>- **Étiqueter les fichiers en fonction du contenu**: conservez la valeur par défaut **activée** </br>- **Étiquette par**défaut : conserver la valeur par défaut de la **stratégie** par défaut </br>- **Réétiqueter les fichiers**: conserver la valeur par défaut **désactivé**        |
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
    
        :::image type="content" source="media/scanner-repository-add.png" alt-text="Ajout d’un référentiel de données pour le scanneur Azure Information Protection":::

    1. Dans le volet **référentiel** , spécifiez le chemin d’accès du référentiel de données, puis sélectionnez **Enregistrer**.

        Par exemple : 

        - Pour un partage réseau, utilisez `\\Server\Folder` . 
        - Pour une bibliothèque SharePoint, utilisez `http://sharepoint.contoso.com/Shared%20Documents/Folder` .

        > [!NOTE]
        > Les caractères génériques ne sont pas pris en charge, ni les emplacements WebDav.
        >     

        Pour les autres paramètres de ce volet, ne les modifiez pas pour cette configuration initiale, mais conservez-les en tant que **travail d’analyse du contenu par défaut**. Le paramètre par défaut signifie que le référentiel de données hérite des paramètres du travail d’analyse de contenu.

        Pour ajouter des chemins d’accès SharePoint, utilisez la syntaxe ci-après :
    
        |Path  |Syntaxe  |
        |---------|---------|
        |**Chemin d’accès racine**     | `http://<SharePoint server name>` </br></br>Analyse tous les sites, y compris les collections de sites autorisées pour l’utilisateur du scanneur. </br>Nécessite [des autorisations supplémentaires](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) pour découvrir automatiquement le contenu racine        |
        |**Sous-site ou regroupement SharePoint spécifique**     | Celui-ci peut avoir l'une des valeurs suivantes : </br>- `http://<SharePoint server name>/<subsite name>` </br>- `http://SharePoint server name>/<site collection name>/<site name>` </br></br>Nécessite [des autorisations supplémentaires](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) pour découvrir automatiquement le contenu de la collection de sites         |
        |**Bibliothèque SharePoint spécifique**     | Celui-ci peut avoir l'une des valeurs suivantes : </br>- `http://<SharePoint server name>/<library name>` </br>- `http://SharePoint server name>/.../<library name>`       |
        |**Dossier SharePoint spécifique**     | `http://<SharePoint server name>/.../<folder name>`        |
        | | |


1. Répétez les étapes précédentes pour ajouter autant de référentiels que nécessaire.

    Lorsque vous avez terminé, fermez les volets du travail **référentiels** et **analyse du contenu** . 

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
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```
    
    Exemples utilisant le nom de profil **Europe** :
    
    - Pour une instance par défaut : `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - Pour une instance nommée : `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - Pour SQL Server Express : `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    Lorsque vous y êtes invité, fournissez les informations d’identification du compte de service du scanneur ( \<domain\user name> ) et du mot de passe.

1. Vérifiez que le service est maintenant installé à l’aide des **Outils d’administration**  >  **services**. 
    
    Le service installé est nommé **Scanneur Azure Information Protection** et il est configuré pour s’exécuter en utilisant le compte de service du scanneur que vous avez créé.

Maintenant que vous avez installé le scanneur, vous devez [obtenir un jeton de Azure AD pour que le compte de service du scanneur](#get-an-azure-ad-token-for-the-scanner) s’authentifie, afin que le scanneur puisse s’exécuter sans assistance. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Obtenir un jeton Azure AD pour le scanneur

Un jeton de Azure AD permet à l’analyseur de s’authentifier auprès du service Azure Information Protection, ce qui permet à l’analyseur de s’exécuter de manière non interactive.

Pour plus d’informations, consultez [Comment étiqueter des fichiers de manière non interactive pour Azure information protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

Pour recevoir un jeton de Azure AD :

1. Revenez à la Portail Azure pour créer une application Azure AD afin de spécifier un jeton d’accès pour l’authentification.

1. À partir de l’ordinateur Windows Server, si votre compte de service de scanneur a reçu le droit **ouvrir une session localement** pour l’installation, connectez-vous avec ce compte et démarrez une session PowerShell. 

    Exécutez [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), en spécifiant les valeurs copiées à partir de l’étape précédente :
    
    ```ps
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
        
    Par exemple :

    ```ps
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

> [!TIP]
> Si votre compte de service de scanneur ne peut pas se voir accorder le droit **ouvrir une session localement** pour l’installation, utilisez le paramètre *OnBehalfOf* avec [Set-AIPAuthentication](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipauthentication), comme décrit dans [Comment étiqueter des fichiers de manière non interactive pour Azure information protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

Le scanneur dispose désormais d’un jeton pour s’authentifier auprès de Azure AD. Ce jeton est valide pendant un an, deux ans ou jamais, en fonction de votre configuration de la clé secrète client de l' **application Web/API** dans Azure ad. 

Lorsque le jeton expire, vous devez répéter cette procédure.

Vous pouvez maintenant exécuter votre première analyse en mode découverte. Pour plus d’informations, consultez [exécuter un cycle de découverte et afficher les rapports du scanneur](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner).

Une fois que vous avez exécuté votre analyse de découverte initiale, poursuivez [la configuration du scanneur pour appliquer la classification et la protection](#configure-the-scanner-to-apply-classification-and-protection).

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurer le scanneur pour appliquer la classification et la protection

Les paramètres par défaut configurent le scanneur pour qu’il s’exécute une seule fois et en mode rapport uniquement.

Pour modifier ces paramètres, modifiez le travail d’analyse du contenu :

1. Dans le Portail Azure, dans le volet **Azure information protection de travaux d’analyse de contenu** , sélectionnez le travail de cluster et d’analyse de contenu pour le modifier.

2. Dans le volet du travail analyse du contenu, modifiez les éléments suivants, puis sélectionnez **Enregistrer**:
    
   - Dans la section **travail d’analyse du contenu** : modifiez la **planification** pour **toujours**
   - À partir de la section application de la **stratégie** : modifier **appliquer** la valeur **activé**
    
    > [!TIP]
    > Vous pouvez modifier d’autres paramètres dans ce volet, par exemple si les attributs de fichier sont modifiés et si le scanneur peut réétiqueter les fichiers. Utilisez l’aide contextuelle des informations pour plus d’informations sur chaque paramètre de configuration.

3. Prenez note de l’heure actuelle et redémarrez le scanneur à partir du volet **travaux d’analyse de contenu Azure information protection** :

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Lancement de l’analyse du scanneur Azure Information Protection":::
    
    Vous pouvez également exécuter la commande suivante dans votre session PowerShell :
    
    ```ps
    Start-AIPScan
    ```

Le scanneur est maintenant programmé pour s’exécuter en continu. Lorsque le scanneur fonctionne dans tous les fichiers configurés, il démarre automatiquement un nouveau cycle afin que tous les fichiers nouveaux et modifiés soient découverts.

## <a name="change-which-file-types-to-protect"></a>Changer les types de fichiers à protéger

Par défaut, le scanneur AIP protège les types de fichiers Office et les fichiers PDF uniquement.

Utilisez les commandes PowerShell pour modifier ce comportement en fonction des besoins, par exemple pour configurer le scanneur afin de protéger tous les types de fichiers, tout comme le fait le client, ou pour protéger des types de fichiers supplémentaires spécifiques. 

Pour une stratégie d’étiquette qui s’applique au compte d’utilisateur qui télécharge des étiquettes pour le scanneur, spécifiez un paramètre avancé PowerShell nommé **PFileSupportedExtensions**. 

Pour un scanneur qui a accès à Internet, ce compte d’utilisateur est le compte que vous spécifiez pour le paramètre *DelegatedUser* avec la commande Set-AIPAuthentication.

**Exemple 1 :**  Commande PowerShell pour que le scanneur protège tous les types de fichiers, où votre stratégie d’étiquette est nommée « scanner » :

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**Exemple 2 :** Commande PowerShell permettant au scanneur de protéger les fichiers. xml et. TIFF en plus des fichiers Office et des fichiers PDF, où votre stratégie d’étiquette est nommée « scanner » :

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}
```

Pour plus d’informations, consultez [modifier les types de fichiers à protéger](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

## <a name="upgrading-your-scanner"></a>Mise à niveau de votre scanneur
 
Si vous avez déjà installé le scanneur et que vous souhaitez effectuer une mise à niveau, suivez les instructions décrites dans [mise à niveau de l’analyseur de Azure information protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

Ensuite, [configurez](deploy-aip-scanner-configure-install.md) et [Utilisez votre scanneur](deploy-aip-scanner-manage.md) comme d’habitude, en ignorant les étapes d’installation de votre scanneur.

## <a name="editing-data-repository-settings-in-bulk"></a>Modification des paramètres du référentiel de données en bloc

Utilisez les boutons **Exporter** et **Importer** pour apporter des modifications à votre scanneur sur plusieurs dépôts. 

De cette façon, vous n’avez pas besoin d’effectuer plusieurs fois les mêmes modifications, manuellement, dans le Portail Azure.

Par exemple, si vous avez un nouveau type de fichier dans plusieurs référentiels de données SharePoint, vous souhaiterez peut-être mettre à jour les paramètres de ces dépôts en bloc.

Pour apporter des modifications en bloc dans les référentiels :

1. Dans le Portail Azure du volet **référentiels** , sélectionnez l’option d' **exportation** . Par exemple :

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="Exportation des paramètres du référentiel de données pour le scanneur de Azure Information Protection":::

1. Modifiez manuellement le fichier exporté pour effectuer votre modification. 

1. Utilisez l’option d' **importation** sur la même page pour réimporter les mises à jour dans vos référentiels.

## <a name="using-the-scanner-with-alternative-configurations"></a>Utilisation du scanneur avec d’autres configurations

Le scanneur de Azure Information Protection recherche généralement des conditions spécifiées pour vos étiquettes afin de classer et de protéger votre contenu si nécessaire.

Dans les scénarios suivants, le Azure Information Protection scanner est également en mesure d’analyser votre contenu et de gérer des étiquettes, sans aucune condition configurée :

- [Appliquer une étiquette par défaut à tous les fichiers d’un référentiel de données](#apply-a-default-label-to-all-files-in-a-data-repository)
- [Supprimer des étiquettes existantes de tous les fichiers d’un référentiel de données](#remove-existing-labels-from-all-files-in-a-data-repository)
- [Identifiez toutes les conditions personnalisées et les types d’informations sensibles connus](#identify-all-custom-conditions-and-known-sensitive-information-types)
### <a name="apply-a-default-label-to-all-files-in-a-data-repository"></a>Appliquer une étiquette par défaut à tous les fichiers d’un référentiel de données

Dans cette configuration, tous les fichiers sans étiquette du référentiel sont étiquetés avec l’étiquette par défaut spécifiée pour le référentiel ou le travail d’analyse du contenu. Les fichiers sont étiquetés sans inspection. 

Configurez les paramètres suivants : 

|Paramètre  |Description  |
|---------|---------|
|**Étiqueter les fichiers en fonction du contenu**    |**Désactivée**         |
|**Étiquette par défaut**     | Définissez sur **personnalisé**, puis sélectionnez l’étiquette à utiliser.       |
|**Appliquer l’étiquette par défaut**     | Sélectionnez cette option pour appliquer l’étiquette par défaut à tous les fichiers, même s’ils sont déjà étiquetés.        |
| | |

### <a name="remove-existing-labels-from-all-files-in-a-data-repository"></a>Supprimer des étiquettes existantes de tous les fichiers d’un référentiel de données

Dans cette configuration, toutes les étiquettes existantes sont supprimées, y compris la protection, si la protection a été appliquée avec l’étiquette. La protection appliquée indépendamment d’une étiquette est conservée.

Configurez les paramètres suivants : 

|Paramètre  |Description  |
|---------|---------|
|**Étiqueter les fichiers en fonction du contenu**    |**Désactivée**         |
|**Étiquette par défaut**     | Définir sur **aucun**  |
|**Réétiqueter les fichiers** | Affectez la valeur **on**à la case à cocher **appliquer l’étiquette par défaut** activée|
| | |

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>Identifiez toutes les conditions personnalisées et les types d’informations sensibles connus

Cette configuration vous permet de trouver des informations sensibles que vous n’avez pas pu constater, aux dépens des taux de numérisation pour le scanneur. 

Définissez les **types d’informations à découvrir** pour **tous**. 

Pour identifier les conditions et les types d’informations pour l’étiquetage, le scanneur utilise tous les types d’informations sensibles personnalisés spécifiés, ainsi que la liste des types d’informations sensibles intégrés disponibles à sélectionner, tels que définis dans le centre de gestion des étiquettes.

## <a name="optimizing-scanner-performance"></a>Optimisation des performances de l’analyseur

> [!NOTE]
> Si vous cherchez à améliorer la réactivité de l’ordinateur du scanneur plutôt que les performances de l’analyseur, utilisez un paramètre client avancé pour [limiter le nombre de threads utilisés par le scanneur](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner).
> 

Utilisez les options et les conseils suivants pour vous aider à optimiser les performances de l’analyseur :

|Option  |Description  |
|---------|---------|
|**Veillez à avoir une connexion haut débit fiable entre l’ordinateur de l’analyseur et le magasin de données analysé**     |  Par exemple, placez l’ordinateur du scanneur sur le même réseau local, ou de préférence, dans le même segment de réseau que le magasin de données analysé. </br></br>La qualité de la connexion réseau affecte les performances de l’analyseur car, pour inspecter les fichiers, l’analyseur transfère le contenu des fichiers sur l’ordinateur exécutant le service du scanneur. </br></br>La réduction ou l’élimination des sauts réseau requis pour le déplacement des données réduit également la charge sur votre réseau.      |
|**Assurez-vous que l’ordinateur de l’analyseur dispose de ressources processeur**     | L’inspection du contenu du fichier et le chiffrement et le déchiffrement des fichiers sont des actions nécessitant beaucoup de ressources du processeur. </br></br>Surveillez les cycles d’analyse typiques pour les magasins de données spécifiés pour déterminer si un manque de ressources du processeur affecte les performances de l’analyseur.        |
|**Installer plusieurs instances du scanneur** | Le scanneur Azure Information Protection prend en charge plusieurs bases de données de configuration sur la même instance de SQL Server lorsque vous spécifiez un nom de cluster personnalisé (profil) pour le scanneur. </br></br>Plusieurs analyseurs peuvent également partager le même cluster (profil), ce qui permet des temps d’analyse plus rapides.|
|**Vérifier l’utilisation de la configuration de remplacement** |Le scanneur s’exécute plus rapidement lorsque vous utilisez la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) pour appliquer une étiquette par défaut à tous les fichiers, car le scanneur n’inspecte pas le contenu du fichier. <br/></br>Le scanneur s’exécute plus lentement lorsque la [configuration de remplacement](#using-the-scanner-with-alternative-configurations) est utilisée pour identifier toutes les conditions personnalisées et tous les types d’informations sensibles connus.|
| | |


### <a name="additional-factors-that-affect-performance"></a>Facteurs supplémentaires qui affectent les performances

Les facteurs supplémentaires qui affectent les performances du scanneur sont les suivants :

|Factor  |Description  |
|---------|---------|
|**Temps de chargement/réponse**     |Les temps de chargement et de réponse actuels des magasins de données qui contiennent les fichiers à analyser affectent également les performances du scanneur.         |
|**Mode scanneur** (détection/application)    | Le mode de détection a généralement un taux d’analyse plus élevé que le mode d’application. </br></br>La découverte requiert une seule action de lecture de fichier, tandis que le mode d’application requiert des actions de lecture et d’écriture.        |
|**Modifications de stratégie**     |Les performances de votre scanneur peuvent être affectées si vous avez apporté des modifications à l’étiquetage automatique dans la stratégie d’étiquette. </br></br>Votre premier cycle d’analyse, lorsque le scanneur doit inspecter chaque fichier, prend plus de temps que les cycles d’analyse suivants qui, par défaut, inspectent uniquement les fichiers nouveaux et modifiés. </br></br>Si vous modifiez les conditions ou les paramètres d’étiquetage automatique, tous les fichiers sont analysés à nouveau. Pour plus d’informations, consultez [rescaning Files](deploy-aip-scanner-manage.md#rescanning-files).|
|**Constructions Regex**    | Les performances de l’analyseur sont affectées par la manière dont vos expressions Regex pour les conditions personnalisées sont construites. </br></br> Pour éviter une consommation de mémoire importante et le risque de dépassements du délai d’expiration (15 minutes par fichier), passez en revue vos expressions regex pour vérifier que la correspondance des modèles est efficace. </br></br>Par exemple : </br>-Évitez les [quantificateurs gourmands](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions) </br>-Utiliser des groupes sans capture comme `(?:expression)` au lieu de `(expression)`    |
|**Niveau de journalisation**     |  Les options de niveau de journalisation sont **Debug**, **info**, **Error** et **off** pour les rapports du scanneur.</br></br>- La valeur **off** permet d’obtenir des performances optimales </br>- Le **débogage** ralentit considérablement le scanneur et doit être utilisé uniquement pour la résolution des problèmes. </br></br>Pour plus d’informations, consultez le paramètre *ReportLevel* de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).       |
|**Fichiers en cours d’analyse**     |-À l’exception des fichiers Excel, les fichiers Office sont analysés plus rapidement que les fichiers PDF. </br></br>-Les fichiers non protégés sont plus rapides à analyser que les fichiers protégés. </br></br>-Les fichiers volumineux sont évidemment plus longs à analyser que les petits fichiers.         |
| | |

## <a name="list-of-cmdlets-for-the-scanner"></a>Liste des cmdlets pour le scanneur

Cette section répertorie les applets de commande PowerShell prises en charge pour le scanneur Azure Information Protection.

> [!NOTE]
> Le scanneur de Azure Information Protection est configuré à partir de la Portail Azure. Par conséquent, les applets de commande utilisées dans les versions précédentes pour configurer les référentiels de données et la liste des types de fichiers analysés sont désormais dépréciées.
> 

Les applets de commande prises en charge pour le scanneur sont les suivantes :

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [MIPNetworkDiscoveryConfiguration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryConfiguration)

- [MIPNetworkDiscoveryJobs](https://docs.microsoft.com/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryJobs)

- [MIPNetworkDiscoveryStatus](https://docs.microsoft.com/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryStatus)

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Import-MIPNetworkDiscoveryConfiguration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Import-MIPNetworkDiscoveryConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Install-MIPNetworkDiscovery](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Set-MIPNetworkDiscoveryConfiguration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Start-AIPScanDiagnostics](/powershell/module/azureinformationprotection/Start-AIPScannerDiagnostics)

- [Start-MIPNetworkDiscovery](https://docs.microsoft.com/powershell/module/azureinformationprotection/Start-MIPNetworkDiscovery)

- [Stop-AIPScan](/powershell/module/azureinformationprotection/Stop-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Uninstall-MIPNetworkDiscovery](https://docs.microsoft.com/powershell/module/azureinformationprotection/Uninstall-MIPNetworkDiscovery)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez installé et configuré votre scanneur, commencez à [analyser vos fichiers](deploy-aip-scanner-manage.md).

Voir aussi : [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md).

**Plus d’informations :**

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- Utilisez PowerShell pour classifier et protéger de manière interactive les fichiers de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md).
