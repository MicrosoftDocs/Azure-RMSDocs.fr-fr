---
title: Client de Azure Information Protection - stratégie de prise en charge et d’historique de Version
description: Découvrez les nouveautés et les changements d’une version du client Azure Information Protection pour Windows, ainsi que la politique du cycle de vie du support.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 569b53a958ae90153133406141be15703ef92901
ms.sourcegitcommit: 849c493cef6b2578945c528f4e17373a2ef26287
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67563387"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection : Historique de publication et politique de support des versions

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

L’équipe Azure Information Protection met régulièrement à jour le client Azure Information Protection avec des correctifs et des nouvelles fonctionnalités. 

Vous pouvez télécharger la dernière version en disponibilité générale (GA) et la préversion actuelle (si elle est disponible) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Après un court délai de quelques semaines en général, la version plus récente de disponibilité générale est également incluse dans le catalogue Microsoft Update avec un nom de produit de **Microsoft Azure Information Protection**  >  **Client Microsoft Azure Information Protection**et la classification de **mises à jour**. Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [Mise à niveau et maintenance du client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!TIP]
> Intéressé par l’utilisation Azure Information Protection client unifié, étiquetage, car vos étiquettes sont publiées à partir de la sécurité Office 365 & centre de conformité, centre de sécurité Microsoft 365 ou centre de conformité de Microsoft 365 ? Lorsque vous téléchargez et installez le client étiquetage unifié à partir du Microsoft Download Center, vous pouvez mettre à niveau votre client Azure Information Protection à ce [client étiquetage unifié](unifiedlabelingclient-version-release-history.md).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version en disponibilité générale (GA) du client Azure Information Protection est prise en charge jusqu'à six mois après la publication de la version GA suivante. À l’exception de cette section, la documentation n’inclut pas d’informations sur les versions non pris en charge du client. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les préversions ne doivent pas être déployées pour des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions en disponibilité générale qui ne sont plus prises en charge :

|Version du client|Date de sortie|
|--------------|--------------------------|
|1.37.19.0|17/09/2018|
|1.29.5.0|26/06/2018|
|1.27.48.0|30/05/2018|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|03/15/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|10/27/2016|
|1.1.23.0|10/01/2016|

À partir de 6/2/2019, le service d’étiquetage pour Azure Information Protection nécessite des connexions qui utilisent TLS 1.2.

Toutes les versions de client à partir de 1.4.21.0 publié le 15/03/2017 prise en charge de TLS 1.2. Versions du client **1.3.155.2**, **1.2.4.0**, et **1.1.23.0** n’utilisent pas de TLS 1.2 et par conséquent ne peuvent plus télécharger la stratégie Azure Information Protection.

### <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés et les changements d’une version prise en charge du client Azure Information Protection pour Windows. La dernière version est la première sur la liste. 

> [!NOTE]
> Les correctifs mineurs ne sont pas listés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, nous vous recommandons de vérifier s’il n’est pas résolu dans la toute dernière version GA. Si le problème persiste, vérifiez la version préliminaire actuelle (si disponible).
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

## <a name="version-1482040"></a>Version 1.48.204.0

**Date de publication** : 04/16/2019

Cette version inclut la version 1.0.3592.627 de MSIPC du client RMS.

**Nouvelles fonctionnalités :**

- Le scanneur Azure Information Protection est maintenant configuré à partir du portail Azure, plutôt qu’à l’aide de PowerShell.
    
    Si vous mettez à niveau à partir d’une version en disponibilité générale du scanneur, le processus de mise à niveau est différent des versions précédentes ; veillez à lire [Mise à niveau du scanneur Azure Information Protection](client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

- L’analyseur prend désormais en charge plusieurs bases de données de configuration sur la même instance SQL server lorsque vous spécifiez un nom de profil.

- Prise en charge des types d’informations sensibles suivants permettant d’identifier les informations d’identification dans les documents et e-mails :
    - Chaîne de connexion Azure Service Bus
    - Chaîne de connexion Azure IoT
    - Compte de stockage Azure
    - Chaîne de connexion de la base de données Azure IAAS et chaîne de connexion SQL Azure
    - Chaîne de connexion du Cache Redis Azure
    - Azure SAS
    - Chaîne de connexion SQL Server
    - Clé d’authentification Azure DocumentDB
    - Mot de passe de paramètre de publication Azure
    - Clé de compte de stockage Azure (générique)

- Nouveaux paramètres client avancés implémentant des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails. [Plus d’informations](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    Notez que si vous avez configuré la propriété de client avancé de OutlookCollaborationTrustedDomains pour la version d’évaluation, ce paramètre est désormais remplacé par trois nouveaux paramètres, afin que les domaines peuvent être exemptés par action : OutlookWarnTrustedDomains, OutlookJustifyTrustedDomains et OutlookBlockTrustedDomains.

- Si vous étiquetez et protégez des fichiers à l’aide de la cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), vous pouvez utiliser le paramètre *EnableTracking* pour enregistrer le fichier sur le site de suivi des documents. [Plus d’informations](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- Nouveau paramètre client avancé qui est applicable seulement quand vous configurez le paramètre de stratégie de façon à ne pas afficher des autorisations personnalisées : Quand un fichier est protégé par des autorisations personnalisées, affichez l’option des autorisations personnalisées dans l’Explorateur de fichiers, pour que les utilisateurs puissent les voir et les changer (s’ils ont les autorisations nécessaires pour changer les paramètres de protection). [Plus d’informations](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)

- Découverte de point de terminaison pour [analytique d’Azure Information Protection](../reports-aip.md).
    
- Deux nouveaux paramètres avancés du client pour l’analytique, pour les scénarios suivants :
    
    - Empêcher l’envoi de correspondances de types d’informations à un sous-ensemble d’utilisateurs lorsque la case correspondant à la collecte de correspondances de contenu est cochée sur le Portail Azure. [Plus d’informations](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - Pour le **découverte de données** de rapport, indique si les fichiers contiennent des informations sensibles. [Plus d’informations](client-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)

**Correctifs** :

- Les chemins d’accès et les noms de fichiers n’affichent pas de points d’interrogation ( **?** ) à la place des caractères non ASCII dans l’analytique Azure Information Protection lorsque les paramètres régionaux du système d’exploitation d’envoi sont configurés en anglais.

- De nouveaux marquages visuels sont systématiquement appliqués lorsqu’un utilisateur ajoute de nouvelles sections à un document Word, puis attribue une nouvelle étiquette au document.

- Le client Azure Information Protection supprime correctement la protection d’un document PDF protégé par l’application de partage Rights Management.

- Les sous-étiquettes sont correctement appliquées par PowerShell et le scanneur lorsque l’étiquette parent est configurée pour des autorisations définies par l’utilisateur.

- Le client Azure Information Protection affiche correctement les étiquettes qui ont été appliquées par les [clients qui prennent en charge l’étiquetage unifié](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

- Les documents s’ouvrent correctement dans Office sans message de récupération lorsque la protection a été supprimée par l’Explorateur de fichiers et avec le bouton droit, PowerShell et le scanneur.

- Quand vous utilisez le paramètre client avancé pour définir une [étiquette par défaut pour Outlook](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook), vous pouvez appliquer une étiquette parent qui a des sous-étiquettes quand toutes ces sous-étiquettes sont désactivées pour l’utilisateur.

- Quand vous utilisez le [paramètre de stratégie](../configure-policy-settings.md) **Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes**, et l’étiquette avec la classification la plus élevée est configurée pour les autorisations définies par l’utilisateur. Avant, le résultat était que l’étiquette était appliquée à l’e-mail, mais la protection ne l’était pas. Maintenant :
    - Quand les autorisations définies par l’utilisateur de l’étiquette incluent Outlook (Ne pas transférer) : Appliquer cette étiquette et sa protection Ne pas transférer à l’e-mail.
    - Quand les autorisations définies par l’utilisateur de l’étiquette sont seulement pour Word, Excel, PowerPoint et l’Explorateur de fichiers : Ne pas appliquer l’étiquette et n’appliquer aucune protection à l’e-mail.

**Autres modifications :**

- Les types d’informations sensibles suivants sont [n’est plus pris en charge](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) pour les étiquettes que vous configurez pour recommandé ou la classification automatique :
    - Numéro de téléphone dans l’UE
    - Coordonnées GPS dans l’UE

- Étant donné que le scanneur Azure Information Protection est configuré à partir du portail Azure, les cmdlets suivantes sont désormais déconseillées et ne peuvent pas être utilisées pour configurer des référentiels de données ou la liste de types de fichiers :
    - Add-AIPScannerRepository
    - Add-AIPScannerScannedFileTypes
    - Get-AIPScannerRepository
    - Remove-AIPScannerRepository
    - Remove-AIPScannerScannedFileTypes
    - Set-AIPScannerRepository
    - Set-AIPScannerScannedFileTypes

- Nouvelle cmdlet PowerShell, [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration), pour les scénarios dans lesquels le scanneur Azure Information Protection ne peut pas télécharger sa configuration à partir du portail Azure.

- Le scanneur Azure Information Protection n’exclut plus les fichiers .zip par défaut. Pour inspecter et étiqueter les fichiers .zip, consultez la section [Pour inspecter les fichiers .zip](client-admin-guide-file-types.md#to-inspect-zip-files) du guide d’administration.

- Le [paramètre de stratégie](../configure-policy-settings.md) **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection** ne s’applique plus au scanneur. Le scanneur effectue ces actions lorsque vous configurez le paramètre **Relabel files** (Réétiqueter les fichiers) sur **Activé** dans le profil du scanneur.

## <a name="version-141510"></a>Version 1.41.51.0

**Date de publication** : 27/11/2018

Prise en charge par le biais 16/10/2019

Cette version inclut la version 1.0.3592.627 de MSIPC du client RMS.

**Nouvelles fonctionnalités :**

- Le client Azure Information Protection par défaut protège maintenant les fichiers PDF à l’aide de la norme ISO pour le chiffrement PDF. Auparavant, vous deviez activer cette prise en charge avec un paramètre client avancé.
    
    Si vous souhaitez que le client rétablisse la protection des fichiers PDF à l’aide d’une extension de nom de fichier .ppdf, utilisez le même [paramètre client avancé](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), mais spécifiez **False**.

- L’audit de données prise en charge pour [reporting centrale](../reports-aip.md) à l’aide d’analytique Azure Information Protection, a annoncé au Microsoft Ignite 2018.

- Prise en charge des [marquages visuels](../configure-policy-markings.md) de différentes couleurs dans Excel.

- Pour les déploiements S/MIME existants, nouveau paramètre client avancé permettant de configurer une étiquette de façon à ce qu’elle applique automatiquement la protection S/MIME dans Outlook. [Plus d’informations](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Nouveau paramètre client avancé (qui évite d’avoir à modifier le Registre) permettant d’empêcher l’affichage des invites de connexion du service Azure Information Protection pour les [ordinateurs déconnectés](client-admin-guide-customizations.md#support-for-disconnected-computers).

- Un nouveau paramètre client avancé pour [prendre en charge l’ordre des sous-étiquettes](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) lorsque vous utilisez le paramètre de stratégie suivant :
    - **Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes**

**Correctifs** :

- Le client Azure Information Protection n’exclut plus les extensions de nom de fichier .msg, .rar et .zip pour l’Explorateur de fichiers (clic droit) et les commandes PowerShell. Toutefois, ces extensions de nom de fichier restent exclues par défaut pour le scanneur. 

- Le client Azure Information Protection peut ôter la protection de plusieurs fichiers (sélection multiple et dossier contenant des fichiers protégés) si vous utilisez l’Explorateur de fichiers avec clic droit.

- Pour Excel :
    
    - Les marquages visuels sont maintenant appliqués si la feuille de calcul est enregistrée pendant la modification d’une cellule.
    
    - Excel 2010 : Pour une feuille de calcul protégée au [niveau d’autorisation](../configure-usage-rights.md#rights-included-in-permissions-levels) Co-auteur, le bouton **Supprimer l’étiquette** est désormais disponible quand vous cliquez avec le bouton droit sur le fichier et que vous choisissez **Classer et protéger**.

- Les paramètres client avancés permettant de [supprimer les en-têtes et pieds de page d’autres solutions d’étiquetage](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) prennent désormais en charge les dispositions personnalisées.

**Autres modifications :**

- Quand la planification du scanneur est définie sur **Toujours**, il y a maintenant un délai de 30 secondes entre les analyses.

- Le scanneur ne modifie plus le propriétaire de Rights Management pour les fichiers qu’il étiquette lorsque le fichier est déjà protégé.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’installation et l’utilisation du client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Client Azure Information Protection - Guide de l’administrateur](client-admin-guide.md)
