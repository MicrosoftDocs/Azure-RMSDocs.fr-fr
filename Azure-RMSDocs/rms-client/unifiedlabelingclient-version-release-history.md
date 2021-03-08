---
title: Nouveautés de Azure Information Protection (AIP)-historique des versions & stratégie de support
description: Découvrez les nouveautés du client d’étiquetage unifié de l’Azure Information Protection (AIP) pour Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e416a7f9b363dc1c0d773561b2c3a1eb6cd56926
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446981"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l’historique des versions et la stratégie de support du client d’étiquetage unifié

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP et versions héritées de Windows et d’Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez [l’historique des versions du client classique et la stratégie de support](client-version-release-history.md). *

Cet article décrit les nouvelles fonctionnalités disponibles pour le client d’étiquetage unifié, ainsi que les informations de maintenance et les chronologies de support pour chaque version du client unifié AIP.

Vous pouvez télécharger le client d’étiquetage unifié Azure Information Protection à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).

Après un bref délai de quatre semaines, la dernière version de la disponibilité générale est également incluse dans le catalogue Microsoft Update. Les versions de Azure information protection ont un nom de produit de **Microsoft Azure information protection**  >  **Microsoft Azure information protection client d’étiquetage unifié** et une classification des **mises à jour**.

L’inclusion de Azure Information Protection dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou d’Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [mise à niveau et maintenance du client d’étiquetage unifié Azure information protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

## <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version de disponibilité générale de la Azure Information Protection client d’étiquetage unifiée est prise en charge pendant six mois après la publication de la version GA suivante. La documentation n’inclut pas d’informations sur les versions non pris en charge du client. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions de la disponibilité générale qui ne sont plus prises en charge

|Version du client|Date de publication|
|--------------|-------------|
| 2.7.96  |01/20/2021 |
|2.6.111.0 | 03/09/2020|
|2.5.33.0 |23/10/2019|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|
| | |

Le format de date utilisé sur cette page est *mois/jour/année*.

### <a name="release-information"></a>Informations de version

Utilisez les informations suivantes pour découvrir les nouveautés ou les modifications apportées à une version prise en charge de l’Azure Information Protection client d’étiquetage unifié pour Windows. La dernière version est répertoriée en première position. Le format de date utilisé sur cette page est *mois/jour/année*.

Notez que les fonctionnalités de Azure Information Protection sont actuellement en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale.

> [!NOTE]
> Les correctifs mineurs ne sont pas répertoriés. par conséquent, si vous rencontrez un problème avec le client d’étiquetage unifié, nous vous recommandons de vérifier s’il est corrigé avec la dernière version de la mise à la disposition générale. Si le problème persiste, vérifiez la version préliminaire actuelle (si disponible).
>
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

Le client d’étiquetage unifié remplace le client Azure Information Protection Classic. Pour comparer les fonctionnalités et les fonctionnalités avec le client Classic, consultez [comparer les solutions d’étiquetage pour les ordinateurs Windows](use-client.md#compare-the-labeling-solutions-for-windows-computers).

## <a name="version-210460-for-co-authoring-public-preview"></a>Version 2.10.46.0 pour la co-création (préversion publique)

2.10.46.0 d’étiquetage unifiée version du client

**Version** 03/02/2021

Cette version dédiée de Azure Information Protection fournit une version préliminaire publique des fonctionnalités de co-création récemment prises en charge dans Microsoft 365.

La co-création d’applications Office permet à plusieurs utilisateurs de modifier des documents étiquetés et chiffrés par des [étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels).

> [!IMPORTANT]
> Pour tirer parti des fonctionnalités de co-création de la version préliminaire publique, vous devez télécharger et installer le fichier d’installation dédié pour cette version. Sur le [site de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018), téléchargez et installez le `AzInfoProtection_2.10.46_CoAuthoring_PublicPreview.exe`  fichier.
>
> Votre système doit également respecter les exigences de version indiquées dans la [Microsoft 365 conditions préalables pour la co-création](/microsoft-365/compliance/sensitivity-labels-coauthoring#prerequisites).
>

Avant de commencer, nous vous recommandons de passer en revue toutes les conditions préalables et limitations associées. Pour plus d’informations, consultez :

- [Activez la co-création de fichiers chiffrés avec des étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels-coauthoring) dans la documentation de Microsoft 365.
- [Problèmes connus de la co-création dans AIP](../known-issues.md#known-issues-for-co-authoring-public-preview)
## <a name="version-210430-for-dlp-policies-public-preview"></a>Version 2.10.43.0 pour les stratégies DLP (version préliminaire publique)

2.10.43.0 de version de scanneur d’étiquetage unifiée

**Version** 03/02/2021

Cette version dédiée de Azure Information Protection fournit une version préliminaire publique de la prise en charge des stratégies de protection contre la perte de données (DLP) prises en charge par Microsoft 365. 

- **L’utilisation d’une stratégie DLP** permet à l’analyseur de détecter les fuites de données potentielles en faisant correspondre les règles DLP aux fichiers stockés dans les partages de fichiers et SharePoint Server. 

- [**Activez les règles DLP dans votre travail d’analyse de contenu**](../deploy-aip-scanner-configure-install.md#use-a-dlp-policy-public-preview) pour réduire l’exposition des fichiers qui correspondent à vos stratégies DLP. 

    Le scanneur peut réduire l’accès aux fichiers aux propriétaires de données uniquement ou réduire l’exposition aux groupes à l’ensemble du réseau, tels que **tout le monde**, **les utilisateurs authentifiés** ou **les utilisateurs du domaine**.

- **L’analyse de vos fichiers avec les règles DLP activé crée également des rapports d’autorisations sur les fichiers**. Interrogez ces rapports pour examiner les expositions de fichiers spécifiques ou explorer l’exposition d’un utilisateur spécifique à des fichiers analysés.

Les paramètres d’application ou de test de la stratégie DLP sont configurés dans le [Centre de conformité Microsoft 365](/microsoft-365/compliance/create-test-tune-dlp-policy#turn-on-a-dlp-policy).

> [!IMPORTANT]
> Pour tirer parti de la prise en charge de DLP dans la version préliminaire publique, vous devez télécharger et installer le fichier d’installation dédié pour cette version. Sur le [site de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018), téléchargez et installez le `AzInfoProtection_2.10.43_DLP_PublicPreview.exe` fichier.
> 
Pour plus d’informations, y compris les conditions de licence, consultez :

- [Configurer une stratégie DLP dans le scanneur AIP](../deploy-aip-scanner-configure-install.md#use-a-dlp-policy-public-preview)
- En [savoir plus sur le Microsoft 365 analyseur local pour la protection contre la perte de données](/microsoft-365/compliance/dlp-on-premises-scanner-learn), dans la documentation de Microsoft 365
- [Prise en main du scanneur local pour la protection contre la perte de données](/microsoft-365/compliance/dlp-on-premises-scanner-get-started)
- [Utiliser le Microsoft 365 analyseur local pour la protection contre la perte de données](/microsoft-365/compliance/dlp-on-premises-scanner-use)



## <a name="version-29116"></a>Version 2.9.116 

2.9.116 de la version du client et du scanneur d’étiquetage unifiée 

**Publication** le 02/08/2021

**Problèmes résolus** Les utilisateurs peuvent désormais afficher les fichiers protégés comme prévu dans les scénarios suivants :

- Lorsque des fichiers protégés sont partagés avec des utilisateurs qui n’ont pas de stratégie AIP configurée, telle que des utilisateurs externes. Ce problème s’est produit uniquement avec l' [application de visionneuse AIP](clientv2-view-use-files.md).

- Lorsque le contenu avec une étiquette délimitée est partagé avec des utilisateurs ou des groupes qui ne sont pas inclus dans la portée de l’étiquette. Ce problème s’est produit avec l' [application de visionneuse AIP](clientv2-view-use-files.md) et lors de l’affichage ou de la classification du contenu partagé via l' [Explorateur de fichiers](clientv2-classify-protect.md#using-file-explorer-to-classify-and-protect-files).

Pour plus d’informations, consultez le Guide de l' [utilisateur du client d’étiquetage unifié AIP](clientv2-user-guide.md).
## <a name="version-291110"></a>Version 2.9.111.0

2.9.111.0 de la version du client et du scanneur d’étiquetage unifiée

**Publication** le 01/13/2021

**Pris en charge jusqu’à** 08/08/2021

Cette version comprend les nouvelles fonctionnalités, les correctifs et les améliorations suivants pour le scanneur d’étiquetage et le client unifiés :

- **Nouvelles fonctionnalités pour le scanneur**:

    - [Prise en charge de PowerShell pour les serveurs de scanneur déconnectés](#powershell-support-for-disconnected-scanner-servers)
    - [Prise en charge des référentiels NFS dans les travaux d’analyse de contenu](#support-for-nfs-repositories-in-content-scan-jobs-public-preview) (version préliminaire publique)
    - [Ajout de la prise en charge de types d’informations sensibles supplémentaires](#added-support-for-additional-sensitive-information-types)

- **Nouvelles fonctionnalités pour le client**:

    - [Suivre l’accès aux documents et révoquer l’accès](#track-document-access-and-revoke-access-public-preview) (version préliminaire publique)
    - [Ajout de la prise en charge de types d’informations sensibles supplémentaires](#added-support-for-additional-sensitive-information-types)

- **Correctifs et améliorations**:

    - [Correctifs et améliorations pour le scanneur d’étiquetage unifié](#fixes-and-improvements-for-the-unified-labeling-scanner)
    - [Correctifs et améliorations pour le client d’étiquetage unifié](#fixes-and-improvements-for-the-unified-labeling-client)

- **Problème connu**: un problème a été identifié dans la dernière version GA (2.9.111) où certains utilisateurs n’ont pas pu afficher les fichiers protégés dans les scénarios suivants :

    - Lorsque des fichiers protégés sont partagés avec des utilisateurs qui n’ont pas de stratégie AIP configurée, telle que des utilisateurs externes. Ce problème se produit uniquement avec l' [application de visionneuse AIP](clientv2-view-use-files.md).

    - Lorsque le contenu avec une étiquette délimitée est partagé avec des utilisateurs ou des groupes qui ne sont pas inclus dans la portée de l’étiquette. Ce problème se produit à la fois avec l' [application de visionneuse AIP](clientv2-view-use-files.md) et lors de l’affichage ou de la classification du contenu partagé via l' [Explorateur de fichiers](clientv2-classify-protect.md#using-file-explorer-to-classify-and-protect-files).

### <a name="powershell-support-for-disconnected-scanner-servers"></a>Prise en charge de PowerShell pour les serveurs de scanneur déconnectés

Le [Azure information protection analyseur local](../deploy-aip-scanner.md) prend désormais en charge la gestion des travaux d’analyse de contenu via PowerShell, pour les serveurs de scanneurs qui ne peuvent pas se connecter à Internet ou pour les scanneurs dans un [environnement Azure China 21ViaNet (Chine souverain)](/microsoft-365/admin/services-in-china/parity-between-azure-information-protection#manage-azure-information-protection-content-scan-jobs).

Pour prendre en charge les serveurs de scanneurs déconnectés ou Azure China 21Vianet, nous avons ajouté les nouvelles applets de commande suivantes :

|Applet de commande  |Description  |
|---------|---------|
|**[Add-AIPScannerRepository](/powershell/module/azureinformationprotection/add-aipscannerrepository)**     | Ajoute un nouveau référentiel à votre travail d’analyse de contenu.        |
|**[AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob)**     |      Obtient des détails sur votre travail d’analyse de contenu.   |
|**[AIPScannerRepository](/powershell/module/azureinformationprotection/get-aipscannerrepository)**     |  Obtient des détails sur les dépôts définis pour votre travail d’analyse de contenu.       |
|**[Remove-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)**       |    Supprime votre travail d’analyse de contenu.     |
| **[Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/remove-aipscannerrepository)**    |   Supprime un référentiel de votre travail d’analyse de contenu.      |
|**[Set-AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob)**     |   Définit les paramètres de votre travail d’analyse de contenu.      |
**[Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository)**     |   Définit les paramètres d’un référentiel existant dans votre travail d’analyse de contenu.      |
| | |

L’applet de commande [**Set-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/set-mipnetworkdiscovery) a également été ajoutée pour fournir une prise en charge supplémentaire, ce qui vous permet de mettre à jour les paramètres d’installation du service de découverte du réseau via PowerShell.

Pour plus d’informations, consultez [lorsque le serveur de scanneur ne peut pas disposer d’une connexion Internet](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity) et [configurer le scanneur](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).

### <a name="support-for-nfs-repositories-in-content-scan-jobs-public-preview"></a>Prise en charge des référentiels NFS dans les travaux d’analyse de contenu (version préliminaire publique)

Vous pouvez désormais ajouter des référentiels NFS à vos travaux d’analyse de contenu, en plus des partages de fichiers SMB et des référentiels SharePoint.

Pour prendre en charge les analyses sur les partages NFS, les services pour NFS doivent être déployés sur l’ordinateur du scanneur :

1. Sur votre ordinateur, accédez à la boîte de dialogue des paramètres **fonctionnalités Windows (activer ou désactiver des fonctionnalités Windows)** .

1. Sélectionnez les éléments suivants :

    - **Services pour NFS**
        - **Outils d’administration**
        - **Client pour NFS**

Pour plus d’informations, consultez [créer un travail d’analyse du contenu](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job).

### <a name="added-support-for-additional-sensitive-information-types"></a>Ajout de la prise en charge de types d’informations sensibles supplémentaires

Nous avons ajouté la prise en charge de types d’informations sensibles supplémentaires dans Azure Information Protection, tels que le **numéro d’entreprise Australie**, le **numéro de société en Australie** ou la carte d' **identité autrichienne**.

Pour plus d’informations, consultez les [définitions d’entité de type d’informations sensibles](/microsoft-365/compliance/sensitive-information-type-entity-definitions) dans la documentation de Microsoft 365.

### <a name="track-document-access-and-revoke-access-public-preview"></a>Suivre l’accès aux documents et révoquer l’accès (version préliminaire publique)

Une fois que vous avez effectué une mise à niveau vers la version 2.9.111.0, tous les documents protégés qui ne sont pas encore enregistrés pour le suivi sont enregistrés la prochaine fois qu’ils sont ouverts sur un ordinateur sur lequel est installé le client d’étiquetage unifié AIP. Les documents protégés sont pris en charge pour la suivi et la révocation, même s’ils ne sont pas étiquetés.

Si vos documents sont enregistrés pour le suivi, permet aux administrateurs d’utiliser PowerShell pour effectuer le suivi de l’accès aux documents et de révoquer l’accès si nécessaire.

Une fois que vous avez mis à niveau, les utilisateurs finaux peuvent également révoquer l’accès pour les documents qu’ils ont protégés. Pour révoquer l’accès à partir de Microsoft Office Apps, utilisez l’option nouveau **révoquer l’accès** dans le menu **sensibilité** .

Pour plus d’informations, consultez :

- [Guide de l’administrateur : suivre et révoquer l’accès aux documents avec Azure Information Protection](track-and-revoke-admin.md)
- [Guide de l’utilisateur : révoquer l’accès aux documents avec Azure Information Protection](revoke-access-user.md)
- [Problèmes connus pour le suivi et la révocation de l’accès aux documents](../known-issues.md#known-issues-for-track-and-revoke-features-public-preview)

Si vous avez des exigences de confidentialité dans votre organisation ou région qui nécessitent que vous désactiviez les fonctionnalités de suivi des documents, consultez les [procédures suivre et révoquer l’administrateur](track-and-revoke-admin.md#turn-off-track-and-revoke-features-for-your-tenant).

**Mises à niveau à partir du client classique**

Le client standard AIP prend en charge les fonctionnalités suivre et révoquer à l’aide du [portail de suivi Microsoft](client-track-revoke.md#using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered). Ce portail de suivi n’est pas pertinent lorsque vous travaillez avec le client d’étiquetage unifié.
 
Pour afficher les données de suivi avec le client d’étiquetage unifié, utilisez uniquement les commandes PowerShell, comme décrit dans le Guide de l' [administrateur](track-and-revoke-admin.md).

### <a name="fixes-and-improvements-for-the-unified-labeling-scanner"></a>Correctifs et améliorations pour le scanneur d’étiquetage unifié

Les correctifs suivants ont été fournis dans la version 2.9.111.0 de l' [Azure information protection scanneur d’étiquetage unifié](../deploy-aip-scanner.md):

- Ajout de la prise en charge des traits d’Union ( **-** ) dans les noms des [bases de données du scanneur](../deploy-aip-scanner-prereqs.md)
- Mises à jour dans les rapports pour lesquelles l’option **[étiqueter les fichiers en fonction du contenu](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job)** a la valeur **désactivé**
- [Amélioration de la consommation de mémoire](../deploy-aip-scanner-configure-install.md#optimize-scanner-performance) pour un grand nombre de correspondances de type d’informations
- Prise en charge des chemins d’accès [locaux SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) qui se terminent par une barre oblique ( **/** )
- Augmentation de la [Vitesse](../deploy-aip-scanner-configure-install.md#optimize-scanner-performance) d’analyse SharePoint
- Prise en charge pour [éviter un délai d’expiration](clientv2-admin-guide-customizations.md#avoid-scanner-timeouts-in-sharepoint) lors de l’analyse d’un serveur SharePoint.

### <a name="fixes-and-improvements-for-the-unified-labeling-client"></a>Correctifs et améliorations pour le client d’étiquetage unifié

- Problèmes résolus pour l' [étiquetage des e-mails](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-emails) à partir d’Office MSI, par exemple lors de la réponse à un message électronique ou de son transfert.

- Les événements du [Journal d’audit NewLabel](../audit-logs.md#new-label-audit-logs) incluent désormais la source de l’action, pour les événements générés par les courriers électroniques envoyés depuis Outlook.

- Problèmes résolus là où la stratégie n’était parfois pas mise à jour sans effacer le cache, après avoir [apporté des modifications à la stratégie d’étiquette dans Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy).

- Le mode Outlook Preview génère désormais [des journaux d’audit pour les événements de découverte](../audit-logs.md#discover-audit-logs)

- Les [étiquettes recommandées](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) et le [marquage visuel](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) sont appliqués comme prévu dans Outlook. 

- Ajout de la prise en charge de la [recherche de destinataires dans les listes de distribution Outlook](clientv2-admin-guide-customizations.md#expand-outlook-distribution-lists-when-searching-for-email-recipients), par exemple lorsque les paramètres [OutlookBlockTrustedDomains](clientv2-admin-guide-customizations.md#to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels) et [OutlookBlockUntrustedCollaborationLabel](clientv2-admin-guide-customizations.md#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels) sont configurés.

    Lorsque vous activez cette fonctionnalité, nous vous recommandons de déclencher également la valeur de délai d’attente par défaut, comme défini dans le paramètre [OutlookGetEmailAddressesTimeOutMSProperty](clientv2-admin-guide-customizations.md#expand-outlook-distribution-lists-when-searching-for-email-recipients) .

- Mises à jour de l' [ordre de priorité](clientv2-admin-guide-customizations.md#order-of-precedence---how-conflicting-settings-are-resolved) utilisé lorsque plusieurs stratégies d’étiquette sont configurées pour un utilisateur, chacune avec des paramètres avancés en conflit.

    Dans ce cas, les paramètres avancés de la première stratégie sont toujours appliqués, en fonction de l’ordre des stratégies dans le centre d’administration. L’exception pour *OutlookDefaultLabel* est maintenant supprimée.

- Dans un scénario où **% AppData% (Appdata\Roaming)** pointe vers une structure de dossiers Windows non définie par défaut, les fichiers des dossiers mappés à des répertoires utilisateur sont désormais [exclus de l’étiquetage et de la protection](clientv2-admin-guide-file-types.md#file-types-excluded-from-classification-and-protection) comme prévu, en fonction de la configuration.

- [Nouveau paramètre de client avancé](clientv2-admin-guide-customizations.md#remove-all-shapes-of-a-specific-shape-name) (**PowerPointRemoveAllShapesByShapeName**), ajouté pour supprimer des formes des en-têtes ou des pieds de page PowerPoint, en utilisant le nom de forme au lieu du texte à l’intérieur d’une forme.

## <a name="version-28850"></a>Version 2.8.85.0

2.8.85.0 de la version du client et du scanneur d’étiquetage unifiée

**Publication** le 09/22/2020

**Pris en charge jusqu’à** 7/13/2021

Cette version comprend les nouvelles fonctionnalités, les correctifs et les améliorations suivants pour le scanneur d’étiquetage et le client unifiés :

- **Nouvelles fonctionnalités pour le scanneur**:

    - [Analyses complètes facultatives pour les modifications détectées](#optional-full-rescans-for-changes-detected)
    - [Configurer des délais d’attente SharePoint](#configure-sharepoint-timeouts)
    - [Prise en charge](#network-discovery-support-public-preview) de la découverte du réseau (version préliminaire publique)

- **Nouvelles fonctionnalités pour le client**:

    - [Personnalisations de l’administrateur pour les fenêtres contextuelles AIP dans Outlook](#administrator-customizations-for-aip-popups-in-outlook)
    - [Personnalisations de l’administrateur pour les invites de justification](#administrator-customizations-for-justification-prompts)
    - [Mises à jour du journal d’audit](#audit-log-updates)
    - [Mises à jour de l’étiquetage basé sur un modèle DKE](#dke-template-based-labeling-updates)

- **Correctifs et améliorations :**

    - [Correctifs et améliorations de l’analyseur](#azure-information-protection-scanner-fixed-issues-version-28850)
    - [Correctifs et améliorations du client](#azure-information-protection-client-fixed-issues-version-28850)


### <a name="optional-full-rescans-for-changes-detected"></a>Analyses complètes facultatives pour les modifications détectées

Les administrateurs peuvent désormais ignorer une nouvelle analyse complète après avoir apporté des modifications aux stratégies ou aux travaux d’analyse de contenu. Si vous ignorez une nouvelle analyse complète, vos modifications ne sont appliquées que sur les fichiers qui ont été modifiés ou créés depuis la dernière analyse.

Par exemple, vous avez peut-être apporté des modifications qui affectent uniquement l’utilisateur final, comme dans les marquages visuels, et vous ne souhaitez pas prendre le temps nécessaire pour exécuter une nouvelle analyse complète immédiatement.

Ignorez la nouvelle analyse complète et immédiate, puis revenez plus tard pour [exécuter une nouvelle analyse complète](../deploy-aip-scanner-manage.md#rescanning-files) et appliquer vos modifications dans vos référentiels.

> [!IMPORTANT]
> Les administrateurs qui modifient leurs stratégies et les travaux d’analyse de contenu doivent maintenant comprendre les effets de ces modifications sur le contenu et déterminer si une nouvelle analyse complète est nécessaire.
>
> Par exemple, si vous avez modifié les paramètres de **stratégie de sensibilité** de **appliquer = désactivé** à **appliquer = on**, veillez à exécuter une nouvelle analyse complète pour appliquer vos étiquettes à votre contenu.
>

### <a name="configure-sharepoint-timeouts"></a>Configurer des délais d’attente SharePoint

Le délai d’attente par défaut pour les interactions SharePoint a été mis à jour à deux minutes, après quoi l’opération d’AIP a échoué.

Les administrateurs AIP peuvent également configurer des délais d’attente SharePoint, séparément pour toutes les requêtes Web et les requêtes Web de fichiers.

Pour plus d’informations, consultez [configurer des délais d’attente SharePoint](clientv2-admin-guide-customizations.md#configure-sharepoint-timeouts).

### <a name="network-discovery-support-public-preview"></a>Prise en charge de la découverte du réseau (version préliminaire publique)

Le scanneur d’étiquetage unifié comprend maintenant un nouveau service de **découverte du réseau** , qui vous permet d’analyser les adresses IP ou plages spécifiées pour les partages de fichiers réseau qui peuvent avoir un contenu sensible.

Le service de **découverte du réseau** met à jour les rapports de **référentiel** avec une liste d’emplacements de partage susceptibles d’être menacés, en fonction des autorisations et des droits d’accès découverts. Vérifiez les rapports de **référentiel** mis à jour pour vous assurer que vos travaux d’analyse de contenu incluent tous les référentiels devant être analysés.

> [!TIP]
> Pour plus d’informations, consultez [applets](#network-discovery-cmdlets-public-preview)de commande de découverte du réseau.

**Pour utiliser le service de découverte du réseau**

1. Mettez à niveau votre version de scanneur et vérifiez que votre cluster de scanneur est correctement configuré. Pour plus d’informations, consultez :
    - [Mise à niveau de votre scanneur](../deploy-aip-scanner-configure-install.md#upgrade-your-scanner)
    - [Créer un cluster de scanneur](../deploy-aip-scanner-configure-install.md#create-a-scanner-cluster)

1. Assurez-vous que Azure Information Protection Analytics est activé.

    Dans la Portail Azure, accédez à **Azure Information Protection > gérer > configurer Analytics (** préversion).

    Pour plus d’informations, consultez [central Reporting for Azure information protection (version préliminaire publique)](../reports-aip.md).

1. Activez la découverte du réseau en exécutant l’applet de commande PowerShell [**install-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) .

    > [!IMPORTANT]
    > Lors de l’exécution de cette applet de commande, veillez à utiliser un utilisateur faible comme valeur pour le paramètre **StandardDomainsUserAccount** afin de vous assurer que tout accès public aux dépôts est signalé.
    >
    > Cet utilisateur doit être membre du groupe **utilisateurs du domaine** uniquement et utilisé pour simuler un accès public aux dépôts.

1. Dans la Portail Azure, accédez à Azure Information Protection > **travaux d’analyse réseau** et [créez des travaux pour analyser des zones spécifiques de votre réseau](../deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview).

1. Utilisez les rapports générés dans le nouveau volet [**référentiels**](../deploy-aip-scanner-configure-install.md#analyze-risky-repositories-found-public-preview) pour rechercher les partages de fichiers réseau supplémentaires qui peuvent être menacés. Ajoutez tous les partages de fichiers risqués à vos [travaux d’analyse de contenu](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job) pour analyser les référentiels ajoutés au contenu sensible.

### <a name="network-discovery-cmdlets-public-preview"></a>Applets de commande de découverte du réseau (version préliminaire publique)

Les applets de commande PowerShell ajoutées pour la découverte du réseau sont les suivantes :

|Applet de commande  |Description  |
|---------|---------|
|[**MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryConfiguration)     |   Obtient le paramètre actuel indiquant si le service de découverte du réseau extrait les données d’analyse réseau de la configuration par défaut, en ligne ou hors connexion exportée à partir de la Portail Azure.      |
|[**MIPNetworkDiscoveryJobs**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryJobs)     |    Obtient la liste des travaux d’analyse réseau actuellement configurés.     |
|[**MIPNetworkDiscoveryStatus**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryStatus)     |     Obtient l’état actuel de tous les travaux d’analyse réseau configurés dans votre locataire.    |
| [**Import-MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Import-MIPNetworkDiscoveryConfiguration)     |    Importe la configuration d’un travail d’analyse réseau à partir d’un fichier.     |
| [**Install-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)| Installe le service de découverte du réseau |
|[**Set-MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration)     |   Définit la configuration pour que le service de découverte du réseau extraie les données d’analyse réseau de la configuration par défaut, en ligne ou d’un fichier hors connexion exporté à partir du Portail Azure.      |
|[**Start-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Start-MIPNetworkDiscovery)     |  Exécute immédiatement un travail d’analyse réseau spécifique.       |
|[**Uninstall-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Uninstall-MIPNetworkDiscovery)     |  Désinstalle le service de découverte du réseau.       |
| | |


### <a name="administrator-customizations-for-aip-popups-in-outlook"></a>Personnalisations de l’administrateur pour les fenêtres contextuelles AIP dans Outlook

Les administrateurs AIP peuvent désormais personnaliser les fenêtres contextuelles qui s’affichent dans Outlook pour les utilisateurs finaux, telles que des fenêtres contextuelles pour les e-mails bloqués, les messages d’avertissement et les invites de justification.

Pour plus d’informations, y compris plusieurs exemples de règles pour les scénarios d’utilisation courants, consultez [personnaliser les messages de la fenêtre contextuelle Outlook](clientv2-admin-guide-customizations.md#customize-outlook-popup-messages).

### <a name="administrator-customizations-for-justification-prompts"></a>Personnalisations de l’administrateur pour les invites de justification

Les administrateurs AIP peuvent désormais personnaliser l’une des options dans les invites de justification qui s’affichent lorsque les utilisateurs finaux modifient les étiquettes de classification sur les documents et les e-mails.

Pour plus d’informations, consultez [personnaliser les textes d’invite de justification pour les étiquettes modifiées](clientv2-admin-guide-customizations.md#customize-justification-prompt-texts-for-modified-labels).

### <a name="audit-log-updates"></a>Mises à jour du journal d’audit

Les journaux d’audit pour les événements d’accès du client d’étiquetage unifié sont désormais envoyés uniquement lorsque les utilisateurs ouvrent des fichiers étiquetés ou protégés, fournissant une indication plus claire de l’accès utilisateur.

Les types d’informations ne sont plus envoyés par [les journaux d’audit pour les événements d’accès](../audit-logs.md#access-audit-logs)et sont maintenant envoyés uniquement avec les [journaux d’audit pour les événements de découverte](../audit-logs.md#discover-audit-logs).

Pour plus d’informations, consultez [accéder aux journaux d’audit](../audit-logs.md#access-audit-logs).

Pour plus d’informations, consultez [Azure information protection référence du journal d’audit](../audit-logs.md).
### <a name="dke-template-based-labeling-updates"></a>Mises à jour de l’étiquetage basé sur un modèle DKE

Azure Information Protection prend désormais en charge l’étiquetage basé sur les modèles de chiffrement à clé double (DKE) dans le scanneur, ainsi que l’utilisation de l’Explorateur de fichiers et de PowerShell.

Pour plus d’informations, consultez :

- [Planification et implémentation de votre clé de locataire Azure Information Protection](../plan-implement-tenant-key.md)
- [Chiffrement à clé double](/microsoft-365/compliance/double-key-encryption) dans la documentation Microsoft 365

### <a name="azure-information-protection-scanner-fixed-issues-version-28850"></a>Azure Information Protection les problèmes résolus du scanneur, version 2.8.85.0

Les correctifs suivants ont été fournis dans la version 2.8.85.0 de l’Azure Information Protection scanneur d’étiquetage unifié :

- Améliorations de [l’analyse des fichiers avec des chemins d’accès longs](../deploy-aip-scanner-prereqs.md#file-path-requirements)
- Le scanneur AIP analyse désormais les environnements [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) complets lorsqu’il y a plusieurs ContentDatabases.
- Le scanneur AIP prend désormais en charge les fichiers [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) avec un point dans le chemin, mais aucune extension. Par exemple, un fichier avec un chemin d’accès `https://sharepoint.contoso.com/shared documents/meeting-notes` , sans extension, est maintenant analysé avec succès.
- Le scanneur AIP prend désormais en charge les [types d’informations sensibles personnalisés](../deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types) qui sont créés dans le centre de sécurité et conformité Microsoft et qui n’appartiennent à aucune stratégie.

### <a name="azure-information-protection-client-fixed-issues-version-28850"></a>Problèmes résolus par le client Azure Information Protection, version 2.8.85.0

Les correctifs suivants ont été fournis dans la version 2.8.85.0 du client d’étiquetage unifié de Azure Information Protection :

- Nouvelle indication avec narration pour tous les éléments actuellement sélectionnés dans le menu de l' ![icône des colonnes](../media/selected-sensitivity-options.png "icône colonnes") de **sensibilité** dans les applications Office. Pour plus d’informations, consultez la page sur les [étiquettes de sensibilité dans le Microsoft 365 docs](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do).
- Correctifs pour l’affichage des fichiers JPEG dans la [visionneuse AIP](clientv2-view-use-files.md)
- La rétrogradation d’une étiquette est maintenant automatiquement incluse **ProtectionOwnerBefore** dans les [événements d’audit](../audit-logs.md#downgrade-label-audit-logs)
- Les événements de modification incluent maintenant les **LastModifiedDate &** dans les [journaux d’audit](../audit-logs.md#change-protection-audit-logs)
- Ajout de la prise en charge des fichiers **proxy. PAC** lors de l’utilisation d’un proxy pour acquérir un jeton. Pour plus d’informations, consultez [Configuration requise pour les pare-feu et l’infrastructure réseau](../requirements.md#firewalls-and-network-infrastructure).
- Correctifs pour l’authentification lors de l' [actualisation des stratégies](../configure-policy.md#making-changes-to-the-policy)
- Correctifs pour les mises à jour [automatiques du marquage de contenu](../configure-policy-markings.md) pour PowerPoint en mode lecture seule
- Améliorations des fenêtres contextuelles et des textes d’erreur
- Info-bulle met à jour pour afficher la classification la plus élevée [des pièces jointes](../faqs-infoprotect.md#when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling), en tenant compte de la classification de l’e-mail et de la pièce jointe.
- Les correctifs **apportés au rapport constituent un** texte de problème lors de la modification des stratégies d’étiquetage de sensibilité à l’aide de l’applet [**de commande Set-LabelPolicy**](/powershell/module/exchange/set-labelpolicy)
- Corrige les erreurs affichées lorsque l’applet de commande [**Set-AipFileLabel**](/powershell/module/azureinformationprotection/set-aipfilelabel) est utilisée avec un ID d’étiquette non valide.
- Correctifs de performances pour le déchiffrement des messages SMIME dans le volet de lecture d’Outlook. Pour implémenter ce correctif, activez la propriété avancée [**OutlookSkipSmimeOnReadingPaneEnabled**](clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) .
- Correctifs pour le [déchiffrement des fichiers PST](clientv2-admin-guide-file-types.md) qui contiennent des fichiers chiffrés par mot de passe. Le déchiffrement des fichiers PST n’échoue plus si le fichier PST contient un fichier protégé par mot de passe.
- La suppression d’une étiquette de protection qui n’est pas incluse dans votre stratégie délimitée supprime désormais à la fois l’étiquette et la protection du contenu.

## <a name="version-271010"></a>Version 2.7.101.0

2.7.101.0 de la version du client et du scanneur d’étiquetage unifiée

**Publication** le 08/23/2020

**Pris en charge jusqu’à** 3/22/2021

**Correctif**:

Correction du problème pour les utilisateurs de PPT, d’Excel et de Word, ce qui a entraîné le blocage, le blocage ou l’obligation de répéter l’enregistrement qui était lié aux étiquettes obligatoires configurées avec la protection, le filigrane et/ou le marquage du contenu.

## <a name="version-27990"></a>Version 2.7.99.0

2.7.99.0 de la version du client et du scanneur d’étiquetage unifiée

**Publication** le 07/20/2020

**Pris en charge jusqu’à** 2/23/2021

**Correctifs et améliorations**:

Correction des problèmes dans les actions d’étiquetage des fichiers pour les nouveaux journaux d’audit des **étiquettes** .

Pour plus d’informations, consultez version 2.7.96.0 et [Azure information protection référence du journal d’audit (](../audit-logs.md) [préversion](#version-27960) publique).

## <a name="version-27960"></a>Version 2.7.96.0

2.7.96.0 de la version du client et du scanneur d’étiquetage unifiée

**Publication** le 06/29/2020

**Pris en charge jusqu’à** 1/20/2021

- [Nouvelles fonctionnalités pour le client d’étiquetage unifié, version 2.7.96.0](#new-features-for-the-unified-labeling-client-version-27960)
- [Nouvelles fonctionnalités pour le scanneur d’étiquetage unifié, version 2.7.96.0](#new-features-for-the-unified-labeling-scanner-version-27960)
- [Nouveaux journaux d’audit générés pour les fichiers supprimés](#new-audit-logs-generated-for-removed-files)
- [Application de TLS 1.2](#tls-12-enforcement)
- [Correctifs et améliorations, version 2.7.96.0](#fixes-and-improvements-version-27960)
### <a name="new-features-for-the-unified-labeling-scanner-version-27960"></a>Nouvelles fonctionnalités pour le scanneur d’étiquetage unifié, version 2.7.96.0

- [Utilisez le scanneur pour appliquer des étiquettes en fonction des conditions recommandées](../deploy-aip-scanner-prereqs.md). Les clients AIP peuvent désormais choisir d’implémenter l’étiquetage automatique côté service uniquement. Cette fonctionnalité permet aux utilisateurs d’AIP de suivre toujours les recommandations au lieu du scénario précédent, qui n’autorise que l’étiquetage automatique côté utilisateur.

- [Découvrez quels fichiers découverts précédemment par le moteur d’analyse ont été supprimés du référentiel analysé](../reports-aip.md) Ces fichiers supprimés n’ont pas été précédemment signalés dans AIP Analytics et sont désormais disponibles dans le rapport de découverte du scanneur.

- [Recevez des rapports du scanner sur les échecs pour appliquer des événements d’action](../reports-aip.md#friendly-schema-reference-for-event-functions). Utilisez les rapports pour en savoir plus sur les événements d’action ayant échoué et découvrir des moyens d’éviter les occurrences futures.

- Présentation de l’outil d’analyse de diagnostics du scanneur AIP pour la détection et l’analyse des erreurs courantes du scanneur. Pour commencer à utiliser les diagnostics du scanneur AIP, [Exécutez l’applet de commande **Start-AIPScannerDiagnostics**](../deploy-aip-scanner-tsg.md#troubleshooting-using-the-scanner-diagnostic-tool).

- Vous pouvez désormais gérer et limiter la consommation maximale de l’UC sur l’ordinateur du scanneur. Découvrez comment empêcher l’utilisation de l’UC de 100% et gérer l’utilisation de votre UC à l’aide de [deux nouveaux paramètres avancés **ScannerMaxCPU** et **ScannerMinCPU**](./clientv2-admin-guide-customizations.md#limit-cpu-consumption).

- Vous pouvez maintenant configurer le scanneur d’étiquetage unifié pour ignorer des fichiers spécifiques en fonction de leurs attributs de fichier. Définissez la liste des attributs de fichier qui déclenchent l’omission d’un fichier à l’aide du nouveau paramètre avancé **[ScannerFSAttributesToSkip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes)** .

### <a name="new-features-for-the-unified-labeling-client-version-27960"></a>Nouvelles fonctionnalités pour le client d’étiquetage unifié, version 2.7.96.0

- Les [**fenêtres contextuelles de justification**](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) s’affichent désormais pour les modifications apportées aux étiquettes par défaut dans le client d’étiquetage unifié.

- Intégration plus lisse avec les marquages de contenu visuel appliqués par Office. Pour plus d’informations sur la configuration des marquages de contenu dans le document Office, consultez [Comment configurer une étiquette pour les marquages visuels pour Azure information protection](../configure-policy-markings.md).

- La nouvelle propriété avancée **WordShapeNameToRemove** permet de supprimer le marquage de contenu dans les documents Word créés par des applications tierces. En savoir plus sur la façon d' [identifier les noms de formes existants et de les définir en vue de leur suppression à l’aide de **WordShapeNameToRemove**](./clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions).

- Prise en charge du **chiffrement à clé double (DKE)** (version préliminaire publique).

    Vous pouvez maintenant utiliser le client d’étiquetage unifié pour protéger du contenu très sensible tout en conservant le contrôle total de votre clé. DKE requiert deux clés pour accéder au contenu protégé : une clé est stockée dans Azure et l’autre clé est détenue par le client.

    Pour plus d’informations sur les clés de racine de locataire par défaut basées sur le Cloud, consultez [planification et implémentation de votre clé de locataire Azure information protection](../plan-implement-tenant-key.md). Pour plus d’informations sur l’implémentation du chiffrement à clé double, consultez [chiffrement à clé double](/microsoft-365/compliance/double-key-encryption) dans la documentation Microsoft 365.

### <a name="new-audit-logs-generated-for-removed-files"></a>Nouveaux journaux d’audit générés pour les fichiers supprimés

Les journaux d’audit sont désormais générés chaque fois que l’analyseur détecte qu’un fichier qui avait été analysé précédemment est maintenant supprimé.

Pour plus d’informations, consultez :

- [Fichiers journaux d’audit supprimés](../audit-logs.md#file-removed-audit-logs)
- [Rapports centraux d’Azure Information Protection](../reports-aip.md)

> [!IMPORTANT]
> Dans cette version, les actions d’étiquetage de fichier ne génèrent pas de nouveaux journaux d’audit **des étiquettes** .
> Si vous exécutez le scanneur dans **appliquer =** en mode, nous vous recommandons d’effectuer la mise à niveau vers la [version 2.7.99.0](#version-27990).
>

### <a name="tls-12-enforcement"></a>Application de TLS 1.2

À partir de cette version du client Azure Information Protection, seules les versions de TLS 1,2 ou ultérieures sont prises en charge.

Les clients qui ont une configuration TLS qui ne prend pas en charge TLS 1,2 doivent passer à un programme d’installation qui prend en charge TLS 1,2 pour utiliser des stratégies de Azure Information Protection, des jetons, des audits et des protections, et pour recevoir des communications basées sur Azure Information Protection.

Pour plus d’informations sur la configuration requise, consultez [firewalls and Network infrastructure Requirements](../requirements.md#firewalls-and-network-infrastructure).

### <a name="fixes-and-improvements-version-27960"></a>Correctifs et améliorations, version 2.7.96.0

- Améliorations de SQL pour le scanneur :
    - Performances
    - Fichiers avec un grand nombre de types d’informations

- Améliorations de l’analyse SharePoint pour :
    - Analyse des performances
    - Fichiers avec des caractères spéciaux dans le chemin d’accès
    - Bibliothèques avec grand nombre de fichiers

    Pour afficher un guide de démarrage rapide pour l’utilisation de Azure Information Protection avec SharePoint, voir [démarrage rapide : Rechercher les informations sensibles que vous avez dans les fichiers stockés localement](../quickstart-findsensitiveinfo.md).

- Notifications utilisateur améliorées pour les stratégies manquantes. Pour plus d’informations sur les stratégies d’étiquette pour le client d’étiquetage unifié, consultez que les stratégies de l’étiquette [peuvent faire](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do) dans la documentation Microsoft 365.

- Les [étiquettes automatiques](../configure-policy-classification.md) sont désormais appliquées dans Excel pour les scénarios où un utilisateur commence à fermer un fichier sans l’enregistrer, comme c’est le cas lorsqu’un utilisateur enregistre activement un fichier.

- Les en-têtes et les pieds de page sont supprimés comme prévu, et non lors de chaque enregistrement de document, lorsque le paramètre [ExternalContentMarkingToRemove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) est configuré.

- Les [variables utilisateur dynamiques](../configure-policy-markings.md#using-variables-in-the-text-string) sont désormais affichées dans les marquages visuels d’un document comme prévu.

- Problème où seule la première page du contenu d’un fichier PDF était utilisée pour l’application des règles de classification automatique est maintenant résolue, et la classification automatique basée sur tout le contenu du fichier PDF se déroule maintenant comme prévu. Pour plus d’informations sur la classification et l’étiquetage, consultez le [Forum aux questions sur la classification et l’étiquetage](../faqs-infoprotect.md).

- Lorsque plusieurs comptes Exchange sont configurés et que le client Azure Information Protection Outlook est activé, les messages électroniques sont envoyés à partir du compte secondaire comme prévu. Pour plus d’informations sur la configuration du client d’étiquetage unifié avec Outlook, consultez [configurer votre stratégie de groupe pour empêcher la désactivation d’AIP](reqs-ul-client.md#configure-your-group-policy-to-prevent-disabling-aip).

- Lorsqu’un document avec une étiquette de confidentialité plus élevée est glissé et déposé dans un message électronique, le message électronique reçoit désormais automatiquement l’étiquette de confidentialité la plus élevée comme prévu. Pour plus d’informations sur l’étiquetage des fonctionnalités clientes, consultez le [tableau comparatif des clients d’étiquetage](use-client.md#compare-the-labeling-solutions-for-windows-computers).

- Les autorisations personnalisées sont désormais appliquées aux courriers électroniques comme prévu, lorsque les adresses de messagerie incluent à la fois une apostrophe (') et un point (.) Pour plus d’informations sur la configuration du client d’étiquetage unifié avec Outlook, consultez [configurer votre stratégie de groupe pour empêcher la désactivation d’AIP](reqs-ul-client.md#configure-your-group-policy-to-prevent-disabling-aip).


- Par défaut, le propriétaire NTFS d’un fichier est perdu lorsque le fichier est étiqueté par le scanneur d’étiquetage unifié, PowerShell ou l’extension de l’Explorateur de fichiers. Vous pouvez maintenant configurer le système pour conserver le propriétaire NTFS du fichier en définissant le paramètre avancé New **[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** sur **true**.

    Le paramètre avancé **UseCopyAndPreserveNTFSOwner** nécessite une connexion réseau fiable et à faible latence entre le scanneur et le référentiel analysé.

## <a name="next-steps"></a>Étapes suivantes

Vous ne savez pas si l’étiquetage unifié est le bon client à installer ?  Consultez [choisir votre solution d’étiquetage Windows](use-client.md#choose-your-windows-labeling-solution).

Pour plus d’informations sur l’installation et l’utilisation du client d’étiquetage unifié :

- Pour les utilisateurs : [Télécharger et installer le client](install-unifiedlabelingclient-app.md)

- Pour les administrateurs : Azure Information Protection le Guide de l' [administrateur du client d’étiquetage unifié](clientv2-admin-guide.md)
