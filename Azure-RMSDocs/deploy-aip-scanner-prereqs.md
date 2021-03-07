---
title: Prérequis du scanneur d’étiquetage unifiée Azure Information Protection (AIP)
description: Répertorie les conditions préalables à l’installation et au déploiement du scanneur d’étiquetage unifié Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/27/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4e8c4444aad6185b54a6f5b5178fa225857b71d2
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414954"
---
# <a name="requirements-for-installing-and-deploying-the-azure-information-protection-unified-labeling-scanner"></a>Configuration requise pour l’installation et le déploiement du scanneur d’étiquetage unifié Azure Information Protection

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez [conditions préalables pour le scanneur client Classic](deploy-aip-scanner-prereqs-classic.md) .*

Avant d’installer le Azure Information Protection scanneur local, assurez-vous que votre système est conforme aux exigences de base de [Azure information protection](requirements.md).

En outre, les conditions requises suivantes sont spécifiques au scanneur :

- [Configuration requise pour Windows Server](#windows-server-requirements)
- [Exigences relatives au compte de service](#service-account-requirements)
- [Configuration requise pour SQL Server](#sql-server-requirements)
- [Exigences du client Azure Information Protection](#azure-information-protection-client-requirements)
- [Configuration requise pour l’étiquette](#label-configuration-requirements)
- [Configuration requise pour SharePoint](#sharepoint-requirements)
- [Configuration requise pour la Microsoft Office](#microsoft-office-requirements)
- [Exigences relatives au chemin de fichier](#file-path-requirements)

Si vous ne pouvez pas répondre à toutes les conditions requises répertoriées pour le scanneur parce qu’elles sont interdites par les stratégies de votre organisation, consultez la section [autres configurations](#deploying-the-scanner-with-alternative-configurations) .

Lors du déploiement du scanneur en production ou du test des performances de plusieurs scanneurs, consultez [exigences de stockage et planification de la capacité pour SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

Lorsque vous êtes prêt à commencer l’installation et le déploiement de votre scanneur, poursuivez [le déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner-configure-install.md).

## <a name="windows-server-requirements"></a>Configuration requise pour Windows Server

Vous devez disposer d’un ordinateur Windows Server pour exécuter le scanneur, qui présente les spécifications système suivantes :

|Caractéristique  |Détails  |
|---------|---------|
|**Processeur**     |4 processeurs principaux         |
|**RAM**     |8 Go         |
|**Espace disque**     |10 Go d’espace libre (moyenne) pour les fichiers temporaires. </br></br>Le scanneur nécessite suffisamment d’espace disque disponible pour créer des fichiers temporaires pour chaque fichier qu’il analyse, quatre fichiers par cœur. </br></br>L’espace disque recommandé de 10 Go permet de disposer de processeurs 4 cœurs analysant 16 fichiers qui ont chacun une taille de 625 Mo.
|**Système d'exploitation**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**Remarque**: à des fins de test ou d’évaluation dans un environnement hors production, vous pouvez également utiliser n’importe quel système d’exploitation Windows [pris en charge par le client Azure information protection](requirements.md#client-devices).
|**Connectivité réseau**     | Votre ordinateur de scanneur peut être un ordinateur physique ou virtuel avec une connexion réseau rapide et fiable aux magasins de données à analyser. </br></br> Si la connexion Internet n’est pas possible en raison des stratégies de votre organisation, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations). </br></br>Dans le cas contraire, assurez-vous que cet ordinateur dispose d’une connectivité Internet qui autorise les URL suivantes sur HTTPs (port 443) :</br><br />-  \*. aadrm.com <br />-  \*. azurerms.com<br />-  \*. informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*. aria.microsoft.com <br />-  \*. protection.outlook.com |
|**Partages NFS** |Pour prendre en charge les analyses sur les partages NFS, les services pour NFS doivent être déployés sur l’ordinateur du scanneur. <br><br>Sur votre ordinateur, accédez à la boîte de dialogue des paramètres **fonctionnalités Windows (activer ou désactiver des fonctionnalités Windows)** , puis sélectionnez les éléments suivants :   >  **Outils d’administration** de NFS et **client pour NFS**. |
| | |

## <a name="service-account-requirements"></a>Configuration requise pour les comptes de service

Vous devez disposer d’un compte de service pour exécuter le service du scanneur sur l’ordinateur Windows Server, ainsi que pour vous authentifier auprès de Azure AD et télécharger la stratégie Azure Information Protection.

Votre compte de service doit être un compte Active Directory et être synchronisé avec Azure AD.

Si vous ne pouvez pas synchroniser ce compte en raison des stratégies de votre organisation, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).

Ce compte de service a la configuration suivante :

|Condition requise  |Détails  |
|---------|---------|
|Attribution **de droits d’utilisateur d’ouverture de session locale**     |Requis pour installer et configurer le scanneur, mais pas pour exécuter des analyses.  </br></br>Une fois que vous avez confirmé que le scanneur peut détecter, classer et protéger les fichiers, vous pouvez supprimer ce droit du compte de service.  </br></br>S’il n’est pas possible d’accorder ce droit même pendant une brève période de temps en raison des stratégies de votre organisation, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).         |
|**Ouvrir une session en tant que service**, attribution des droits utilisateur.     |  Ce droit est accordé automatiquement au compte de service pendant l’installation du scanneur et il est exigé pour l’installation, la configuration et le fonctionnement du scanneur.        |
|**Autorisations pour les référentiels de données**     |- **Partages de fichiers ou fichiers locaux**: accordez les autorisations **lire**, **écrire** et **modifier** pour analyser les fichiers, puis appliquer la classification et la protection conformément à la configuration.  <br /><br />- **SharePoint**: vous devez accorder des autorisations **contrôle total** pour analyser les fichiers, puis appliquer la classification et la protection aux fichiers qui remplissent les conditions de la stratégie de Azure information protection.  <br /><br />- **Mode de découverte**: pour exécuter le scanneur en mode détection uniquement, l’autorisation **lecture** est suffisante.         |
|**Pour les étiquettes qui reprotègent ou suppriment la protection**     | Pour vous assurer que le scanneur a toujours accès aux fichiers protégés, définissez ce compte comme [super utilisateur](configure-super-users.md) pour Azure information protection et assurez-vous que la fonctionnalité de super utilisateur est activée. </br></br>En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que le compte de service est inclus dans les contrôles d’intégration que vous avez configurés.|
|**Analyse de niveau d’URL spécifique**: |Pour analyser et découvrir des sites et des sous-sites [sous une URL spécifique](#deploying-the-scanner-with-alternative-configurations), accordez des droits d' **auditeur du collecteur de sites** au compte de l’analyseur au niveau de la batterie de serveurs.|
| | |

## <a name="sql-server-requirements"></a>Configuration requise pour SQL Server

Pour stocker les données de configuration de l’analyseur, utilisez un serveur SQL Server avec les spécifications suivantes :

- **Instance locale ou distante.**

    Nous vous recommandons d’héberger SQL Server et le service de scanneur sur des ordinateurs différents, sauf si vous utilisez un petit déploiement. En outre, nous vous recommandons d’avoir une instance SQL dédiée qui sert uniquement la base de données du scanneur et qui n’est pas partagée avec d’autres applications.

    Si vous travaillez sur un serveur partagé, assurez-vous que le [nombre de cœurs recommandé](#windows-server-requirements) est gratuit pour que la base de données du scanneur fonctionne.

    SQL Server 2016 est la version minimale pour les éditions suivantes :

    - SQL Server Entreprise

    - SQL Server Standard

    - SQL Server Express (recommandé pour les environnements de test uniquement)

- **Un compte avec le rôle sysadmin pour installer le scanneur.**

    Le rôle sysadmin permet au processus d’installation de créer automatiquement la base de données de configuration du scanneur et d’accorder le rôle de **db_owner** requis au compte de service qui exécute le scanneur.

    Si vous ne pouvez pas accorder le rôle sysadmin ou si les stratégies de votre organisation nécessitent la création et la configuration de bases de données manuellement, consultez [déploiement du scanneur avec d’autres configurations](#deploying-the-scanner-with-alternative-configurations).

- **Capacité.** Pour obtenir des conseils sur la capacité, consultez [exigences de stockage et planification de la capacité pour SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).

- **[Classement non sensible](/sql/relational-databases/collations/collation-and-unicode-support)à la casse.**

> [!NOTE]
> Plusieurs bases de données de configuration sur le même serveur SQL Server sont prises en charge lorsque vous spécifiez un nom de cluster personnalisé pour le scanneur, ou lorsque vous utilisez la version préliminaire du scanneur.
>
### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Exigences de stockage et planification de la capacité pour SQL Server

La quantité d’espace disque requise pour la base de données de configuration du scanneur et la spécification de l’ordinateur qui exécute SQL Server peuvent varier pour chaque environnement, nous vous encourageons donc à effectuer vos propres tests. Utilisez les instructions suivantes comme point de départ.

Pour plus d’informations, consultez [optimisation des performances du scanneur](deploy-aip-scanner-configure-install.md#optimize-scanner-performance).

La taille du disque de la base de données de configuration de l’analyseur varie pour chaque déploiement. Utilisez l’équation suivante en guise d’aide :

```cli
100 KB + <file count> *(1000 + 4* <average file name length>)
```

Par exemple, pour analyser les fichiers 1 million dont la longueur moyenne du nom de fichier est de 250 octets, allouez un espace disque de 2 Go.

Pour plusieurs Scanneurs :

- **Jusqu’à 10 scanneurs**, utilisez :

    - 4 processeurs principaux
    - 8 Go de RAM recommandés

- **Plus de 10 scanneurs** (40 maximum), utilisez :
    - 8 processus de base
    - 16 Go de RAM recommandés

## <a name="azure-information-protection-client-requirements"></a>Exigences du client Azure Information Protection

Vous devez disposer de la [version actuelle de la disponibilité générale](./rms-client/unifiedlabelingclient-version-release-history.md) du client Azure information Protection installé sur l’ordinateur Windows Server.

Pour plus d’informations, consultez le [Guide d’administration du client d’étiquetage unifié](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner).

> [!IMPORTANT]
> Vous devez installer le client complet pour le scanneur. N’installez pas le client avec juste le module PowerShell.
>

## <a name="label-configuration-requirements"></a>Configuration requise pour l’étiquette

Au moins une étiquette de sensibilité doit être configurée dans l’un des Microsoft 365 l’étiquetage des centres d’administration pour le compte du scanneur, pour appliquer la classification et, éventuellement, la protection.

Microsoft 365 l’étiquetage des centres d’administration, citons les Microsoft 365 Security Center, le centre de conformité Microsoft 365 et le centre de conformité et de sécurité Microsoft 365. 

Le *compte du scanneur* est le compte que vous spécifiez dans le paramètre **DelegatedUser** de l’applet de commande [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) , exécuté lors de la configuration de votre scanneur. 

Si vos étiquettes n’ont pas de conditions d’étiquetage automatique, consultez les [instructions pour les autres configurations](#restriction-your-labels-do-not-have-auto-labeling-conditions) ci-dessous.

Pour plus d’informations, consultez :

- [En savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels)
- [Appliquer automatiquement une étiquette sensibilité au contenu](/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [Restriction de l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](/microsoft-365/compliance/encryption-sensitivity-labels)
- [Configuration et installation du scanneur d’étiquetage unifié Azure Information Protection](deploy-aip-scanner-configure-install.md)

## <a name="sharepoint-requirements"></a>Configuration requise pour SharePoint

Pour analyser les dossiers et bibliothèques de documents SharePoint, assurez-vous que votre serveur SharePoint est conforme aux exigences suivantes :

|Condition requise  |Description  |
|---------|---------|
|**Versions prises en charge** | Les versions prises en charge sont les suivantes : SharePoint 2019, SharePoint 2016 et SharePoint 2013. <br> D’autres versions de SharePoint ne sont pas prises en charge pour le scanneur.     |
|**Contrôle de version**     |  Lorsque vous utilisez le contrôle de [version](/sharepoint/governance/versioning-content-approval-and-check-out-planning), le scanneur inspecte et étiquette la dernière version publiée. <br><br>Si le scanneur étiquette une approbation de fichier et de [contenu](/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) est requise, ce fichier doit être approuvé pour être disponible pour les utilisateurs.       |
|**Batteries de serveurs SharePoint de grande taille** |Pour les grandes batteries de serveurs SharePoint, regardez si vous devez augmenter le seuil d’affichage de liste (par défaut, 5 000) pour le scanneur pour accéder à tous les fichiers. <br><br>Pour plus d’informations, consultez [gérer des listes et des bibliothèques de grande taille dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server). |
|**Chemins d’accès de fichiers longs**  |Si vous avez des chemins d’accès de fichiers longs dans SharePoint, assurez-vous que la valeur [httpRuntime. maxUrlLength](/dotnet/api/system.web.configuration.httpruntimesection.maxurllength) de votre serveur SharePoint est supérieure à la valeur par défaut de 260 caractères. <br><br>Pour plus d’informations, consultez [éviter les délais d’attente des scanneurs dans SharePoint](rms-client/clientv2-admin-guide-customizations.md#avoid-scanner-timeouts-in-sharepoint). | 
| | |

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
|**Windows 10 ou Windows Server 2016**     | Définissez le [paramètre de stratégie de groupe](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)suivant : stratégie de l' **ordinateur local**  >  **Configuration ordinateur**  >  **modèles d’administration**  >  **tous les paramètres**  >  **activer les chemins d’accès longs Win32**.    </br></br>Pour plus d’informations sur la prise en charge des chemins de fichiers longs dans ces versions, consultez la section limitation de la [longueur maximale du chemin d’accès](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation du développeur Windows 10.    |
|**Windows 10, version 1607 ou ultérieure**     |  Abonnez-vous à la fonctionnalité de **MAX_PATH** mise à jour. Pour plus d’informations, consultez [activer des chemins d’accès longs dans Windows 10 versions 1607 et ultérieures](/windows/win32/fileio/naming-a-file#enable-long-paths-in-windows-10-version-1607-and-later).      |
| | |


## <a name="deploying-the-scanner-with-alternative-configurations"></a>Déploiement du scanneur avec d’autres configurations

Les conditions préalables répertoriées ci-dessus sont les conditions par défaut pour le déploiement de l’analyseur, et recommandées car elles prennent en charge la configuration d’analyseur la plus simple.

Les spécifications par défaut doivent être adaptées au test initial, afin que vous puissiez vérifier les fonctionnalités du scanneur.

Toutefois, dans un environnement de production, les stratégies de votre organisation peuvent être différentes des exigences par défaut. Le scanneur peut prendre en charge les modifications suivantes avec une configuration supplémentaire :

- [Détection et analyse de tous les sites et sous-sites sous une URL spécifique](#discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url)

- [Restriction : le serveur de scanneur ne peut pas disposer d’une connexion Internet](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory mais le serveur dispose d’une connexion Internet](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [Restriction : le compte de service du scanneur ne peut pas se voir accorder le droit **ouvrir une session localement**](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

- [Restriction : vos étiquettes n’ont pas de conditions d’étiquetage automatique](#restriction-your-labels-do-not-have-auto-labeling-conditions)

### <a name="discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url"></a>Détection et analyse de tous les sites et sous-sites SharePoint sous une URL spécifique

Le scanneur peut détecter et analyser tous les sites et sous-sites SharePoint sous une URL spécifique avec la configuration suivante :

1. Démarrez l' **administration centrale de SharePoint**.

1. Sur le site Web **administration centrale de SharePoint** , dans la section **gestion des applications** , cliquez sur **gérer les applications Web**.

1. Cliquez pour mettre en surbrillance l’application Web dont vous souhaitez gérer le niveau de stratégie d’autorisation.

1. Choisissez la batterie de serveurs appropriée, puis sélectionnez **gérer les niveaux de stratégie des autorisations**.

1. Sélectionnez l' **auditeur de collection de sites** dans les options autorisations pour la collection de **sites** , puis octroyer afficher les **pages d’application** dans la liste des autorisations. Enfin, nommez le nouveau scanneur AIP du niveau de stratégie **auditeur et visionneuse de sites**.

1. Ajoutez votre utilisateur de scanneur à la nouvelle stratégie et accordez la **collection de sites** dans la liste des autorisations.   

1. Ajoutez une URL de SharePoint qui héberge des sites ou des sous-sites qui doivent être analysés. Pour plus d’informations, consultez [configurer le scanneur dans le portail Azure](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

Pour en savoir plus sur la gestion de vos niveaux de stratégie SharePoint, consultez [gérer les stratégies d’autorisation pour une application Web](/sharepoint/administration/manage-permission-policies-for-a-web-application).

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction : le serveur de scanneur ne peut pas disposer d’une connexion Internet

Alors que le client d’étiquetage unifié ne peut pas appliquer la protection sans connexion Internet, le scanneur peut toujours appliquer des étiquettes basées sur des stratégies importées.

Pour prendre en charge un ordinateur déconnecté, utilisez l’une des méthodes suivantes :

- [Utiliser le portail Azure](#use-the-azure-portal-with-a-disconnected-computer) (recommandé dans la mesure du possible)

- [Utiliser PowerShell](#use-powershell-with-a-disconnected-computer)

#### <a name="use-the-azure-portal-with-a-disconnected-computer"></a>Utiliser le Portail Azure avec un ordinateur déconnecté

Pour prendre en charge un ordinateur déconnecté du Portail Azure, procédez comme suit :

1.  Configurez des étiquettes dans votre stratégie, puis utilisez la [procédure pour prendre en charge les ordinateurs déconnectés](rms-client/clientv2-admin-guide-customizations.md#support-for-disconnected-computers) afin d’activer la classification et l’étiquetage hors connexion.

1. Activez la gestion hors connexion pour le contenu et les travaux d’analyse réseau comme suit :

    **Activer la gestion hors connexion pour les travaux d’analyse de contenu**:

    1. Configurez le scanneur pour qu’il fonctionne en mode **hors connexion** à l’aide de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) .

    1. Configurez le scanneur dans le Portail Azure en créant un cluster de scanneur. Pour plus d’informations, consultez [configurer le scanneur dans le portail Azure](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

    1. Exportez votre travail de contenu à partir du volet **Azure information protection-travaux d’analyse de contenu** à l’aide de l’option d' **exportation** .
    
    1. Importez la stratégie à l’aide de l’applet [de commande Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/import-aipscannerconfiguration) . 
    
    Les résultats des travaux d’analyse de contenu hors connexion se trouvent à l’emplacement suivant : **%LocalAppData%\Microsoft\MSIP\Scanner\Reports**
    
    **Activer la gestion hors connexion des travaux d’analyse réseau**:

    1. Configurez le service de découverte du réseau (version préliminaire publique) pour qu’il fonctionne en mode hors connexion à l’aide de l’applet de commande [Set-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/set-mipnetworkdiscoveryconfiguration) .

    1. Configurez le travail Network Scan dans le Portail Azure. Pour plus d’informations, consultez [création d’un travail d’analyse réseau](deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview).
    
    1. Exportez votre travail d’analyse réseau à partir du volet **Azure information protection-tâches d’analyse réseau (** préversion) à l’aide de l’option d' **exportation** . 
    
    1.  Importez le travail d’analyse réseau à l’aide du fichier qui correspond à notre nom de cluster à l’aide de l’applet [de commande Import-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/import-mipnetworkdiscoveryconfiguration) .  
    
    Les résultats des travaux d’analyse réseau hors connexion se trouvent à l’emplacement suivant : **%LocalAppData%\Microsoft\MSIP\Scanner\Reports**

#### <a name="use-powershell-with-a-disconnected-computer"></a>Utiliser PowerShell avec un ordinateur déconnecté

Procédez comme suit pour prendre en charge un ordinateur déconnecté à l’aide de PowerShell uniquement.

> [!IMPORTANT]
> Les administrateurs des [serveurs de scanneurs Azure China 21ViaNet](/microsoft-365/admin/services-in-china/parity-between-azure-information-protection#manage-azure-information-protection-content-scan-jobs) *doivent* suivre cette procédure afin de gérer leurs travaux d’analyse de contenu.
> 

**Gérer vos travaux d’analyse de contenu à l’aide de PowerShell uniquement**:

1. Configurez le scanneur pour qu’il fonctionne en mode **hors connexion** à l’aide de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) .

1. Créez un travail d’analyse de contenu à l’aide de l’applet de commande [Set-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob) , en veillant à utiliser le `-Enforce On` paramètre obligatoire.

1. Ajoutez vos référentiels à l’aide de l’applet de commande [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/add-aipscannerrepository) , avec le chemin d’accès au référentiel que vous souhaitez ajouter.

    > [!TIP]
    > Pour empêcher le dépôt d’hériter des paramètres de votre travail d’analyse de contenu, ajoutez le `OverrideContentScanJob On` paramètre, ainsi que les valeurs des paramètres supplémentaires.
    >
    > Pour modifier les détails d’un référentiel existant, utilisez la commande [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository) .
    >
 
1. Utilisez les applets de commande [AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob) et [obten-AIPScannerRepository](/powershell/module/azureinformationprotection/get-aipscannerrepository) pour retourner des informations sur les paramètres actuels de votre travail d’analyse de contenu. 

1. Utilisez la commande [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository) pour mettre à jour les détails d’un référentiel existant.

1. Exécutez votre travail d’analyse de contenu immédiatement si nécessaire, à l’aide de l’applet de commande [Start-AIPScan](/powershell/module/azureinformationprotection/start-aipscan) . 

    Les résultats des travaux d’analyse de contenu hors connexion se trouvent à l’emplacement suivant : **%LocalAppData%\Microsoft\MSIP\Scanner\Reports**

1. Si vous devez supprimer un référentiel ou un travail d’analyse de contenu entier, utilisez les applets de commande suivantes :

    - [Remove-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)
    - [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/remove-aipscannerrepository)

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restriction : vous ne pouvez pas obtenir le rôle Sysadmin ou les bases de données doivent être créées et configurées manuellement

Utilisez les procédures suivantes pour créer manuellement des bases de données et accorder le rôle **db_owner** , si nécessaire.

- [Procédure pour la base de données du scanneur](#manually-create-a-database-and-user-for-the-scanner-and-grant-db_owner-rights)
- [Procédure pour la base de données de découverte du réseau](#manually-create-a-database-and-user-for-the-network-discovery-service-and-grant-db_owner-rights)

Si le rôle sysadmin peut être accordé *temporairement* pour installer le scanneur, vous pouvez supprimer ce rôle une fois l’installation du scanneur terminée.

Effectuez l’une des opérations suivantes, selon les besoins de votre organisation :

|Restriction  |Description  |
|---------|---------|
|**Vous pouvez avoir le rôle sysadmin temporairement**     |  Si vous avez temporairement le rôle sysadmin, la base de données est automatiquement créée pour vous et le compte de service du scanneur reçoit automatiquement les autorisations requises. <br><br>Toutefois, le compte d’utilisateur qui configure le scanneur requiert toujours le rôle **db_owner** pour la base de données de configuration de l’analyseur. Si vous avez uniquement le rôle sysadmin jusqu’à ce que l’installation du scanneur soit terminée, accordez manuellement le rôle **db_owner** au compte d’utilisateur.       |
|**Vous ne pouvez pas avoir le rôle sysadmin**     |  Si vous ne pouvez pas recevoir le rôle sysadmin même temporairement, vous devez demander à un utilisateur disposant des droits d’administrateur système de créer manuellement une base de données avant d’installer le scanneur. <br><br>Pour cette configuration, le rôle de **db_owner** doit être affecté aux comptes suivants : <br>-Compte de service pour le scanneur<br>-Compte d’utilisateur pour l’installation du scanneur<br>-Compte d’utilisateur pour la configuration du scanneur <br><br>En règle générale, vous utilisez le même compte utilisateur pour installer et configurer le scanneur. Si vous utilisez des comptes différents, ils nécessitent tous deux le rôle **db_owner** pour la base de données de configuration de l’analyseur. Créez cet utilisateur et les droits nécessaires. Si vous spécifiez votre propre nom de cluster, la base de données de configuration est nommée **AIPScannerUL_<cluster_name>**.  |
| | |

De plus :

- Vous devez être un administrateur local sur le serveur qui exécutera le scanneur.
- Le compte de service qui exécutera le scanneur doit disposer des autorisations contrôle total sur les clés de Registre suivantes :

    - `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server`
    - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server`

Si, après avoir configuré ces autorisations, vous voyez une erreur lors de l’installation du scanneur, l’erreur peut être ignorée et vous pouvez démarrer manuellement le service du scanneur.

#### <a name="manually-create-a-database-and-user-for-the-scanner-and-grant-db_owner-rights"></a>Créez manuellement une base de données et un utilisateur pour le scanneur, et accordez des droits de db_owner

Si vous devez créer manuellement votre base de données de scanneur et/ou créer un utilisateur et accorder des droits de **db_owner** sur la base de données, demandez à votre administrateur système d’effectuer les étapes suivantes :

1. Créer une base de données pour le scanneur :

    ```sql
    **CREATE DATABASE AIPScannerUL_[clustername]**

    **ALTER DATABASE AIPScannerUL_[clustername] SET TRUSTWORTHY ON**
    ```

2. Accordez des droits à l’utilisateur qui exécute la commande d’installation et qui est utilisé pour exécuter des commandes de gestion du scanneur. Utilisez le script suivant :

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. Accordez des droits au compte de service du scanneur. Utilisez le script suivant :

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```

#### <a name="manually-create-a-database-and-user-for-the-network-discovery-service-and-grant-db_owner-rights"></a>Créez manuellement une base de données et un utilisateur pour le service de découverte du réseau et accordez des droits db_owner

Si vous avez besoin de créer manuellement votre base de données de [découverte du réseau](deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview) et/ou de créer un utilisateur et d’accorder des droits de **db_owner** sur la base de données, demandez à votre administrateur système d’effectuer les étapes suivantes :

1. Créer une base de données pour le service de découverte du réseau :

    ```sql
    **CREATE DATABASE AIPNetworkDiscovery_[clustername]**

    **ALTER DATABASE AIPNetworkDiscovery_[clustername] SET TRUSTWORTHY ON**
    ```

2. Accordez des droits à l’utilisateur qui exécute la commande d’installation et qui est utilisé pour exécuter des commandes de gestion du scanneur. Utilisez le script suivant :

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. Accordez des droits au compte de service du scanneur. Utilisez le script suivant :

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```
### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restriction : le compte de service pour le scanneur ne peut pas obtenir le droit **Ouvrir une session localement**

Si les stratégies de votre organisation n’interdisent pas le droit d' **ouverture de session en local** pour les comptes de service, utilisez le paramètre *OnBehalfOf* avec set-AIPAuthentication.

Pour plus d’informations, consultez [Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction : le compte de service du scanneur ne peut pas être synchronisé avec Azure Active Directory mais le serveur dispose d’une connexion Internet

Vous pouvez avoir un compte pour exécuter le service du scanneur et un autre compte pour l’authentification auprès d’Azure Active Directory :

- **Pour le compte de service du scanneur**, utilisez un compte Windows local ou un compte Active Directory.

- **Pour le compte Azure Active Directory**, spécifiez votre compte local pour le paramètre *OnBehalfOf* avec set-AIPAuthentication. Pour plus d’informations, consultez [Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

### <a name="restriction-your-labels-do-not-have-auto-labeling-conditions"></a>Restriction : vos étiquettes n’ont pas de conditions d’étiquetage automatique

Si vos étiquettes n’ont pas de conditions d’étiquetage automatique, envisagez d’utiliser l’une des options suivantes lors de la configuration de votre scanneur :

|Option  |Description  |
|---------|---------|
|**Découvrir tous les types d’informations**     |  Dans votre [travail d’analyse de contenu](deploy-aip-scanner-configure-install.md#create-a-content-scan-job), définissez l’option **types d’informations sur** **tous**. </br></br>Cette option définit le travail d’analyse de contenu pour analyser votre contenu pour tous les types d’informations sensibles.      |
|**Utiliser l’étiquetage recommandé**     |  Dans votre [travail d’analyse de contenu](deploy-aip-scanner-configure-install.md#create-a-content-scan-job), affectez la valeur **on** à l’option **considérer l’étiquetage recommandé comme automatique** .</br></br> Ce paramètre configure le scanneur pour appliquer automatiquement toutes les étiquettes recommandées sur votre contenu.      |
|**Définir une étiquette par défaut**     |   Définissez une étiquette par défaut dans votre [stratégie](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do), le [travail d’analyse de contenu](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)ou le [référentiel](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository). </br></br>Dans ce cas, le scanner applique l’étiquette par défaut sur tous les fichiers trouvés.       |
| | |

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez confirmé que votre système est conforme aux conditions préalables du scanneur, poursuivez [le déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner-configure-install.md).

Pour obtenir une vue d’ensemble du scanneur, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner.md).

**Plus d’informations**:

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md).