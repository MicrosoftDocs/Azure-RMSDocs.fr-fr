---
title: Azure Information Protection unifiée étiquetage client - stratégie de prise en charge et d’historique de Version
description: Consultez les informations de version pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 6f359c304080918713cee52667a1bedeb7b4ae07
ms.sourcegitcommit: 9628dcd88abde32f612896195f8d3d9a2c1d87bf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67398745"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection unifiée l’étiquetage client - Version historique des versions et politique de support

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Vous pouvez télécharger le client étiquetage unifié d’Azure Information Protection à partir de la [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Après un court délai de quelques semaines en général, la version plus récente de disponibilité générale est également incluse dans le catalogue Microsoft Update avec un nom de produit de **Microsoft Azure Information Protection**  >  **Microsoft Client Azure Information Protection unifiée l’étiquetage**et la classification de **mises à jour**. Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [étiquetage client unifié, la mise à niveau et la maintenance d’Azure Information Protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version de disponibilité générale (GA) du client Azure Information Protection unifiée étiquetage est prise en charge jusqu'à six mois après la publication de la version GA suivante. La documentation n’inclut pas d’informations sur les versions non pris en charge du client. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les préversions ne doivent pas être déployées pour des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

> [!NOTE]
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

### <a name="release-information"></a>Informations de version

Utilisez les informations suivantes pour voir ce qui est pris en charge pour la version disponibilité générale du client Azure Information Protection unifiée étiquetage.

Ce client installe un module complémentaire Office pour les ordinateurs Windows, une extension pour l’Explorateur de fichiers et un module PowerShell. Ce client a les mêmes [prérequis](../requirements.md) que le client Azure Information Protection qui télécharge une stratégie à partir d’Azure.

Pour comparer les fonctions et fonctionnalités avec le client Azure Information Protection, consultez [comparer les clients](use-client.md#compare-the-clients).

## <a name="versions-later-than-207790"></a>Versions postérieures à 2.0.779.0

**Date de publication** : 06/20/2019

Si vous avez une version 2 du client qui est ultérieure à 2.0.779.0, il est une version d’évaluation à des fins de test et d’évaluation. 

**Nouvelles fonctionnalités :**

- Prise en charge de [paramètres avancés](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous configurez avec PowerShell pour le centre sécurité et conformité.
    
    Ces paramètres avancés prennent en charge les personnalisations suivantes :
     - [Afficher la barre Information Protection dans les applications Office](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [Activer la classification recommandée dans Outlook](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [Définir une autre étiquette par défaut pour Outlook](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [Supprimer « Pas maintenant » pour les documents quand l’étiquetage obligatoire est utilisé](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées pour les utilisateurs dans l’Explorateur de fichiers](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [Ajouter « Signaler un problème » pour les utilisateurs](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [Désactiver l’envoi des informations sensibles découvertes dans les documents à l’analytique d’Azure Information Protection](clientv2-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)
    - [Désactiver l’envoi de correspondances de types d’informations pour un sous-ensemble d’utilisateurs](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [Appliquer une propriété personnalisée, quand une étiquette est appliquée.](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Spécifier une sous-étiquette par défaut pour une étiquette parent](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Spécifiez une couleur pour l’étiquette](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Prise en charge pour les étiquettes qui sont configurés pour les autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers :
    - Si vous avez des étiquettes avec cette configuration à partir du portail Azure, ils sont désormais pris en charge par le client d’étiquetage unifié bien qu’il n’existe actuellement aucune configuration équivalente dans les centres d’administration.
    - Lorsqu’un utilisateur sélectionne une étiquette avec cette configuration, ils sont invités à sélectionner les utilisateurs et les paramètres de protection pour le document.

- Modifications de PowerShell dans le module AzureInformationProtection :
    - Nouvelle applet de commande : [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -remplace RMSProtectionLicense de nouveau pour créer une stratégie ad hoc des autorisations personnalisées
    - Nouveaux paramètres :
        -  *CustomPermissions* et *RemoveProtection* - ajouté à [Set-AIPFileLabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf* - ajouté au [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), pour être utilisé au lieu du *jeton* paramètre pour les sessions non interactives
        -  *WhatIf* et *DiscoveryInfoTypes* - ajouté au [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), de sorte que cette applet de commande peut exécuter en mode découverte sans appliquer les étiquettes
    - Applets de commande déconseillées : Clear-RMSAuthentication, Get-RMSFileStatus, Get-RMSServer, Get-RMSServerAuthentication, Get-RMSTemplate, protéger-RMSFile, Set-RMSServerAuthentication, RMSFile ôter la protection


**Correctifs :**

- Lorsque l’étiquetage automatique est configurée, l’étiquette s’applique à la première fois qu’un document est enregistré.

- Par défaut les sous-étiquettes prend en charge l’étiquetage.

## <a name="version-207790"></a>Version 2.0.779.0

**Date de publication** : 05/01/2019

Cette version comporte un seul correctif pour résoudre une condition de concurrence où, aucune étiquette n’affiche parfois dans les applications Office ou de l’Explorateur de fichiers.

## <a name="version-207780"></a>Version 2.0.778.0

**Date de publication** : 04/16/2019

Prise en charge via le 01/11/2019

Cette première version de disponibilité générale du client étiquetage unifiée Azure Information Protection pour Windows prend en charge les fonctionnalités suivantes : 

- Mise à niveau à partir du client Azure Information Protection.

- Étiquetage manuel, automatique et recommandé : Pour plus d’informations sur la configuration de l’étiquetage automatique et de l’étiquetage recommandé pour ce client, voir [Appliquer automatiquement une étiquette de confidentialité au contenu](/Office365/SecurityCompliance/apply_sensitivity_label_automatically).

- Dans l’Explorateur de fichiers, actions déclenchées par clic droit pour classifier et protéger des fichiers, supprimer la protection et appliquer des autorisations personnalisées.

- Visionneuse pour les fichiers texte et image protégés, les fichiers PDF protégés ainsi que les fichiers faisant l’objet d’une protection générique.

- Commandes PowerShell pour effectuer les actions suivantes :
    - [Définir ou supprimer une étiquette dans un document](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [Étiqueter un document après en avoir examiné le contenu](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [Lire les informations d’étiquette appliquées à un document](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [S’authentifier pour prendre en charge les sessions PowerShell sans assistance](/powershell/module/azureinformationprotection/set-aipauthentication)

- L’audit des données et point de terminaison discovery prennent en charge pour les rapports centrale à l’aide de [analytique d’Azure Information Protection](../reports-aip.md).

- Paramètres d’étiquette et de stratégie suivants :
    - Marquage visuel (en-têtes, pieds de page, filigranes)
    - Par défaut l’étiquetage - actuellement limité aux étiquettes sans les sous-étiquettes
    - Étiquettes qui appliquent Ne pas transférer et s’affichent uniquement dans Outlook
    - Invites de justification si les utilisateurs baissent le niveau de classification ou suppriment une étiquette
    - Couleurs des étiquettes

- Actualisation de la stratégie à partir des centres d’administration :
    - à chaque démarrage d’une application Office et toutes les 4 heures ;
    - lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier ;
    - lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection.

- Boîte de dialogue Aide et commentaires, qui inclut des paramètres de réinitialisation et des journaux d’exportation.


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez les [tableaux de comparaison](use-client.md#compare-the-clients).

Pour plus d’informations sur l’installation et à l’aide de ce client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-unifiedlabelingclient-app.md)

- Pour les administrateurs : [Azure Information Protection unifiée étiquetage guide de l’administrateur client](clientv2-admin-guide.md)

