---
title: Azure Information Protection l’historique des versions du client d’étiquetage unifié-version & la stratégie de support
description: Consultez les informations de version pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 32d0ac2669e0cc304d0f06c603f64d623c216c68
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117593"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection l’historique des versions et la stratégie de support du client d’étiquetage unifié

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Vous pouvez télécharger le client d’étiquetage unifié Azure Information Protection à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Après un bref délai de quelques semaines, la dernière version de la disponibilité générale est également incluse dans le catalogue Microsoft Update avec le nom de produit **Microsoft Azure Information Protection** > **Microsoft Azure information protection client d’étiquetage unifié**et la classification des **mises à jour**. Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [mise à niveau et maintenance du client d’étiquetage unifié Azure information protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version de disponibilité générale de la Azure Information Protection client d’étiquetage unifiée est prise en charge pendant six mois après la publication de la version GA suivante. La documentation n’inclut pas d’informations sur les versions non pris en charge du client. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les versions préliminaires ne doivent pas être déployées auprès des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions de la disponibilité générale qui ne sont plus prises en charge :

|Version du client|Date de publication|
|--------------|-------------|
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

## <a name="version-261010"></a>Version 2.6.101.0

**Publication** le 1/15/2020

**Nouvelles fonctionnalités :**

- La modification de l’applet de commande [PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell) **Set-AIPFileLabel** pour permettre la suppression de la protection des fichiers PST, rar, 7zip et MSG. 

- Ajout de la possibilité pour les administrateurs de Azure Information Protection de contrôler le moment où les extensions pfile sont utilisées pour les fichiers. En savoir plus sur la [modification des types de fichiers protégés](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#change-which-file-types-to-protect). 

- Prise en charge du marquage visuel dynamique ajoutée pour les applications et les variables. En savoir plus sur la [Configuration des étiquettes pour les marquages visuels](https://docs.microsoft.com/azure/information-protection/configure-policy-markings). 

- Améliorations apportées à [des conseils de stratégie personnalisables pour les étiquettes automatiques et recommandées](use-client.md).   

- Prise en charge ajoutée pour la [fonctionnalité d’étiquetage hors connexion](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#support-for-disconnected-computers) avec les applications Office dans le client d’étiquetage unifié.

- La nouvelle propriété avancée **WordShapeNameToRemove** permet de supprimer le marquage de contenu dans les documents Word créés par des applications tierces. En savoir plus sur la façon d' [identifier les noms de formes existants et de les définir en vue de leur suppression à l’aide de **WordShapeNameToRemove**](https://docs.microsoft.com/azure/information-protection/clientv2-admin-guide-customizations#remove-headers-and-footers-from-other-labeling-solutions). 

- Fonctionnalités liées au [scanneur](../deploy-aip-scanner.md) :
    - [Simplification de la découverte des sous-sites et SharePoint locaux](https://docs.microsoft.com/azure/information-protection/quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories). La définition de chaque site spécifique n’est plus nécessaire. 
    - Propriété avancée pour le [dimensionnement du segment SQL](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#storage-requirements-and-capacity-planning-for-sql-server) ajouté.
    - Les administrateurs ont désormais la possibilité d' [arrêter des analyses existantes et d’effectuer une nouvelle analyse](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#stop-a-scan) si une modification a été apportée à l’étiquette par défaut.
    - Par défaut, l’analyseur définit maintenant une télémétrie minimale pour des analyses plus rapides et une taille de journal réduite et les types d’informations sont maintenant mis en cache dans la base de données. En savoir plus sur l' [optimisation du scanneur](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#optimizing-the-performance-of-the-scanner). 

**Correctifs :**

- Le scanneur prend désormais en charge des déploiements distincts pour la base de données et le service, tandis que les droits **sysadmin** sont nécessaires uniquement pour le déploiement de base de données. 
- Dans les cas où les utilisateurs ont tenté sans succès d’ouvrir des fichiers TIFF protégés et des fichiers TIFF créés par RightFax, les fichiers TIFF s’ouvrent et restent stables comme prévu.  
- Les endommagements précédents des fichiers txt et PDF protégés sont résolus.
- Une étiquette incohérente entre les Log Analytics **automatique** et **manuelle** a été corrigée. 
- Des problèmes d’héritage inattendus identifiés entre les nouveaux e-mails et le dernier e-mail ouvert d’un utilisateur sont désormais résolus.  
- La protection des fichiers. msg en tant que. msg. fichiers pfile fonctionne à présent comme prévu. 
- Les autorisations de copropriétaire ajoutées à partir des paramètres définis par l’utilisateur Office sont désormais appliquées comme prévu. 
- Lorsque vous entrez des autorisations de mise à niveau vers la version antérieure, le texte ne peut plus être entré lorsque d’autres options sont déjà sélectionnées. 


## <a name="version-25330"></a>Version 2.5.33.0

**Publication**: 10/23/2019

**Nouvelles fonctionnalités :**

- Version préliminaire du [scanneur](../deploy-aip-scanner.md), pour inspecter et étiqueter les documents des magasins de données locaux. Avec cette version du scanneur :
    
    - Plusieurs scanneurs peuvent partager la même SQL Server base de données lorsque vous configurez les scanneurs pour qu’ils utilisent le même profil de scanneur. Cette configuration facilite la gestion de plusieurs scanneurs et entraîne des temps d’analyse plus rapides. Lorsque vous utilisez cette configuration, attendez toujours que l’installation d’un scanneur soit terminée avant d’installer un autre scanneur avec le même profil.
    
    - Vous devez spécifier un profil lorsque vous installez le scanneur et que la base de données du scanneur s’intitule **AIPScannerUL_\<profile_name >** . Le paramètre de *Profil* est également obligatoire pour Set-AIPScanner.
    
    - Vous pouvez définir une étiquette par défaut pour tous les documents, même si les documents sont déjà étiquetés. Dans les paramètres Profil du scanneur ou référentiel, affectez à l’option **Renommer les fichiers** la valeur **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée.
    
    - Vous pouvez supprimer des étiquettes existantes de tous les documents. cette action comprend la suppression de la protection si elle a été appliquée précédemment par une étiquette. La protection appliquée indépendamment d’une étiquette est conservée. Cette configuration de scanneur est effectuée dans les paramètres de profil du scanneur ou de référentiel avec les paramètres suivants :
        - **Étiqueter les fichiers en fonction du contenu**: **désactivé**
        - **Étiquette par défaut**: **aucune**
        - **Renommer les fichiers**: **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée
    
    - Comme avec le scanneur du client classique, par défaut, le scanneur protège les fichiers Office et les fichiers PDF. Vous pouvez protéger d’autres types de fichiers lorsque vous utilisez un [paramètre avancé PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).
    
    - Les ID d’événement pour les cycles de scanneur en début et en fin ne sont pas écrits dans le journal des événements Windows. Utilisez plutôt le Portail Azure pour ces informations.
    
    - Problème connu : les étiquettes nouvelles et renommées ne peuvent pas être sélectionnées en tant qu’étiquette par défaut pour les paramètres de profil de scanneur ou de référentiel. Solutions :
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

- [Réinitialiser les paramètres](clientv2-admin-guide.md#more-information-about-the-reset-settings-option) supprime maintenant les dossiers%LocalAppData%\Microsoft\MSIP\mip\\ *\<processname. exe\>* au lieu du dossier%LocalAppData%\Microsoft\MSIP\mip\\ *\<ProcessName\>* \mip.

- L' [AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) d’accès à la sécurité comprend désormais l’ID de contenu d’un document protégé.

## <a name="version-22210"></a>Version 2.2.21.0

**Publication**: 09/03/2019

Pris en charge jusqu’à 04/23/2020

**Correctifs :**

- Quand vous utilisez le paramètre avancé [OutlookDefaultLabel](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook) pour définir une autre étiquette par défaut pour Outlook, et que l’étiquette que vous spécifiez n’a pas de sous-étiquettes pour la stratégie d’étiquette, l’étiquette est correctement appliquée.

- Lorsque le client Azure Information Protection est utilisé dans une application Office, un utilisateur avec un compte Active Directory qui n’est pas configuré pour l’authentification unique est invité à s’authentifier pour Azure Information Protection. Une fois l’authentification réussie, l’état du client passe correctement à en ligne, ce qui permet la fonctionnalité d’étiquetage.

## <a name="version-22190"></a>Version 2.2.19.0

**Publication**: 08/06/2019

Pris en charge jusqu’à 03/03/2020

**Correctifs :**

- Le client peut télécharger sa stratégie et afficher les étiquettes de sensibilité actuelles. Ce correctif est nécessaire après la mise à niveau à partir d’une version précédente et vous n’avez pas configuré de types d’informations personnalisées dans votre centre d’étiquetage.

- Améliorations générales des performances et de la stabilité.

## <a name="version-22140"></a>Version 2.2.14.0

**Publication**: 07/15/2019

Pris en charge jusqu’à 02/06/2020

**Nouvelles fonctionnalités :**

- Prise en charge des [Paramètres avancés](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous configurez avec PowerShell pour le centre de sécurité et de conformité.
    
    Ces paramètres avancés prennent en charge les personnalisations suivantes :
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
    - [Envoyer les correspondances de type d’informations à Azure Information Protection Analytics](clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics)
    - [Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [Appliquer une propriété personnalisée lorsqu’une étiquette est appliquée](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Spécifier une sous-étiquette par défaut pour une étiquette parent](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Spécifier une couleur pour l’étiquette](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Prise en charge des étiquettes configurées pour des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers. Pour plus d’informations, consultez la section [autoriser les utilisateurs à attribuer des autorisations](/microsoft-365/compliance/encryption-sensitivity-labels#let-users-assign-permissions) dans la documentation Office.

- Modifications de PowerShell dans le module AzureInformationProtection :
    - Nouvelle applet de commande : [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -remplace New-RMSProtectionLicense pour créer une stratégie ad hoc pour les autorisations personnalisées
    - Nouveaux paramètres :
        -  *CustomPermissions* et *RemoveProtection* -ajouté à [Set-AIPFileLabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf* -ajouté à [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), à utiliser à la place du paramètre *Token* pour les sessions non interactives
        -  *WhatIf* et *DiscoveryInfoTypes* -ajoutés à [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), afin que cette applet de commande puisse s’exécuter en mode détection sans appliquer d’étiquettes
    - Applets de commande déconseillées qui se connectent directement à un service de protection : Clear-RMSAuthentication, Set-RMSFileStatus, Set-RMSServer, obtenir-RMSServerAuthentication, obtenir-RMSTemplate, Protect-RMSFile, Set-RMSServerAuthentication, Unprotect-RMSFile


**Correctifs :**

- Prise en charge des [correspondances de contenu](../reports-aip.md#content-matches-for-deeper-analysis) pour Analytics et [Set-AIPFileClassification](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipfileclassification?view=azureipps) avec le paramètre *DiscoveryInfoTypes* .

- Après avoir modifié les paramètres régionaux de remplacement dans Windows, vous pouvez toujours appliquer une étiquette avec protection à un document PDF.

- Lorsqu’une étiquette est supprimée du contenu, la protection est également supprimée uniquement lorsqu’elle a été appliquée dans le cadre de la configuration de l’étiquette. Si la protection a été appliquée indépendamment de l’étiquette, cette protection est conservée. Par exemple, un utilisateur a appliqué des autorisations personnalisées à un fichier.

- Lorsque l’étiquetage automatique est configuré, l’étiquette s’applique la première fois qu’un document est enregistré.

- L’étiquetage par défaut prend en charge les sous-étiquettes.

## <a name="next-steps"></a>Étapes suivantes

Vous ne savez pas s’il s’agit du bon client à installer ?  Consultez [choisir le client d’étiquetage à utiliser pour les ordinateurs Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Pour plus d’informations sur l’installation et l’utilisation de ce client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-unifiedlabelingclient-app.md)

- Pour les administrateurs : Azure Information Protection le Guide de l' [administrateur du client d’étiquetage unifié](clientv2-admin-guide.md)

