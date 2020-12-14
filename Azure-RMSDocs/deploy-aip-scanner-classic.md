---
title: Comprendre le Azure Information Protection scanneur classique-AIP
description: Instructions d’installation, de configuration et d’exécution du Azure Information Protection scanneur classique pour détecter, classer et protéger des fichiers sur des magasins de données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 77d7ddb996a224e871a89227bd58872989bdc759
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382851"
---
# <a name="what-is-the-azure-information-protection-classic-scanner"></a>Qu’est-ce que le scanneur classique Azure Information Protection ?

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [qu’est-ce que le scanneur d’étiquetage unifié Azure information protection ?](deploy-aip-scanner.md). *

> [!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Utilisez les informations de cette section pour en savoir plus sur le Azure Information Protection scanneur client classique, puis sur la façon d’installer, de configurer, d’exécuter et, le cas échéant, de le résoudre.

Le scanneur AIP s’exécute en tant que service sur Windows Server et vous permet de découvrir, classifier et protéger des fichiers sur les banques de données suivantes :

- **Chemins UNC** pour les partages réseau qui utilisent le protocole SMB (Server Message Block).

- **Bibliothèques de documents SharePoint et dossier** pour sharepoint server 2019 via sharepoint server 2013. 

> [!NOTE]
> Pour analyser et étiqueter des fichiers sur des référentiels cloud, utilisez [Cloud App Security](/cloud-app-security/) au lieu du scanneur.
>
## <a name="azure-information-protection-classic-scanner-overview"></a>Présentation du scanneur classique Azure Information Protection

Le scanneur AIP peut inspecter les fichiers que Windows peut indexer. Si vous avez configuré des étiquettes qui appliquent une classification automatique, le scanneur peut étiqueter les fichiers détectés pour appliquer cette classification et éventuellement appliquer ou supprimer la protection.

L’illustration suivante montre l’architecture du scanneur AIP, où le scanneur Découvre des fichiers sur vos serveurs locaux et SharePoint.

:::image type="content" source="media/classic-scanner-arch.png" alt-text="Architecture du scanneur Azure Information Protection Classic":::

Pour inspecter vos fichiers, le scanneur utilise les IFilters installés sur l’ordinateur. Pour déterminer si les fichiers doivent être étiquetés, le scanneur utilise Microsoft 365 les types d’informations de confidentialité intégrés de protection contre la perte de données (DLP) et la détection de modèle, ou Microsoft 365 des modèles Regex.

Le scanneur utilise le client Azure Information Protection et peut classer et protéger les mêmes types de fichiers que le client. Pour plus d’informations, consultez [types de fichiers pris en charge par le client Azure information protection](./rms-client/client-admin-guide-file-types.md).

Effectuez l’une des opérations suivantes pour configurer vos analyses en fonction des besoins :

- **Exécutez le scanneur en mode détection uniquement** pour créer des rapports qui vérifient ce qui se produit lorsque vos fichiers sont étiquetés.
- **Exécutez le scanneur pour détecter les fichiers contenant des informations sensibles**, sans configurer les étiquettes qui appliquent la classification automatique.
- **Exécutez le scanner automatiquement** pour appliquer les étiquettes configurées.
- **Définissez une liste de types de fichiers** pour spécifier des fichiers à analyser ou à exclure.

> [!NOTE]
> Le scanneur ne découvre pas et n’étiquette pas en temps réel. Il analyse systématiquement les fichiers des magasins de données que vous spécifiez. Configurez ce cycle pour qu’il s’exécute une seule fois, ou à plusieurs reprises.

## <a name="aip-scanning-process"></a>Processus d’analyse AIP

Lors de l’analyse des fichiers, le scanneur AIP exécute les étapes suivantes :

[1. déterminer si les fichiers sont inclus ou exclus pour l’analyse](#1-determine-whether-files-are-included-or-excluded-for-scanning)

[2. Inspectez et étiquetez les fichiers](#2-inspect-and-label-files)

[3. étiquetez les fichiers qui ne peuvent pas être inspectés](#3-label-files-that-cant-be-inspected)

> [!NOTE]
> Pour plus d’informations, consultez [fichiers non marqués par le scanneur](#files-not-labeled-by-the-scanner).

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. déterminer si les fichiers sont inclus ou exclus pour l’analyse

Le scanneur ignore automatiquement les fichiers qui sont exclus de la classification et de la protection, comme les fichiers exécutables et les fichiers système. Pour plus d’informations, consultez [types de fichiers exclus de la classification et](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)de la protection.

Le scanneur prend également en compte toutes les listes de fichiers explicitement définies pour analyser ou exclure de l’analyse. Les listes de fichiers s’appliquent à tous les référentiels de données par défaut et peuvent également être définies pour des référentiels spécifiques.

Pour définir des listes de fichiers à des fins d’analyse ou d’exclusion, utilisez le paramètre **types de fichiers à analyser** du travail d’analyse du contenu. Par exemple :

![Configurer les types de fichiers à analyser pour le scanneur Azure Information Protection](./media/scanner-file-types.png)

Pour plus d’informations, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner-configure-install.md).

### <a name="2-inspect-and-label-files"></a>2. Inspectez et étiquetez les fichiers

Après avoir identifié les fichiers exclus, le scanneur filtre à nouveau pour identifier les fichiers pris en charge pour l’inspection.

Ces filtres supplémentaires sont les mêmes que ceux utilisés par le système d’exploitation pour la recherche et l’indexation Windows et ne nécessitent aucune configuration supplémentaire. Windows IFilter est également utilisé pour analyser les types de fichiers utilisés par Word, Excel et PowerPoint, ainsi que pour les documents PDF et les fichiers texte.

Pour obtenir la liste complète des types de fichiers pris en charge pour l’inspection, ainsi que des instructions supplémentaires pour la configuration des filtres pour inclure des fichiers. zip et. TIFF, consultez [types de fichiers pris en charge pour l’inspection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection).

Après l’inspection, les types de fichiers pris en charge sont étiquetés à l’aide des conditions spécifiées pour vos étiquettes. Si vous utilisez le mode détection, ces fichiers peuvent être consignés pour contenir les conditions spécifiées pour vos étiquettes, ou être signalés comme contenant des types d’informations sensibles connus.

### <a name="3-label-files-that-cant-be-inspected"></a>3. étiquetez les fichiers qui ne peuvent pas être inspectés

Pour tous les types de fichiers qui ne peuvent pas être inspectés, le scanneur AIP applique l’étiquette par défaut dans la stratégie de Azure Information Protection ou l’étiquette par défaut configurée pour le scanneur.

### <a name="files-not-labeled-by-the-scanner"></a>Fichiers non marqués par le scanneur

Le scanneur AIP ne peut pas étiqueter les fichiers dans les circonstances suivantes :

- Lorsque l’étiquette applique la classification, mais pas la protection, et que le type de fichier ne prend pas en charge la classification uniquement par le client. Pour plus d’informations, consultez [types de fichiers client classiques](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

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

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs-classic.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur tous les scénarios qui utilisent PowerShell, consultez [Utiliser PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).