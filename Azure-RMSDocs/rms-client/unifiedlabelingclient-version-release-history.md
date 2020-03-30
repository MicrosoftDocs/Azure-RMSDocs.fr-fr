---
title: Azure Information Protection l’historique des versions du client d’étiquetage unifié-version & la stratégie de support
description: Consultez les informations de version pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9db865f64e2780d680a05cc8deae873b8cc975ea
ms.sourcegitcommit: 1ade392edac5842adb14996012efb6e605c39d8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80382048"
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

Les préversions ne doivent pas être déployées pour des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions de la disponibilité générale qui ne sont plus prises en charge :

|Version du client|Date de publication|
|--------------|-------------|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|

Le format de date utilisé sur cette page est *mois/jour/année*.


### <a name="release-information"></a>Informations de version

Utilisez les informations suivantes pour découvrir les nouveautés ou les modifications apportées à une version prise en charge de l’Azure Information Protection client d’étiquetage unifié pour Windows. La dernière version est la première sur la liste. Le format de date utilisé sur cette page est *mois/jour/année*.

> [!NOTE]
> Les correctifs mineurs ne sont pas répertoriés. par conséquent, si vous rencontrez un problème avec le client d’étiquetage unifié, nous vous recommandons de vérifier s’il est corrigé avec la dernière version de la mise à la disposition générale. Si le problème persiste, vérifiez la version préliminaire actuelle (si disponible).
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

Ce client remplace le client Azure Information Protection (Classic). Pour comparer les fonctionnalités et les fonctionnalités avec le client Classic, consultez [comparer les clients d’étiquetage pour les ordinateurs Windows](use-client.md#compare-the-labeling-clients-for-windows-computers).

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


**Céder**

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
    
    - Vous devez spécifier un profil lorsque vous installez le scanneur et que la base de données du scanneur s’intitule **AIPScannerUL_\<profile_name >** . Le paramètre de *Profil* est également obligatoire pour Set-AIPScanner.
    
    - Vous pouvez définir une étiquette par défaut pour tous les documents, même si les documents sont déjà étiquetés. Dans les paramètres Profil du scanneur ou référentiel, affectez à l’option **Renommer les fichiers** la valeur **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée.
    
    - Vous pouvez supprimer des étiquettes existantes de tous les documents. cette action comprend la suppression de la protection si elle a été appliquée précédemment par une étiquette. La protection appliquée indépendamment d’une étiquette est conservée. Cette configuration de scanneur est effectuée dans les paramètres de profil du scanneur ou de référentiel avec les paramètres suivants :
        - **Étiqueter les fichiers en fonction du contenu**: **désactivé**
        - **Étiquette par défaut**: **aucune**
        - **Renommer les fichiers**: **activé** avec la case à cocher **appliquer l’étiquette par défaut** activée
    
    - Comme avec le scanneur du client classique, par défaut, le scanneur protège les fichiers Office et les fichiers PDF. Vous pouvez protéger d’autres types de fichiers lorsque vous utilisez un [paramètre avancé PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).
    
    - Les ID d’événement pour les cycles de scanneur en début et en fin ne sont pas écrits dans le journal des événements Windows. Utilisez plutôt le Portail Azure pour ces informations.
    
    - Problème connu : les étiquettes nouvelles et renommées ne peuvent pas être sélectionnées en tant qu’étiquette par défaut pour les paramètres de profil de scanneur ou de référentiel. Solutions de contournement :
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

**Céder**

- Vous pouvez apporter des modifications à un fichier protégé à l’aide de l’Explorateur de fichiers et cliquer avec le bouton droit après avoir supprimé un mot de passe pour le fichier.

- Vous pouvez ouvrir des fichiers protégés en mode natif dans la visionneuse sans avoir à [utiliser le droit](../configure-usage-rights.md#usage-rights-and-descriptions)enregistrer sous, exporter (exporter).

- Les étiquettes et les paramètres de stratégie sont actualisés comme prévu sans devoir exécuter [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication?)ou supprimer manuellement le dossier%localappdata%\Microsoft\MSIP\mip.

**Modifications supplémentaires**

- [Réinitialiser les paramètres](clientv2-admin-guide.md#more-information-about-the-reset-settings-option) supprime maintenant les dossiers%LocalAppData%\Microsoft\MSIP\mip\\ *\<processname. exe\>* au lieu du dossier%LocalAppData%\Microsoft\MSIP\mip\\ *\<ProcessName\>* \mip.

- L' [AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) d’accès à la sécurité comprend désormais l’ID de contenu d’un document protégé.

## <a name="version-22210"></a>Version 2.2.21.0

**Publication**: 09/03/2019

Pris en charge jusqu’à 04/23/2020

**Céder**

- Quand vous utilisez le paramètre avancé [OutlookDefaultLabel](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook) pour définir une autre étiquette par défaut pour Outlook, et que l’étiquette que vous spécifiez n’a pas de sous-étiquettes pour la stratégie d’étiquette, l’étiquette est correctement appliquée.

- Lorsque le client Azure Information Protection est utilisé dans une application Office, un utilisateur avec un compte Active Directory qui n’est pas configuré pour l’authentification unique est invité à s’authentifier pour Azure Information Protection. Une fois l’authentification réussie, l’état du client passe correctement à en ligne, ce qui permet la fonctionnalité d’étiquetage.

## <a name="next-steps"></a>Étapes suivantes :

Vous ne savez pas s’il s’agit du bon client à installer ?  Consultez [choisir le client d’étiquetage à utiliser pour les ordinateurs Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Pour plus d’informations sur l’installation et l’utilisation de ce client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-unifiedlabelingclient-app.md)

- Pour les administrateurs : Azure Information Protection le Guide de l' [administrateur du client d’étiquetage unifié](clientv2-admin-guide.md)

