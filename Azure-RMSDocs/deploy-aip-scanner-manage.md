---
title: Exécution de l’Azure Information Protection le scanner d’étiquetage unifié (AIP)
description: Instructions pour exécuter le Azure Information Protection scanner d’étiquetage unifié pour détecter, classer et protéger des fichiers sur des magasins de données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/01/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 13484ad0301ec8d7404c4127ff78720df81d8eb5
ms.sourcegitcommit: caf2978ab03e4893b59175ce753791867793dcfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2021
ms.locfileid: "100524776"
---
# <a name="running-the-azure-information-protection-scanner"></a>Exécution du scanneur Azure Information Protection

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le scanneur classique, consultez [exécution du scanneur classique Azure information protection](deploy-aip-scanner-manage-classic.md). *

Une fois que vous avez confirmé la [Configuration requise](deploy-aip-scanner-prereqs.md) et [configuré et installé votre scanneur](deploy-aip-scanner-configure-install.md), [exécutez une analyse de découverte](#run-a-discovery-cycle-and-view-reports-for-the-scanner) pour commencer.

Suivez les autres étapes décrites ci-dessous pour gérer vos analyses.

- [Arrêter une analyse](#stopping-a-scan)
- [Réanalyse des fichiers](#rescanning-files)

Pour plus d’informations, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner.md).

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Exécuter un cycle de découverte et afficher les rapports pour le scanneur

Utilisez la procédure suivante après avoir [configuré et installé votre scanneur](deploy-aip-scanner-configure-install.md) pour avoir une compréhension initiale de votre contenu.

Effectuez ces étapes autant de fois que nécessaire lorsque votre contenu change.

1. Dans le Portail Azure, dans le volet **Azure information protection de travaux d’analyse de contenu** , sélectionnez vos travaux d’analyse de contenu, puis sélectionnez l’option **Analyser maintenant** :

    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

    Dans votre session PowerShell, vous pouvez également exécuter la commande suivante :

    ```PowerShell
    Start-AIPScan
    ```

1. Attendez que le scanneur termine son cycle. L’analyse se termine lorsque le scanneur a analysé tous les fichiers des magasins de données spécifiés.

    Pour surveiller la progression du scanneur, effectuez l’une des opérations suivantes :

    - **Actualisez les travaux d’analyse.**  Dans le volet **Azure information protection-travaux d’analyse de contenu** , sélectionnez **Actualiser**.

        Patientez jusqu’à ce que les valeurs de la colonne des résultats de la **dernière** analyse et de la **dernière analyse (heure de fin)** s’affichent.

    - **Utilisez une commande PowerShell.** Exécutez `Get-AIPScannerStatus` pour surveiller la modification de l’État.

1. Une fois l’analyse terminée, examinez les rapports stockés dans le répertoire **% *LocalAppData*% \ Microsoft\MSIP\Scanner\Reports** .

    - Les fichiers de résumé .txt incluent la durée de l’analyse, le nombre de fichiers analysés et le nombre de fichiers correspondants aux types d’informations.

    - Les fichiers .csv offrent plus de détails pour chaque fichier. Ce dossier stocke jusqu’à 60 rapports pour chaque cycle d’analyse et tous, sauf le dernier rapport, sont compressés afin de réduire l’espace disque requis.

Les [configurations initiales](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal) vous indiquent de définir les **types d’informations à découvrir** pour la **stratégie uniquement**. Cette configuration signifie que seuls les fichiers qui remplissent les conditions que vous avez configurées pour la classification automatique sont inclus dans les rapports détaillés.

Si aucune étiquette n’est appliquée, vérifiez que la configuration de votre étiquette comprend la classification automatique plutôt que recommandée, ou activez l' **étiquetage recommandé sur automatique** (disponible dans le scanneur version 2.7. x. x et versions ultérieures).

Si les résultats ne sont pas toujours les mêmes que prévu, vous devrez peut-être reconfigurer les conditions que vous avez spécifiées pour vos étiquettes. Si c’est le cas, reconfigurez les conditions en fonction des besoins, puis répétez cette procédure jusqu’à ce que vous soyez satisfait des résultats. Ensuite, mettez à jour votre configuration automatiquement et éventuellement la protection.

### <a name="viewing-updates-in-the-azure-portal"></a>Affichage des mises à jour dans le Portail Azure

Les scanneurs envoient ces informations à Azure Information Protection toutes les cinq minutes, afin que vous puissiez afficher les résultats en temps quasi réel à partir du Portail Azure. Pour plus d’informations, consultez [Création de rapports pour Azure Information Protection](reports-aip.md).

Le portail Azure affiche des informations portant uniquement sur la dernière analyse. Si vous devez consulter les résultats des analyses précédentes, accédez aux rapports qui sont stockés sur l’ordinateur du scanneur, dans le dossier %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

### <a name="changing-log-levels-or-locations"></a>Modification des emplacements ou des niveaux de journal

Modifiez le niveau de journalisation à l’aide du paramètre *ReportLevel* avec [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration).

L’emplacement ou le nom du dossier de rapport ne peut pas être modifié. Si vous souhaitez stocker des rapports dans un autre emplacement, envisagez d’utiliser une jonction de répertoire pour le dossier.

Par exemple, utilisez la commande [MKLINK](/windows-server/administration/windows-commands/mklink) : `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

Si vous avez effectué ces étapes après une configuration et une installation initiales, poursuivez [la configuration du scanneur pour appliquer la classification et la protection](deploy-aip-scanner-configure-install.md#configure-the-scanner-to-apply-classification-and-protection).

## <a name="stopping-a-scan"></a>Arrêt d’une analyse

Pour arrêter une analyse en cours d’exécution avant qu’elle ne soit terminée, utilisez l’une des méthodes suivantes :

- **Portail Azure.** Sélectionnez **arrêter l’analyse**:

    ![Arrêter une analyse pour le scanneur de Azure Information Protection](./media/scanner-stop-scan.png)

- **Exécutez une commande PowerShell.** Exécutez la commande suivante :

    ```PowerShell
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>Réanalyse des fichiers

Pour le [premier cycle d’analyse](#run-a-discovery-cycle-and-view-reports-for-the-scanner), le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, seuls les fichiers nouveaux ou modifiés sont inspectés.

L’inspection de nouveau de tous les fichiers est généralement utile lorsque vous souhaitez que les rapports incluent tous les fichiers, lorsque vous avez des modifications que vous souhaitez appliquer à tous les fichiers et lorsque le scanneur s’exécute en mode découverte.

**Pour exécuter manuellement une nouvelle analyse complète**:

1. Accédez au volet **travaux d’analyse de contenu Azure information protection** dans le portail Azure.

1. Sélectionnez votre travail d’analyse de contenu dans la liste, puis sélectionnez l’option **relancer l’analyse de tous les fichiers** :

    ![Relancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-rescan-files.png)

Lorsqu’une analyse complète est terminée, le type d’analyse passe automatiquement à incrémentiel afin que, pour les analyses suivantes, seuls les fichiers nouveaux ou modifiés soient à nouveau analysés.

> [!TIP]
> Si vous avez apporté des modifications à votre [travail d’analyse de contenu](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)AIP, le portail Azure vous invite à ignorer une nouvelle analyse complète. Pour vous assurer que votre nouvelle analyse se produit, veillez à sélectionner **non** dans l’invite qui s’affiche.
> 
### <a name="trigger-a-full-rescan-by-modifying-your-settings-versions-271010-and-lower"></a>Déclencher une nouvelle analyse complète en modifiant vos paramètres (versions 2.7.101.0 et antérieures)

Dans versions du scanneur [2.7.101.0](rms-client/unifiedlabelingclient-version-release-history.md#version-271010) et versions antérieures, tous les fichiers sont analysés chaque fois que l’analyseur détecte des paramètres nouveaux ou modifiés pour l’étiquetage automatique et recommandé. Le scanneur actualise automatiquement la stratégie toutes les quatre heures.

Pour actualiser la stratégie plus tôt, par exemple pendant le test, supprimez manuellement le contenu du répertoire **%LocalAppData%\Microsoft\MSIP\mip \<processname> \mip** et redémarrez le service Azure information protection.

Si vous avez également modifié les paramètres de protection de vos étiquettes, patientez 15 minutes après l’enregistrement des paramètres de protection mis à jour avant le redémarrage du service Azure Information Protection.

> [!IMPORTANT]
> Si vous avez effectué une mise à niveau vers la version [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) ou ultérieure, AIP ignore la rerecherche complète des paramètres mis à jour pour garantir des performances cohérentes. Si vous avez effectué une mise à niveau, veillez à [exécuter une nouvelle analyse complète manuellement](#rescanning-files) en fonction des besoins. 
>
> Par exemple, si vous avez modifié les paramètres de **stratégie de sensibilité** de **appliquer = désactivé** à **appliquer = on**, veillez à exécuter une nouvelle analyse complète pour appliquer vos étiquettes à votre contenu.
> 

## <a name="next-steps"></a>Étapes suivantes

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md).