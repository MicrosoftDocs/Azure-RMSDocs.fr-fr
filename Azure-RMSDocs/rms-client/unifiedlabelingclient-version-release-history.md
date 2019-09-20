---
title: Azure Information Protection l’historique des versions du client d’étiquetage unifié-version & la stratégie de support
description: Consultez les informations de version pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/19/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8934e23594ba51248e691ce2e52d69308cb320e5
ms.sourcegitcommit: d5f046e34de0ad79b64d3f412999145b7d097e75
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71127551"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l’historique des versions et la stratégie de support du client d’étiquetage unifié

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Vous pouvez télécharger le client d’étiquetage unifié Azure Information Protection à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Après un bref délai de quelques semaines, la dernière version de la disponibilité générale est également incluse dans le catalogue Microsoft Update avec le nom de produit **Microsoft Azure information protection** > **Microsoft Azure informations Le client d’étiquetage unifié de protection**et la classification des **mises à jour**. Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [mise à niveau et maintenance du client d’étiquetage unifié Azure information protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version de disponibilité générale de la Azure Information Protection client d’étiquetage unifiée est prise en charge pendant six mois après la publication de la version GA suivante. La documentation n’inclut pas d’informations sur les versions non pris en charge du client. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les préversions ne doivent pas être déployées pour des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

> [!NOTE]
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

### <a name="release-information"></a>Informations de version

Utilisez les informations suivantes pour découvrir les nouveautés ou les modifications apportées à une version prise en charge de l’Azure Information Protection client d’étiquetage unifié pour Windows. La dernière version est répertoriée en première position. Le format de date utilisé sur cette page est *mois/jour/année*.

> [!NOTE]
> Les correctifs mineurs ne sont pas répertoriés. par conséquent, si vous rencontrez un problème avec le client d’étiquetage unifié, nous vous recommandons de vérifier s’il est corrigé avec la dernière version de la mise à la disposition générale. Si le problème persiste, vérifiez la version préliminaire actuelle (si disponible).
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

Ce client remplace le client Azure Information Protection (Classic). Pour comparer les fonctionnalités et les fonctionnalités avec le client classique, consultez [comparer les clients](use-client.md#compare-the-clients).

## <a name="versions-later-than-22210"></a>Versions ultérieures à 2.2.21.0

Si vous disposez d’une version 2 du client qui est ultérieure à 2.2.21.0, il s’agit d’une version préliminaire à des fins de test et d’évaluation.

**Date de publication** : 09/17/2019

**Nouvelles fonctionnalités :**

- Prise en charge du [scanneur](../deploy-aip-scanner.md), pour inspecter et étiqueter les documents des magasins de données locaux. Avec cette version du scanneur :
    
    - Plusieurs scanneurs peuvent partager la même SQL Server base de données lorsque vous configurez les scanneurs pour qu’ils utilisent le même profil de scanneur. Cette configuration facilite la gestion de plusieurs scanneurs et entraîne des temps d’analyse plus rapides. Lorsque vous utilisez cette configuration, attendez toujours que l’installation d’un scanneur soit terminée avant d’installer un autre scanneur avec le même profil.
    
    - Vous devez spécifier un profil lorsque vous installez le scanneur et que la base de données du scanneur est nommée **\<AIPScannerUL_ profile_name >** . Le paramètre de *Profil* est également obligatoire pour Set-AIPScanner.
    
    - Vous pouvez définir une étiquette par défaut pour tous les documents, même si les documents sont déjà étiquetés. Dans les paramètres Profil du scanneur ou référentiel, affectez à l’option **Renommer les fichiers** la valeur **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée.
    
    - Vous pouvez supprimer des étiquettes existantes de tous les documents. cette action comprend la suppression de la protection si elle a été appliquée précédemment par une étiquette. La protection appliquée indépendamment d’une étiquette est conservée. Cette configuration de scanneur est effectuée dans les paramètres de profil du scanneur ou de référentiel avec les paramètres suivants :
        - **Label files based on content** (Étiqueter les fichiers en fonction du contenu) : **Off**
        - **Étiquette par défaut** : **Aucune.**
        - **Relabel files** (Réétiqueter les fichiers) : **Activé** avec la case à cocher **appliquer l’étiquette par défaut** sélectionnée
    
    - Comme avec le scanneur du client classique, le scanneur protège les fichiers Office et les fichiers PDF. Actuellement, vous ne pouvez pas configurer d’autres types de fichiers à protéger par cette version du scanneur.
    
    - Problème connu : Les étiquettes nouvelles et renommées ne peuvent pas être sélectionnées en tant qu’étiquette par défaut pour le profil du scanneur ou les paramètres du référentiel. Contournement
        - Pour les nouvelles étiquettes : Dans la Portail Azure, [Ajoutez l’étiquette](../configure-policy-add-remove-label.md) que vous souhaitez utiliser à la stratégie globale ou à une stratégie délimitée.
        - Pour les étiquettes renommées : Dans le portail Azure, accédez à **Azure information protection** > **gérer** > l'**étiquetage unifié**, puis sélectionnez **publier**.
    
    Vous pouvez mettre à niveau les analyseurs à partir du client Azure Information Protection (Classic). Après la mise à niveau, qui crée une base de données, le moteur de base de données analyse à nouveau tous les fichiers lors de sa première exécution. Pour obtenir des instructions, consultez [mise à niveau de l’analyseur de Azure information protection](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner) à partir du Guide de l’administrateur.
    
    Pour plus d’informations, consultez l’annonce du billet de blog : [La version préliminaire du scanneur AIP d’étiquetage unifiée offre une montée en charge horizontale et bien plus encore.](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)

- L’applet de commande PowerShell [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) a de nouveaux paramètres lorsque vous souhaitez [étiqueter des fichiers de manière non interactive](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection), et une [nouvelle procédure pour inscrire une application dans Azure ad](clientv2-admin-guide-powershell.md#to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication---preview-client). Les exemples de scénarios incluent le scanneur et les scripts PowerShell automatisés pour étiqueter les documents.

- Les types d’informations sensibles personnalisés correspondants sont envoyés à [Azure information protection Analytics](../reports-aip.md).

- L’étiquette appliquée affiche la couleur configurée pour l’étiquette, si une [couleur a été configurée](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).

- Lorsque vous ajoutez ou modifiez des paramètres de protection sur une étiquette, le client réapplique l’étiquette avec ces derniers paramètres de protection lors de l’enregistrement du document suivant. De même, le scanneur réapplique l’étiquette avec ces derniers paramètres de protection lors de la prochaine analyse du document en mode d’application.

- New cmdlet, [Export-AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs), pour rassembler tous les fichiers journaux de%LocalAppData%\Microsoft\MSIP\Logs et les enregistre dans un fichier unique et compressé avec un format. zip. Ce fichier peut ensuite être envoyé à Support Microsoft si vous êtes invité à envoyer des fichiers journaux pour vous aider à examiner un problème signalé.

**Céder**

- Vous pouvez apporter des modifications à un fichier protégé à l’aide de l’Explorateur de fichiers et cliquer avec le bouton droit après avoir supprimé un mot de passe pour le fichier.


## <a name="version-22210"></a>Version 2.2.21.0

**Date de publication** : 09/03/2019

**Céder**

- Quand vous utilisez le paramètre avancé [OutlookDefaultLabel](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook) pour définir une autre étiquette par défaut pour Outlook, et que l’étiquette que vous spécifiez n’a pas de sous-étiquettes pour la stratégie d’étiquette, l’étiquette est correctement appliquée.

- Lorsque le client Azure Information Protection est utilisé dans une application Office, un utilisateur avec un compte Active Directory qui n’est pas configuré pour l’authentification unique est invité à s’authentifier pour Azure Information Protection. Une fois l’authentification réussie, l’état du client passe correctement à en ligne, ce qui permet la fonctionnalité d’étiquetage.

## <a name="version-22190"></a>Version 2.2.19.0

**Date de publication** : 08/06/2019

Pris en charge jusqu’à 03/03/2020

**Céder**

- Le client peut télécharger sa stratégie et afficher les étiquettes de sensibilité actuelles. Ce correctif est nécessaire après la mise à niveau à partir d’une version précédente et vous n’avez pas configuré de types d’informations personnalisées dans votre centre d’étiquetage.

- Améliorations générales des performances et de la stabilité.

## <a name="version-22140"></a>Version 2.2.14.0

**Date de publication** : 07/15/2019

Pris en charge jusqu’à 02/06/2020

**Nouvelles fonctionnalités :**

- Prise en charge des [Paramètres avancés](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous configurez avec PowerShell pour le centre de sécurité et de conformité.
    
    Ces paramètres avancés prennent en charge les personnalisations suivantes:
     - [Afficher la barre Information Protection dans les applications Office](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [Exempter les messages Outlook de l’étiquetage obligatoire](clientv2-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)
    - [Activer la classification recommandée dans Outlook](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [Définir une autre étiquette par défaut pour Outlook](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [Supprimer « Pas maintenant » pour les documents quand l’étiquetage obligatoire est utilisé](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées pour les utilisateurs dans l’Explorateur de fichiers](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [Ajouter « Signaler un problème » pour les utilisateurs](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [Désactiver l’envoi d’informations sensibles découvertes dans des documents à Azure Information Protection Analytics](clientv2-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)
    - [Désactiver l’envoi de correspondances de types d’informations pour un sous-ensemble d’utilisateurs](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [Appliquer une propriété personnalisée lorsqu’une étiquette est appliquée](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Spécifier une sous-étiquette par défaut pour une étiquette parent](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Spécifier une couleur pour l’étiquette](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Prise en charge des étiquettes configurées pour des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers. Pour plus d’informations, consultez la section [autoriser les utilisateurs à attribuer des autorisations](/Office365/SecurityCompliance/encryption-sensitivity-labels#let-users-assign-permissions) dans la documentation Office.

- Modifications de PowerShell dans le module AzureInformationProtection:
    - Nouvelle applet de commande: [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -remplace New-RMSProtectionLicense pour créer une stratégie ad hoc pour les autorisations personnalisées
    - Nouveaux paramètres:
        -  *CustomPermissions* et *RemoveProtection* -ajouté à [Set-AIPFileLabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf* -ajouté à [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), à utiliser à la place du paramètre *Token* pour les sessions non interactives
        -  *WhatIf* et *DiscoveryInfoTypes* -ajoutés à [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), afin que cette applet de commande puisse s’exécuter en mode détection sans appliquer d’étiquettes
    - Applets de commande déconseillées qui se connectent directement à un service de protection: Clear-RMSAuthentication, Set-RMSFileStatus, Set-RMSServer, Set-RMSServerAuthentication, obtient-RMSTemplate, Protect-RMSFile, Set-RMSServerAuthentication, Unprotect-RMSFile


**Céder**

- Prise en charge des correspondances de [contenu](../reports-aip.md#content-matches-for-deeper-analysis) pour Analytics et [Set-AIPFileClassification](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipfileclassification?view=azureipps) avec le paramètre *DiscoveryInfoTypes* .

- Après avoir modifié les paramètres régionaux de remplacement dans Windows, vous pouvez toujours appliquer une étiquette avec protection à un document PDF.

- Lorsqu’une étiquette est supprimée du contenu, la protection est également supprimée uniquement lorsqu’elle a été appliquée dans le cadre de la configuration de l’étiquette. Si la protection a été appliquée indépendamment de l’étiquette, cette protection est conservée. Par exemple, un utilisateur a appliqué des autorisations personnalisées à un fichier.

- Lorsque l’étiquetage automatique est configuré, l’étiquette s’applique la première fois qu’un document est enregistré.

- L’étiquetage par défaut prend en charge les sous-étiquettes.

## <a name="version-207790"></a>Version 2.0.779.0

**Date de publication** : 05/01/2019

Pris en charge jusqu’à 02/15/2020

Cette version offre un correctif unique pour résoudre un problème de condition de course dans le cas où il peut arriver que des étiquettes ne s’affichent pas dans les applications Office ou l’Explorateur de fichiers.

## <a name="version-207780"></a>Version 2.0.778.0

**Date de publication** : 04/16/2019

Pris en charge jusqu’à 11/01/2019

Cette première version de disponibilité générale du client d’étiquetage unifié Azure Information Protection pour Windows prend en charge les fonctionnalités suivantes: 

- Mise à niveau à partir du client Azure Information Protection.

- Étiquetage manuel, automatique et recommandé : Pour plus d’informations sur la configuration de l’étiquetage automatique et de l’étiquetage recommandé pour ce client, voir [Appliquer automatiquement une étiquette de confidentialité au contenu](/Office365/SecurityCompliance/apply-sensitivity-label-automatically).

- Dans l’Explorateur de fichiers, actions déclenchées par clic droit pour classifier et protéger des fichiers, supprimer la protection et appliquer des autorisations personnalisées.

- Visionneuse pour les fichiers texte et image protégés, les fichiers PDF protégés ainsi que les fichiers faisant l’objet d’une protection générique.

- Commandes PowerShell pour effectuer les actions suivantes :
    - [Définir ou supprimer une étiquette dans un document](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [Étiqueter un document après en avoir examiné le contenu](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [Lire les informations d’étiquette appliquées à un document](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [S’authentifier pour prendre en charge les sessions PowerShell sans assistance](/powershell/module/azureinformationprotection/set-aipauthentication)

- Audit des données et prise en charge de la découverte des points de terminaison pour la création de rapports centralisée à l’aide d' [Azure information protection Analytics](../reports-aip.md)

- Paramètres d’étiquette et de stratégie suivants :
    - Marquage visuel (en-têtes, pieds de page, filigranes)
    - Étiquetage par défaut-actuellement limité aux étiquettes sans sous-étiquettes
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

Pour plus d’informations sur l’installation et l’utilisation de ce client: 

- Pour les utilisateurs : [Télécharger et installer le client](install-unifiedlabelingclient-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client d’étiquetage unifié Azure Information Protection](clientv2-admin-guide.md)

