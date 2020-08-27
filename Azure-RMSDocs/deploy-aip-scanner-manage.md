---
title: Exécution de l’Azure Information Protection le scanner d’étiquetage unifié (AIP)
description: Instructions pour exécuter le Azure Information Protection scanner d’étiquetage unifié pour détecter, classer et protéger des fichiers sur des magasins de données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ad523eb3537c11ec2ca839b08da72d3275cfbef5
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953063"
---
# <a name="running-the-azure-information-protection-scanner"></a>Exécution de l’analyseur de Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows server 2012 R2*

>[!NOTE]
> Si vous utilisez le scanneur classique, consultez [installation et configuration du Azure information protection scanneur classique](deploy-aip-scanner-configure-install-classic.md).

Une fois que vous avez confirmé la [Configuration requise](deploy-aip-scanner-prereqs.md) et [configuré et installé votre scanneur](deploy-aip-scanner-configure-install.md), [exécutez une analyse de découverte](#run-a-discovery-cycle-and-view-reports-for-the-scanner) pour commencer.

Suivez les autres étapes décrites ci-dessous pour gérer vos analyses.

- [Arrêter une analyse](#stopping-a-scan)
- [Réanalyse des fichiers](#rescanning-files)
- [Résolution des problèmes d’analyse arrêtée](#troubleshooting-a-stopped-scan)
- [Résolution des problèmes à l’aide de l’outil de diagnostic du scanneur](#troubleshooting-using-the-scanner-diagnostic-tool)

Pour plus d’informations, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner.md).

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Exécuter un cycle de découverte et afficher les rapports pour le scanneur

Utilisez la procédure suivante après avoir [configuré et installé votre scanneur](deploy-aip-scanner-configure-install.md) pour avoir une compréhension initiale de votre contenu.

Effectuez ces étapes autant de fois que nécessaire lorsque votre contenu change.

1. Dans le Portail Azure, dans le volet **Azure information protection de travaux d’analyse de contenu** , sélectionnez vos travaux d’analyse de contenu, puis sélectionnez l’option **Analyser maintenant** :

    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

    Dans votre session PowerShell, vous pouvez également exécuter la commande suivante :

    ```ps
    Start-AIPScan
    ```

1. Attendez que le scanneur termine son cycle. L’analyse se termine lorsque le scanneur a analysé tous les fichiers des magasins de données spécifiés.

    Pour surveiller la progression du scanneur, effectuez l’une des opérations suivantes :

    - **Actualisez les travaux d’analyse.**  Dans le volet **Azure information protection-travaux d’analyse de contenu** , sélectionnez **Actualiser**.

        Patientez jusqu’à ce que les valeurs de la colonne des résultats de la **dernière** analyse et de la **dernière analyse (heure de fin)** s’affichent.

    - **Utilisez une commande PowerShell.** Exécutez `Get-AIPScannerStatus` pour surveiller la modification de l’État.

1. Une fois l’analyse terminée, examinez les rapports stockés dans le répertoire ** % *LocalAppData*% \ Microsoft\MSIP\Scanner\Reports** .

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

- **Exécutez une commande PowerShell.** Exécutez la commande suivante :

    ```ps
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>Réanalyse des fichiers

Pour le [premier cycle d’analyse](#run-a-discovery-cycle-and-view-reports-for-the-scanner), le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, seuls les fichiers nouveaux ou modifiés sont inspectés.

L’inspection de nouveau de tous les fichiers est généralement utile lorsque vous souhaitez que les rapports incluent tous les fichiers, lorsque vous avez des modifications que vous souhaitez appliquer à tous les fichiers et lorsque le scanneur s’exécute en mode découverte.

**Pour exécuter manuellement une nouvelle analyse complète :**

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
> Si vous avez effectué une mise à niveau vers la version [2.8.83](rms-client/unifiedlabelingclient-version-release-history.md#version-2883-public-preview) ou ultérieure, AIP ignore la rerecherche complète des paramètres mis à jour pour garantir des performances cohérentes. Si vous avez effectué une mise à niveau, veillez à [exécuter une nouvelle analyse complète manuellement](#rescanning-files) en fonction des besoins. 
>
> Par exemple, si vous avez modifié les paramètres de **mise en application des stratégies** de **appliquer = désactivé** à **appliquer = on,** veillez à exécuter une nouvelle analyse complète pour appliquer vos étiquettes à votre contenu.
> 

## <a name="troubleshooting-a-stopped-scan"></a>Résolution des problèmes d’analyse arrêtée

Si le scanneur s’arrête de manière inattendue et ne termine pas l’analyse d’un grand nombre de fichiers dans un référentiel, vous devrez peut-être modifier l’un des paramètres suivants :

- **Nombre de ports dynamiques**. Vous devrez peut-être augmenter le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers. Le renforcement du serveur pour SharePoint peut être l’une des raisons expliquant pourquoi le scanneur dépasse le nombre de connexions réseau autorisées et s’arrête.

    Pour vérifier s’il s’agit de la cause de l’arrêt du scanneur, regardez si le message d’erreur suivant est consigné pour le scanneur dans le fichier ** % *LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog** .

    **Impossible de se connecter au serveur distant---> System .net. Sockets. SocketException : une seule utilisation de chaque adresse de socket (protocole/adresse réseau/port) est normalement autorisée sur IP : port**

    > [!NOTE]
    > Ce fichier sera compressé s’il existe plusieurs journaux.

    Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).

- **Seuil du mode liste.** Pour les batteries de serveurs SharePoint de grande taille, vous devrez peut-être augmenter le seuil d’affichage de liste. Par défaut, le seuil d’affichage de liste est défini sur 5 000.

    Pour plus d’informations, consultez [gérer des listes et des bibliothèques de grande taille dans SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>Résolution des problèmes à l’aide de l’outil de diagnostic du scanneur

Si vous rencontrez des problèmes avec Azure information scanner, vérifiez que votre déploiement est sain à l’aide de la commande PowerShell suivante :

```ps
Start-AIPScannerDiagnostics
```

L’outil de diagnostic vérifie les détails suivants, puis exporte un fichier journal avec les résultats :

- Si la base de données est à jour
- Si les URL réseau sont accessibles
- Indique s’il existe un jeton d’authentification valide et si la stratégie peut être acquise
- Si le profil est défini dans le Portail Azure
- Indique si la configuration en ligne/hors connexion existe et peut être acquise
- Indique si les règles configurées sont valides

> [!TIP]
> Si vous exécutez la commande sous un utilisateur qui n’est pas l’utilisateur du scanneur, veillez à ajouter le paramètre **-OnBehalf** . 
>

> [!NOTE]
> L’outil **Start-AIPScannerDiagnostics** n’exécute pas une vérification de la configuration requise complète. Si vous rencontrez des problèmes avec le scanneur, vérifiez également que votre système est conforme aux [exigences du scanneur](deploy-aip-scanner-prereqs.md)et que la [configuration et l’installation de votre scanneur](deploy-aip-scanner-configure-install.md) sont terminées.
>

## <a name="next-steps"></a>Étapes suivantes

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur ce scénario et d’autres scénarios qui utilisent PowerShell, consultez [utilisation de PowerShell avec le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-powershell.md).
