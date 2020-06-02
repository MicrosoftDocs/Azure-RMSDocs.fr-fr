---
title: Azure Information Protection l’historique des versions du client d’étiquetage unifié-version & la stratégie de support
description: Consultez les informations de version pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b1e91bcbfca3d4f925750fd8d1f135bd8f4ff2c4
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84250041"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l’historique des versions et la stratégie de support du client d’étiquetage unifié

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Vous pouvez télécharger le client d’étiquetage unifié Azure Information Protection à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).

Après un bref délai de quelques semaines, la dernière version de la disponibilité générale est également incluse dans le catalogue Microsoft Update avec le nom de produit **Microsoft Azure information protection**  >  **Microsoft Azure information protection client d’étiquetage unifié**et la classification des **mises à jour**. Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [mise à niveau et maintenance du client d’étiquetage unifié Azure information protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version de disponibilité générale de la Azure Information Protection client d’étiquetage unifiée est prise en charge pendant six mois après la publication de la version GA suivante. La documentation n’inclut pas d’informations sur les versions non pris en charge du client. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les versions préliminaires ne doivent pas être déployées auprès des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions de la disponibilité générale qui ne sont plus prises en charge :

|Version du client|Date de publication|
|--------------|-------------|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|

Le format de date utilisé sur cette page est *mois/jour/année*.


### <a name="release-information"></a>Informations de version

Utilisez les informations suivantes pour découvrir les nouveautés ou les modifications apportées à une version prise en charge de l’Azure Information Protection client d’étiquetage unifié pour Windows. La dernière version est répertoriée en première position. Le format de date utilisé sur cette page est *mois/jour/année*.

> [!NOTE]
> Les correctifs mineurs ne sont pas répertoriés. par conséquent, si vous rencontrez un problème avec le client d’étiquetage unifié, nous vous recommandons de vérifier s’il est corrigé avec la dernière version de la mise à la disposition générale. Si le problème persiste, vérifiez la version préliminaire actuelle (si disponible).
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

Ce client remplace le client Azure Information Protection (Classic). Pour comparer les fonctionnalités et les fonctionnalités avec le client Classic, consultez [comparer les clients d’étiquetage pour les ordinateurs Windows](use-client.md#compare-the-labeling-clients-for-windows-computers).

## <a name="version-27950-public-preview"></a>Version préliminaire publique de la version 2.7.95.0

Scanner d’étiquetage unifié et client (version préliminaire publique) version 2.7.95.0

**Publication** le 06/01/2020

**Nouvelles fonctionnalités pour le scanneur d’étiquetage unifié :**

- [Utilisez le scanneur pour appliquer des étiquettes en fonction des conditions recommandées](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#prerequisites-for-the-azure-information-protection-scanner). Les clients AIP peuvent désormais choisir d’implémenter l’étiquetage automatique côté service uniquement. Cette fonctionnalité permet aux utilisateurs d’AIP de toujours suivre les recommandations au lieu du scénario précédent, qui ne permettait que l’étiquetage automatique côté utilisateur.

- [Découvrez quels fichiers découverts précédemment par le moteur d’analyse ont été supprimés du référentiel analysé](https://docs.microsoft.com/azure/information-protection/reports-aip) Ces fichiers supprimés n’ont pas été précédemment signalés dans AIP Analytics et sont désormais disponibles dans le rapport de découverte du scanneur.

- [Recevez des rapports du scanner sur les échecs pour appliquer des événements d’action](https://docs.microsoft.com/azure/information-protection/reports-aip#friendly-schema-reference-for-event-functions). Utilisez les rapports pour en savoir plus sur les événements d’action ayant échoué et découvrir des moyens d’éviter les occurrences futures. 

- Présentation de l’outil d’analyse de diagnostics du scanneur AIP pour la détection et l’analyse des erreurs courantes du scanneur. Pour commencer à utiliser les diagnostics du scanneur AIP, [exécutez la nouvelle applet de commande **Start-AIPScannerDiagnostics** ](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#troubleshooting-using-scanner-diagnostic-tool). 

- Vous pouvez désormais gérer et limiter la consommation maximale de l’UC sur l’ordinateur du scanneur. Découvrez comment empêcher l’utilisation de l’UC de 100% et gérer l’utilisation de votre UC à l’aide de [deux nouveaux paramètres avancés **ScannerMaxCPU**et **ScannerMinCPU**](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#limit-cpu-consumption). 

- Vous pouvez maintenant configurer le scanneur d’étiquetage unifié pour ignorer des fichiers spécifiques en fonction de leurs attributs de fichier. Définissez la liste des attributs de fichier qui déclenchent l’omission d’un fichier à l’aide du nouveau paramètre avancé **[ScannerFSAttributesToSkip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes-public-preview)** .

**Nouvelles fonctionnalités pour le client d’étiquetage unifié :**

- Les [fenêtres contextuelles de justification](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) s’affichent désormais pour les modifications apportées aux étiquettes par défaut dans le client d’étiquetage unifié.
    
- Intégration plus lisse avec les marquages de contenu visuel appliqués par Office. Pour plus d’informations sur la configuration des marquages de contenu dans le document Office, consultez [Comment configurer une étiquette pour les marquages visuels pour Azure information protection](../configure-policy-markings.md).

- La nouvelle propriété avancée **WordShapeNameToRemove** permet de supprimer le marquage de contenu dans les documents Word créés par des applications tierces. En savoir plus sur la façon d' [identifier les noms de formes existants et de les définir en vue de leur suppression à l’aide de **WordShapeNameToRemove**](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#remove-headers-and-footers-from-other-labeling-solutions).

**Nouveaux journaux d’audit générés pour les fichiers supprimés**

Les journaux d’audit sont désormais générés chaque fois que l’analyseur détecte qu’un fichier qui avait été analysé précédemment est maintenant supprimé.

Pour plus d'informations, consultez les pages suivantes :
- [Fichiers journaux d’audit supprimés](../audit-logs.md#file-removed-audit-logs)
- [Rapports centraux d’Azure Information Protection](../reports-aip.md)

**Application de TLS 1.2**

À partir de cette version du client Azure Information Protection, seules les versions TLS 1,2 ou ultérieures sont prises en charge.
    
Les clients qui ont une configuration TLS qui ne prend pas en charge TLS 1,2 doivent migrer vers le programme d’installation qui prend en charge TLS 1,2 pour utiliser les stratégies de Azure Information Protection, les jetons, l’audit et la protection, ainsi que pour recevoir la communication basée sur Azure Information Protection. 
    
Pour plus d’informations sur la configuration requise, consultez [firewalls and Network infrastructure Requirements](../requirements.md#firewalls-and-network-infrastructure).

**Correctifs et améliorations** 
- Améliorations de SQL pour le scanneur :
    - Performances
    - Fichiers avec un grand nombre de types d’informations
    
- Améliorations de l’analyse SharePoint pour :
    - Analyse des performances
    - Fichiers avec des caractères spéciaux dans le chemin d’accès
    - Bibliothèques avec grand nombre de fichiers
    
    Pour afficher un guide de démarrage rapide pour l’utilisation de Azure Information Protection avec SharePoint, voir [démarrage rapide : Rechercher les informations sensibles que vous avez dans les fichiers stockés localement](../quickstart-findsensitiveinfo.md).
        
- Notifications utilisateur améliorées pour les stratégies manquantes. Pour plus d’informations sur les stratégies d’étiquette pour le client d’étiquetage unifié, consultez que les stratégies de l’étiquette [peuvent faire](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do) dans la documentation Microsoft 365.

- Les [étiquettes automatiques](../configure-policy-classification.md) sont désormais appliquées dans Excel pour les scénarios où un utilisateur commence à fermer un fichier sans l’enregistrer, comme c’est le cas lorsqu’un utilisateur enregistre activement un fichier.

- Les en-têtes et les pieds de page sont supprimés comme prévu, et non lors de chaque enregistrement de document, lorsque le paramètre [ExternalContentMarkingToRemove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) est configuré.

- Les [variables utilisateur dynamiques](../configure-policy-markings.md#using-variables-in-the-text-string) sont désormais affichées dans les marquages visuels d’un document comme prévu.

- Lorsque plusieurs comptes Exchange sont configurés et que le client Azure Information Protection Outlook est activé, les messages électroniques sont envoyés à partir du compte secondaire comme prévu. Pour plus d’informations sur la configuration du client d’étiquetage unifié avec Outlook, voir [conditions préalables supplémentaires pour le client d’étiquetage unifié Azure information protection](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).

- Lorsqu’un document avec une étiquette de confidentialité plus élevée est glissé et déposé dans un message électronique, le message électronique reçoit désormais automatiquement l’étiquette de confidentialité la plus élevée comme prévu. Pour plus d’informations sur l’étiquetage des fonctionnalités clientes, consultez le [tableau comparatif des clients d’étiquetage](use-client.md#compare-the-labeling-clients-for-windows-computers).

- Les autorisations personnalisées sont désormais appliquées aux courriers électroniques comme prévu, lorsque les adresses de messagerie incluent à la fois une apostrophe (') et un point (.) Pour plus d’informations sur la configuration du client d’étiquetage unifié avec Outlook, voir [conditions préalables supplémentaires pour le client d’étiquetage unifié Azure information protection](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).

- Par défaut, le propriétaire NTFS d’un fichier est perdu lorsque le fichier est étiqueté par le scanneur d’étiquetage unifié, PowerShell ou l’extension de l’Explorateur de fichiers. Vous pouvez maintenant configurer le système pour conserver le propriétaire NTFS du fichier en définissant le paramètre avancé New **[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** sur **true**. 

    Le paramètre avancé **UseCopyAndPreserveNTFSOwner** nécessite une connexion réseau fiable et à faible latence entre le scanneur et le référentiel analysé.


## <a name="version-261110"></a>Version 2.6.111.0 

**Publication** le 03/09/2020

**Nouvelles fonctionnalités :**

- Version de disponibilité générale du [scanneur](../deploy-aip-scanner.md), pour inspecter et étiqueter des documents dans des magasins de données locaux. 

- Lié au [scanneur](../deploy-aip-scanner.md) :
    - [Simplification de la découverte des sous-sites et SharePoint locaux](https://docs.microsoft.com/azure/information-protection/quickstart-findsensitiveinfo#permission-users-to-scan-sharepoint-repositories). La définition de chaque site spécifique n’est plus nécessaire. 
    - Propriété avancée pour le [dimensionnement du segment SQL](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#storage-requirements-and-capacity-planning-for-sql-server) ajouté.
    - Les administrateurs ont désormais la possibilité d' [arrêter des analyses existantes et d’effectuer une nouvelle analyse](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#stop-a-scan) si une modification a été apportée à l’étiquette par défaut.
    - Par défaut, l’analyseur définit maintenant une télémétrie minimale pour des analyses plus rapides et une taille de journal réduite et les types d’informations sont maintenant mis en cache dans la base de données. En savoir plus sur l' [optimisation du scanneur](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#optimizing-the-performance-of-the-scanner). 
    - Le scanneur prend désormais en charge des déploiements distincts pour la base de données et le service, tandis que les droits **sysadmin** sont nécessaires uniquement pour le déploiement de base de données.
    - Améliorations apportées aux performances de l’analyseur. 

- Modification de l’applet de commande [PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell) **Set-AIPFileLabel** pour permettre la suppression de la protection des fichiers PST, rar, 7zip et MSG. Cette fonctionnalité est désactivée par défaut et doit être activée à l’aide de l’applet de commande [Set-LabelPolicy](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations) , comme décrit [ici](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#enable-removal-of-protection-from-compressed-files).  

- Ajout de la possibilité pour les administrateurs de Azure Information Protection de contrôler le moment où les extensions pfile sont utilisées pour les fichiers. En savoir plus sur la [modification des types de fichiers protégés](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#change-which-file-types-to-protect). 

- Prise en charge du marquage visuel dynamique ajoutée pour les applications et les variables. En savoir plus sur la [Configuration des étiquettes pour les marquages visuels](https://docs.microsoft.com/azure/information-protection/configure-policy-markings). 

- Améliorations apportées à [des conseils de stratégie personnalisables pour les étiquettes automatiques et recommandées](use-client.md).   

- Prise en charge ajoutée pour la [fonctionnalité d’étiquetage hors connexion](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#support-for-disconnected-computers) avec les applications Office dans le client d’étiquetage unifié.

**Correctifs :**

- Dans les cas où les utilisateurs ont tenté sans succès d’ouvrir des fichiers TIFF protégés et des fichiers TIFF créés par RightFax, les fichiers TIFF s’ouvrent et restent stables comme prévu.  
- Les endommagements précédents des fichiers txt et PDF protégés sont résolus.
- Une étiquette incohérente entre les Log Analytics **automatique** et **manuelle** a été corrigée. 
- Des problèmes d’héritage inattendus identifiés entre les nouveaux e-mails et le dernier e-mail ouvert d’un utilisateur sont désormais résolus.  
- La protection des fichiers. msg en tant que. msg. fichiers pfile fonctionne à présent comme prévu. 
- Les autorisations de copropriétaire ajoutées à partir des paramètres définis par l’utilisateur Office sont désormais appliquées comme prévu. 
- Lorsque vous entrez des autorisations de mise à niveau vers la version antérieure, le texte ne peut plus être entré lorsque d’autres options sont déjà sélectionnées. 


## <a name="version-25330"></a>Version 2.5.33.0

**Publication**: 10/23/2019

Pris en charge jusqu’à 09/09/2020

**Nouvelles fonctionnalités :**

- Version préliminaire du [scanneur](../deploy-aip-scanner.md), pour inspecter et étiqueter les documents des magasins de données locaux. Avec cette version du scanneur :
    
    - Plusieurs scanneurs peuvent partager la même SQL Server base de données lorsque vous configurez les scanneurs pour qu’ils utilisent le même profil de scanneur. Cette configuration facilite la gestion de plusieurs scanneurs et entraîne des temps d’analyse plus rapides. Lorsque vous utilisez cette configuration, attendez toujours que l’installation d’un scanneur soit terminée avant d’installer un autre scanneur avec le même profil.
    
    - Vous devez spécifier un profil lorsque vous installez le scanneur et que la base de données du scanneur est nommée **AIPScannerUL_ \<profile_name> **. Le paramètre de *Profil* est également obligatoire pour Set-AIPScanner.
    
    - Vous pouvez définir une étiquette par défaut pour tous les documents, même si les documents sont déjà étiquetés. Dans les paramètres Profil du scanneur ou référentiel, affectez à l’option **Renommer les fichiers** la valeur **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée.
    
    - Vous pouvez supprimer des étiquettes existantes de tous les documents. cette action comprend la suppression de la protection si elle a été appliquée précédemment par une étiquette. La protection appliquée indépendamment d’une étiquette est conservée. Cette configuration de scanneur est effectuée dans les paramètres de profil du scanneur ou de référentiel avec les paramètres suivants :
        - **Étiqueter les fichiers en fonction du contenu**: **désactivé**
        - **Étiquette par défaut**: **aucune**
        - **Renommer les fichiers**: **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée
    
    - Comme avec le scanneur du client classique, par défaut, le scanneur protège les fichiers Office et les fichiers PDF. Vous pouvez protéger d’autres types de fichiers lorsque vous utilisez un [paramètre avancé PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).
    
    - Les ID d’événement pour les cycles de scanneur en début et en fin ne sont pas écrits dans le journal des événements Windows. Utilisez plutôt le Portail Azure pour ces informations.
    
    - Problème connu : les étiquettes nouvelles et renommées ne peuvent pas être sélectionnées en tant qu’étiquette par défaut pour les paramètres de profil de scanneur ou de référentiel. Solutions de contournement :
        - Pour les nouvelles étiquettes : dans la Portail Azure, [Ajoutez l’étiquette](../configure-policy-add-remove-label.md) que vous souhaitez utiliser à la stratégie globale ou à une stratégie délimitée.
        - Pour les étiquettes renommées : fermez et rouvrez le Portail Azure.
    
    Vous pouvez mettre à niveau les analyseurs à partir du client Azure Information Protection (Classic). Après la mise à niveau, qui crée une base de données, le moteur de base de données analyse à nouveau tous les fichiers lors de sa première exécution. Pour obtenir des instructions, consultez [mise à niveau de l’analyseur de Azure information protection](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner) à partir du Guide de l’administrateur.
    
    Pour plus d’informations, consultez l’annonce du billet de blog : l’étiquetage unifié la préversion du [scanneur AIP offre une montée en charge horizontale et bien plus encore.](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)

- L’applet de commande PowerShell [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) possède de nouveaux paramètres (*AppID*, *AppSecret*, *TenantId*, *DelegatedUser*et *OnBehalfOf*) pour lorsque vous souhaitez étiqueter des fichiers de manière non interactive, ainsi qu’une nouvelle procédure pour inscrire une application dans Azure ad. Les exemples de scénarios incluent le scanneur et les scripts PowerShell automatisés pour étiqueter les documents. Pour obtenir des instructions, consultez [Comment étiqueter des fichiers de manière non interactive](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) à partir du Guide de l’administrateur.
    
    Notez que *DelegatedUser* est un nouveau paramètre depuis la dernière version d’évaluation du client d’étiquetage unifié et que les autorisations de l’API pour l’application inscrite ont donc changé.

- Nouveau paramètre avancé de stratégie d’étiquette PowerShell pour [modifier les types de fichiers à protéger](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

- Nouveau paramètre avancé de stratégie d’étiquette PowerShell pour [étendre vos règles de migration d’étiquette aux propriétés SharePoint](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-sharepoint-properties).

- Les types d’informations sensibles personnalisés correspondants sont envoyés à [Azure information protection Analytics](../reports-aip.md).

- L’étiquette appliquée affiche la couleur configurée pour l’étiquette, si une [couleur a été configurée](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).

- Lorsque vous ajoutez ou modifiez des paramètres de protection sur une étiquette, le client réapplique l’étiquette avec ces derniers paramètres de protection lors de l’enregistrement du document suivant. De même, le scanneur réapplique l’étiquette avec ces derniers paramètres de protection lors de la prochaine analyse du document en mode d’application.

- [Prise en charge des ordinateurs déconnectés](clientv2-admin-guide-customizations.md#support-for-disconnected-computers) en exportant des fichiers à partir d’un client et en les copiant manuellement sur l’ordinateur déconnecté. Notez que cette configuration est prise en charge pour l’étiquetage avec l’Explorateur de fichiers, PowerShell et le scanneur. Cette configuration n’est pas prise en charge pour l’étiquetage avec les applications Office.

- New cmdlet, [Export-AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs), pour rassembler tous les fichiers journaux de%LocalAppData%\Microsoft\MSIP\Logs et les enregistre dans un fichier unique et compressé avec un format. zip. Ce fichier peut ensuite être envoyé à Support Microsoft si vous êtes invité à envoyer des fichiers journaux pour vous aider à examiner un problème signalé.

**Correctifs :**

- Vous pouvez apporter des modifications à un fichier protégé à l’aide de l’Explorateur de fichiers et cliquer avec le bouton droit après avoir supprimé un mot de passe pour le fichier.

- Vous pouvez ouvrir des fichiers protégés en mode natif dans la visionneuse sans avoir à [utiliser le droit](../configure-usage-rights.md#usage-rights-and-descriptions)enregistrer sous, exporter (exporter).

- Les étiquettes et les paramètres de stratégie sont actualisés comme prévu sans devoir exécuter [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication?)ou supprimer manuellement le dossier%localappdata%\Microsoft\MSIP\mip.

**Modifications supplémentaires**

- [Réinitialiser les paramètres](clientv2-admin-guide.md#more-information-about-the-reset-settings-option) supprime maintenant les \\ *\<ProcessName.exe\>* dossiers%LocalAppData%\Microsoft\MSIP\mip au lieu du \\ *\<ProcessName\>* dossier%localappdata%\Microsoft\MSIP\mip \mip.

- L' [AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) d’accès à la sécurité comprend désormais l’ID de contenu d’un document protégé.


## <a name="next-steps"></a>Étapes suivantes

Vous ne savez pas si l’étiquetage unifié est le bon client à installer ?  Consultez [choisir le client d’étiquetage à utiliser pour les ordinateurs Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Pour plus d’informations sur l’installation et l’utilisation du client d’étiquetage unifié : 

- Pour les utilisateurs : [Télécharger et installer le client](install-unifiedlabelingclient-app.md)

- Pour les administrateurs : Azure Information Protection le Guide de l' [administrateur du client d’étiquetage unifié](clientv2-admin-guide.md)

