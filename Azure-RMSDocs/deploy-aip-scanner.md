---
title: Fonctionnement du scanneur d’étiquetage unifié Azure Information Protection-AIP
description: Instructions d’installation, de configuration et d’exécution de la version actuelle de l’Azure Information Protection scanneur d’étiquetage unifié pour détecter, classer et protéger des fichiers dans des banques de données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 24429f7727800650e5ce8f5f814597dfd83de0b2
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414988"
---
# <a name="what-is-the-azure-information-protection-unified-labeling-scanner"></a>Qu’est-ce que le scanneur d’étiquetage unifié Azure Information Protection ?

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez [qu’est-ce que le Azure information protection scanneur classique ?](deploy-aip-scanner-classic.md)*

>[!NOTE] 
> Pour analyser et étiqueter des fichiers sur des référentiels cloud, utilisez [Cloud App Security](/cloud-app-security/) au lieu du scanneur.

Utilisez les informations de cette section pour en savoir plus sur le Azure Information Protection scanneur d’étiquetage unifié, puis sur la façon d’installer, de configurer, d’exécuter et, le cas échéant, de le résoudre.

Le scanneur AIP s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les banques de données suivantes :

- **Chemins UNC** pour les partages réseau qui utilisent les protocoles SMB ou NFS (version préliminaire).

- **Bibliothèques de documents SharePoint et dossier** pour sharepoint server 2019 via sharepoint server 2013. SharePoint 2010 est également pris en charge pour les clients disposant de la [prise en charge étendue de cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Pour classifier et protéger vos fichiers, le scanneur utilise des [étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) configurées dans l’un des Microsoft 365 les centres d’administration d’étiquetage, y compris les Microsoft 365 Security Center, le centre de conformité Microsoft 365, ainsi que le centre de conformité et de sécurité Microsoft 365. 

## <a name="azure-information-protection-unified-labeling-scanner-overview"></a>Vue d’ensemble du scanner d’étiquetage unifié Azure Information Protection

Le scanneur AIP peut inspecter les fichiers que Windows peut indexer. Si vous avez configuré des étiquettes de sensibilité pour appliquer la classification automatique, le scanneur peut étiqueter les fichiers détectés pour appliquer cette classification et éventuellement appliquer ou supprimer la protection. 

L’illustration suivante montre l’architecture du scanneur AIP, où le scanneur Découvre des fichiers sur vos serveurs locaux et SharePoint.

:::image type="content" source="media/ul-scanner-arch.png" alt-text="Architecture du scanneur d’étiquetage unifiée Azure Information Protection":::

Pour inspecter vos fichiers, le scanneur utilise les IFilters installés sur l’ordinateur. Pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise Microsoft 365 les types d’informations de confidentialité intégrés de protection contre la perte de données (DLP) et la détection de modèle, ou Microsoft 365 des modèles Regex.

Le scanneur utilise le client Azure Information Protection et peut classer et protéger les mêmes types de fichiers que le client. Pour plus d’informations, consultez [types de fichiers pris en charge par le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-file-types.md).

Effectuez l’une des opérations suivantes pour configurer vos analyses en fonction des besoins :

- **Exécutez le scanneur en mode détection uniquement** pour créer des rapports qui vérifient ce qui se produit lorsque vos fichiers sont étiquetés.
- **Exécutez le scanneur pour détecter les fichiers contenant des informations sensibles**, sans configurer les étiquettes qui appliquent la classification automatique.
- **Exécutez le scanner automatiquement** pour appliquer les étiquettes configurées. 
- **Définissez une liste de types de fichiers** pour spécifier des fichiers à analyser ou à exclure.

> [!NOTE]
> Le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers des magasins de données que vous spécifiez. Configurez ce cycle pour qu’il s’exécute une seule fois, ou à plusieurs reprises.

> [!TIP]
> Le scanner d’étiquetage unifié prend en charge les clusters de scanneurs avec plusieurs nœuds, ce qui permet à votre organisation de monter en charge, ce qui permet des temps d’analyse plus rapides et une portée plus large. 
> 
> Déployez plusieurs nœuds directement à partir du début, ou démarrez avec un cluster à nœud unique et ajoutez des nœuds supplémentaires plus tard au fur et à mesure que vous augmentez. Déployez plusieurs nœuds en utilisant les mêmes nom de cluster et base de données pour l’applet de commande **install-AIPScanner** .
> 

## <a name="aip-scanning-process"></a>Processus d’analyse AIP

Lors de l’analyse des fichiers, le scanneur AIP exécute les étapes suivantes :

[1. déterminer si les fichiers sont inclus ou exclus pour l’analyse](#1-determine-whether-files-are-included-or-excluded-for-scanning)

[2. Inspectez et étiquetez les fichiers](#2-inspect-and-label-files)

[3. étiquetez les fichiers qui ne peuvent pas être inspectés](#3-label-files-that-cant-be-inspected) 

Pour plus d’informations, consultez [fichiers non marqués par le scanneur](#files-not-labeled-by-the-scanner).

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. déterminer si les fichiers sont inclus ou exclus pour l’analyse 

Le scanneur ignore automatiquement les fichiers qui sont exclus de la classification et de la protection, comme les fichiers exécutables et les fichiers système. Pour plus d’informations, consultez [types de fichiers exclus de la classification et de la protection](rms-client/clientv2-admin-guide-file-types.md#file-types-excluded-from-classification-and-protection).

Le scanneur prend également en compte toutes les listes de fichiers explicitement définies pour analyser ou exclure de l’analyse. Les listes de fichiers s’appliquent à tous les référentiels de données par défaut et peuvent également être définies pour des référentiels spécifiques.

Pour définir des listes de fichiers à des fins d’analyse ou d’exclusion, utilisez le paramètre **types de fichiers à analyser** du travail d’analyse du contenu. Par exemple :

![Configurer les types de fichiers à analyser pour le scanneur Azure Information Protection](./media/scanner-file-types.png)

Pour plus d’informations, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner-configure-install.md).

### <a name="2-inspect-and-label-files"></a>2. Inspectez et étiquetez les fichiers

Après avoir identifié les fichiers exclus, le scanneur filtre à nouveau pour identifier les fichiers pris en charge pour l’inspection.

Ces filtres sont les mêmes que ceux utilisés par le système d’exploitation pour la recherche et l’indexation Windows et ne nécessitent aucune configuration supplémentaire. Windows IFilter est également utilisé pour analyser les types de fichiers utilisés par Word, Excel et PowerPoint, ainsi que pour les documents PDF et les fichiers texte.

Pour obtenir la liste complète des types de fichiers pris en charge pour l’inspection, ainsi que d’autres instructions pour la configuration des filtres pour inclure des fichiers. zip et. TIFF, consultez [types de fichiers pris en charge pour l’inspection](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection).

Après l’inspection, les types de fichiers pris en charge sont étiquetés à l’aide des conditions spécifiées pour vos étiquettes. Si vous utilisez le mode détection, ces fichiers peuvent être consignés pour contenir les conditions spécifiées pour vos étiquettes, ou être signalés comme contenant des types d’informations sensibles connus.

#### <a name="stopped-scanner-processes"></a>Processus de scanneur arrêtés

Si le scanneur s’arrête et ne termine pas une analyse pour un grand nombre de fichiers dans votre référentiel, vous devrez peut-être augmenter le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers.

Par exemple, le renforcement de serveur pour SharePoint est une des raisons pour lesquelles le scanneur dépasserait le nombre de connexions réseau autorisées et, par conséquent, s’arrêter.

Pour vérifier si le renforcement de serveur pour SharePoint est la cause de l’arrêt du scanneur, recherchez le message d’erreur suivant dans les journaux du scanneur sur **%LocalAppData%\Microsoft\MSIP\Logs\MSIPScanner.Iplog** (plusieurs journaux sont compressés dans un fichier zip) :

`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`

Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmenter si nécessaire, consultez [paramètres pouvant être modifiés pour améliorer les performances du réseau](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).

> [!TIP]
> Pour les batteries de serveurs SharePoint de grande taille, vous devrez peut-être augmenter le seuil d’affichage de liste, qui a une valeur par défaut de **5 000**.
>
> Pour plus d’informations, consultez [gérer les grandes listes et les bibliothèques dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).
>

### <a name="3-label-files-that-cant-be-inspected"></a>3. étiquetez les fichiers qui ne peuvent pas être inspectés

Pour tous les types de fichiers qui ne peuvent pas être inspectés, le scanneur AIP applique l’étiquette par défaut dans la stratégie de Azure Information Protection ou l’étiquette par défaut configurée pour le scanneur.

### <a name="files-not-labeled-by-the-scanner"></a>Fichiers non marqués par le scanneur
Le scanneur AIP ne peut pas étiqueter les fichiers dans les circonstances suivantes :

- Lorsque l’étiquette applique la classification, mais pas la protection, et que le type de fichier ne prend pas en charge la classification uniquement par le client. Pour plus d’informations, consultez [types de fichiers du client d’étiquetage unifié](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Lorsque l’étiquette applique la classification et la protection, mais que le scanneur ne prend pas en charge le type de fichier.
  
    Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). 

    D’autres types de fichiers peuvent être ajoutés pour la protection lorsque vous [Modifiez les types de fichiers à protéger](deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect).

**Exemple**: après l’inspection des fichiers. txt, le scanneur ne peut pas appliquer une étiquette qui est configurée pour la classification uniquement, car le type de fichier. txt ne prend pas en charge la classification uniquement. 

Toutefois, si l’étiquette est configurée pour la classification et la protection et que le type de fichier. txt est inclus pour le scanneur à protéger, le scanneur peut étiqueter le fichier.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le déploiement du scanneur, consultez les articles suivants :

- [Conditions préalables au déploiement du scanneur AIP](deploy-aip-scanner-prereqs.md)
- [Configuration et installation du scanneur AIP](deploy-aip-scanner-configure-install.md)
- [Exécution d’analyses à l’aide du scanneur AIP](deploy-aip-scanner-manage.md)

**Plus d’informations**:

- [Regardez notre vidéo de déploiement !](https://techcommunity.microsoft.com/t5/microsoft-security-and/mip-scanner-deployment-watch-our-video/ba-p/2023277) Visionnez une démonstration pas à pas de l’installation et de la configuration du scanneur local avec étiquetage.

- Consultez notre blog sur les meilleures pratiques pour le scanneur d’étiquetage unifié : [meilleures pratiques pour le déploiement et l’utilisation du scanneur UL AIP](https://aka.ms/AIPScannerBestPractices)

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md).
