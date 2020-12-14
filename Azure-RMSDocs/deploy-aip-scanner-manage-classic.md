---
title: Exécution du scanner Azure Information Protection Classic (AIP)
description: Instructions pour exécuter le Azure Information Protection scanneur classique pour détecter, classer et protéger des fichiers sur des magasins de données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d8ea8fdccbfc92e954ba1c2f656b498fc0f8f4ee
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382783"
---
# <a name="running-the-azure-information-protection-classic-scanner"></a>Exécution du scanneur classique Azure Information Protection

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [exécution de l’analyseur de Azure information protection](deploy-aip-scanner-manage.md)*.

> [!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Une fois que vous avez confirmé la [Configuration requise](deploy-aip-scanner-prereqs-classic.md) et [configuré et installé votre scanneur](deploy-aip-scanner-configure-install-classic.md), [exécutez une analyse de découverte](#run-a-discovery-cycle-and-view-reports-for-the-scanner) pour commencer.

Suivez les autres étapes décrites ci-dessous pour gérer vos analyses.

- [Arrêter une analyse](#stopping-a-scan)
- [Réanalyse des fichiers](#rescanning-files)
- [Résolution des problèmes d’analyse arrêtée](#troubleshooting-a-stopped-scan)
- [Résolution des problèmes à l’aide de l’outil de diagnostic du scanneur](#troubleshooting-using-the-scanner-diagnostic-tool)
- [ID et descriptions des journaux des événements du scanneur](#event-log-ids-and-descriptions-for-the-scanner)

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

    - **Vérifiez les journaux des événements Windows.** Vérifiez le journal des événements **des applications et services** Windows local, nommé **Azure information protection**.

        Ce journal signale également le moment où le scanneur a terminé l’analyse, y compris un résumé des résultats. Recherchez l’ID d’événement d’information **911**. Pour plus d’informations, consultez [ID et descriptions du journal des événements pour le scanneur](#event-log-ids-and-descriptions-for-the-scanner).

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
    
    ```ps
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>Réanalyse des fichiers

Pour le [premier cycle d’analyse](#run-a-discovery-cycle-and-view-reports-for-the-scanner), le scanneur inspecte tous les fichiers des magasins de données configurés. Pour les analyses suivantes, seuls les fichiers nouveaux ou modifiés sont inspectés.

L’inspection de nouveau de tous les fichiers est généralement utile lorsque vous souhaitez que les rapports incluent tous les fichiers et lorsque le scanneur s’exécute en mode détection.

Exécutez une nouvelle analyse de tous vos fichiers à l’aide de l’une des méthodes suivantes :

- [Exécuter manuellement une nouvelle analyse complète](#manually-run-a-full-rescan)
- [Déclencher une nouvelle analyse complète en actualisant la stratégie](#trigger-a-full-rescan-by-refreshing-the-policy)

### <a name="manually-run-a-full-rescan"></a>Exécuter manuellement une nouvelle analyse complète

Forcez le scanneur à inspecter à nouveau tous les fichiers, si nécessaire, à partir du volet **travaux d’analyse de contenu Azure information protection** de la portail Azure.

Sélectionnez votre travail d’analyse de contenu dans la liste, puis sélectionnez l’option **relancer l’analyse de tous les fichiers** :

![Relancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-rescan-files.png)

Lorsqu’une analyse complète est terminée, le type d’analyse passe automatiquement à incrémentiel afin que, pour les analyses suivantes, seuls les fichiers nouveaux ou modifiés soient à nouveau analysés.

### <a name="trigger-a-full-rescan-by-refreshing-the-policy"></a>Déclencher une nouvelle analyse complète en actualisant la stratégie

Tous les fichiers sont également inspectés dans les scénarios suivants chaque fois que le scanneur télécharge une stratégie de Azure Information Protection qui a des conditions nouvelles ou modifiées.

Le scanneur actualise automatiquement la stratégie toutes les heures, ainsi que chaque fois que le service démarre et que la stratégie se trouve à plus d’une heure.

Pour actualiser la stratégie plus tôt, par exemple pendant le test, supprimez manuellement le fichier de stratégie **Policy.msip**  du répertoire **%LocalAppData%\Microsoft\MSIP** et redémarrez le service Azure information protection.

> [!NOTE]
> Si vous avez également modifié les paramètres de protection de vos étiquettes, patientez 15 minutes après l’enregistrement des paramètres de protection mis à jour avant le redémarrage du service Azure Information Protection.
>

## <a name="troubleshooting-a-stopped-scan"></a>Résolution des problèmes d’analyse arrêtée

Si le scanneur s’arrête de manière inattendue et ne termine pas l’analyse d’un grand nombre de fichiers dans un référentiel, vous devrez peut-être modifier l’un des paramètres suivants :

- **Nombre de ports dynamiques**. Vous devrez peut-être augmenter le nombre de ports dynamiques pour le système d’exploitation hébergeant les fichiers. Le renforcement du serveur pour SharePoint peut être l’une des raisons expliquant pourquoi le scanneur dépasse le nombre de connexions réseau autorisées et s’arrête.

    Pour vérifier s’il s’agit de la cause de l’arrêt du scanneur, regardez si le message d’erreur suivant est consigné pour le scanneur dans le fichier **% *LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog** .

    **Impossible de se connecter au serveur distant---> System .net. Sockets. SocketException : une seule utilisation de chaque adresse de socket (protocole/adresse réseau/port) est normalement autorisée sur IP : port**

    > [!NOTE]
    > Ce fichier sera compressé s’il existe plusieurs journaux.

    Pour plus d’informations sur l’affichage de la plage de ports actuelle et l’augmentation de la plage, consultez [Paramètres modifiables pour améliorer les performances du réseau](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).

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

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>ID du journal des événements et descriptions pour le scanneur

Les événements de journalisation du scanneur AIP suivants sont stockés dans le journal des événements **applications et services** Windows nommé **Azure information protection**.

|ID de l’événement  |Activité  |Description  |
|---------|---------|---------|
|**910**     | Cycle du scanneur démarré        | Consigné lorsque le service du scanneur est démarré et commence à rechercher les fichiers dans les référentiels de données que vous avez spécifiés.        |
|**911**     |   Cycle du scanneur terminé      | Consigné lorsque le scanneur a terminé une analyse manuelle ou que le scanneur a terminé un cycle pour une planification continue.       |
| | | |

> [!TIP]
> Si le scanneur a été configuré pour s’exécuter manuellement plutôt que en continu, pour analyser de nouveau les fichiers, définissez la **planification** sur **Manuel** ou **toujours** dans le travail d’analyse du contenu, puis redémarrez le service. Pour plus d’informations, consultez [rescaning Files](#rescanning-files).
>

## <a name="next-steps"></a>Étapes suivantes

- Comment l’équipe Core Services Engineering and Operations de Microsoft a-t-elle implémenté ce scanneur ?  Lisez l’étude de cas technique : [Automatiser la protection des données avec le scanneur Azure Information Protection](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner).

- Vous vous posez peut-être [la différence entre Windows Server FCI et le scanneur Azure information protection ?](faqs-classic.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- Vous pouvez également utiliser PowerShell pour classifier et protéger des fichiers de manière interactive à partir de votre ordinateur de bureau. Pour plus d’informations sur tous les scénarios qui utilisent PowerShell, consultez [Utiliser PowerShell avec le client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).