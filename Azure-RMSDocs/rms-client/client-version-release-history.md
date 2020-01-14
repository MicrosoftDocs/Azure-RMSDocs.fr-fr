---
title: Azure Information Protection l’historique des versions du client & la stratégie de support
description: Découvrez les nouveautés et les modifications d’une version du client Azure Information Protection pour Windows, ainsi que la politique du cycle de vie du support.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/05/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 021919bbc683c47edd778b98a2a5685419515b8e
ms.sourcegitcommit: 2d75192e7cd2e322ab422fc2115aa063e8dda18b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75913347"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection : historique des versions et politique du support


>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*
>
> *Instructions pour : [Azure information protection client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*



Vous pouvez télécharger la dernière version en disponibilité générale (GA) et la préversion actuelle (si elle est disponible) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Après un bref délai de quelques semaines, la dernière version de la disponibilité générale est également incluse dans le catalogue Microsoft Update avec le nom de produit **Microsoft Azure Information Protection** > **client Microsoft Azure information protection**, ainsi que la classification des **mises à jour**. Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [Mise à niveau et maintenance du client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!TIP]
> Vous souhaitez utiliser le client d’étiquetage unifié Azure Information Protection, car vos étiquettes sont publiées à partir d’Office 365 Centre de sécurité et de conformité, Microsoft 365 Security Center ou Microsoft 365 Compliance Center ? Lorsque vous téléchargez, puis installez le client d’étiquetage unifié à partir du centre de téléchargement Microsoft, vous pouvez mettre à niveau votre client Azure Information Protection vers le [client d’étiquetage unifié](unifiedlabelingclient-version-release-history.md).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version en disponibilité générale (GA) du client Azure Information Protection est prise en charge jusqu'à six mois après la publication de la version GA suivante. À l’exception de cette section, la documentation n’inclut pas d’informations sur les versions du client non prises en charge. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les versions préliminaires ne doivent pas être déployées auprès des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions de la disponibilité générale qui ne sont plus prises en charge :

|Version du client|Date de publication|
|--------------|-------------|
|1.41.51.0|27/11/2018|
|1.37.19.0|17/09/2018|
|1.29.5.0|26/06/2018|
|1.27.48.0|30/05/2018|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|15/03/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|27/10/2016|
|1.1.23.0|10/01/2016|

Le format de date utilisé sur cette page est *mois/jour/année*.

À compter du 6/2/2019, le service d’étiquetage pour Azure Information Protection nécessite des connexions qui utilisent TLS 1,2.

Toutes les versions du client de 1.4.21.0 publiées 03/15/2017 prennent en charge TLS 1,2. Les versions clientes **1.3.155.2**, **1.2.4.0**et **1.1.23.0** n’utilisent pas TLS 1,2 et ne peuvent donc plus télécharger la stratégie de Azure information protection.

### <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés et les modifications d’une version prise en charge du client Azure Information Protection pour Windows. La dernière version est répertoriée en première position.

> [!NOTE]
> Les correctifs mineurs ne sont pas listés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, nous vous recommandons de vérifier s’il n’est pas résolu dans la toute dernière version GA. Si le problème persiste, vérifiez la version préliminaire actuelle (si disponible).
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).


## <a name="version-154330"></a>Version 1.54.33.0

**Publication**: 10/23/2019

Cette version comprend la version MSIPC 1.0.4008.0813 du client RMS.

Cette version propose des correctifs généraux pour la stabilité et les performances.

## <a name="version-153100"></a>Version 1.53.10.0

**Publication**: 07/15/2019

Pris en charge jusqu’à 04/23/2020

Cette version comprend la version MSIPC 1.0.3889.0419 du client RMS.

**Nouvelles fonctionnalités :**

- Nouveau paramètre de client avancé pour exempter les messages Outlook du paramètre de stratégie **tous les documents et e-mails doivent avoir une étiquette**. [Informations complémentaires](client-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)

- Nouveau paramètre de client avancé pour personnaliser davantage les paramètres qui implémentent des messages contextuels dans Outlook qui avertissent, justifient ou bloquent les courriers électroniques envoyés. Avec ce nouveau paramètre avancé, vous pouvez définir une action différente pour les messages électroniques sans pièce jointe. [Informations complémentaires](client-admin-guide-customizations.md#to-specify-a-different-action-for-email-messages-without-attachments)

**Correctifs** :

- Lorsque vous utilisez l’Explorateur de fichiers, cliquez avec le bouton droit pour étiqueter un fichier dont la protection est appliquée indépendamment d’une étiquette, cette protection est conservée. Par exemple, un utilisateur a appliqué des autorisations personnalisées à un fichier.

- Lorsque vous remplacez l’option ne pas transférer sur un thread de courrier électronique par une étiquette qui est configurée pour les autorisations définies par l’utilisateur et ne pas transférer, les destinataires d’origine peuvent toujours ouvrir le message électronique.

- Dans le scénario suivant, un utilisateur ne voit plus dans l’info-bulle de l’étiquette que l’étiquette a été automatiquement définie par lui : un utilisateur reçoit un e-mail protégé avec un document joint qui n’est pas étiqueté, mais qui est automatiquement protégé. Lorsque l’utilisateur de la même organisation que l’expéditeur ouvre le document, l’étiquette correspondante pour les paramètres de protection est appliquée au document.

- Le [droit d’utilisation](../configure-usage-rights.md#usage-rights-and-descriptions) minimal pour exécuter l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) est maintenant **Enregistrer sous, exporter** (exporter) au lieu de **copier** (extraire).

## <a name="version-1482040"></a>Version 1.48.204.0

**Publication**: 04/16/2019

Pris en charge jusqu’à 01/15/2020

Cette version inclut la version 1.0.3592.627 de MSIPC du client RMS.

**Nouvelles fonctionnalités :**

- Le scanneur de Azure Information Protection est maintenant configuré à partir du Portail Azure, plutôt qu’à l’aide de PowerShell.
    
    Si vous mettez à niveau à partir d’une version en disponibilité générale du scanneur, le processus de mise à niveau est différent des versions précédentes ; veillez à lire [Mise à niveau du scanneur Azure Information Protection](client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

- Le scanneur prend désormais en charge plusieurs bases de données de configuration sur la même instance de SQL Server lorsque vous spécifiez un nom de profil.

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

- Prise en charge de la découverte des points de terminaison pour [Azure information protection Analytics](../reports-aip.md), pour signaler les informations sensibles détectées lors de la première sauvegarde d’un document Office (à l’aide d’applications de bureau pour Word, Excel et PowerPoint) :
    - Pour découvrir ces informations, les documents n’ont pas besoin d’être étiquetés.
    - Les informations sensibles sont identifiées par des types d’informations prédéfinis et personnalisés.
    - Si vous ne souhaitez pas que les types d’informations sensibles soient envoyés à Azure Information Protection Analytics, vous pouvez désactiver la découverte de point de terminaison avec un [paramètre client avancé](client-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics).

- Nouveaux paramètres client avancés implémentant des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails. [Informations complémentaires](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    Notez que si vous avez configuré la propriété de client avancé de OutlookCollaborationTrustedDomains pour la version préliminaire, ce paramètre est désormais remplacé par trois nouveaux paramètres, afin que les domaines puissent être exemptés par action : OutlookWarnTrustedDomains, OutlookJustifyTrustedDomains et OutlookBlockTrustedDomains.

- Si vous étiquetez et protégez des fichiers à l’aide de la cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), vous pouvez utiliser le paramètre *EnableTracking* pour enregistrer le fichier sur le site de suivi des documents. [Informations complémentaires](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- Nouveau paramètre client avancé pour [Azure information protection Analytics](../reports-aip.md), afin d’éviter d’envoyer des correspondances de types d’informations pour un sous-ensemble d’utilisateurs lorsque vous avez activé la case à cocher dans la portail Azure qui permet une analyse plus approfondie de vos données sensibles. Ce paramètre s’applique au client et au scanneur. [Informations complémentaires](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)

- Nouveau paramètre client avancé applicable uniquement lorsque vous configurez le paramètre de stratégie de manière à ne pas afficher les autorisations personnalisées : quand un fichier est protégé par des autorisations personnalisées, affichez l’option autorisations personnalisées dans l’Explorateur de fichiers pour que les utilisateurs puissent voir et les modifier (s’ils disposent des autorisations nécessaires pour modifier les paramètres de protection). [Informations complémentaires](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)


**Correctifs** :

- Les chemins d’accès et les noms de fichiers n’affichent pas de points d’interrogation ( **?** ) à la place des caractères non ASCII dans l’analytique Azure Information Protection lorsque les paramètres régionaux du système d’exploitation d’envoi sont configurés en anglais.

- De nouveaux marquages visuels sont systématiquement appliqués lorsqu’un utilisateur ajoute de nouvelles sections à un document Word, puis attribue une nouvelle étiquette au document.

- Le client Azure Information Protection supprime correctement la protection d’un document PDF protégé par l’application de partage Rights Management.

- Les sous-étiquettes sont correctement appliquées par PowerShell et le scanneur lorsque l’étiquette parent est configurée pour des autorisations définies par l’utilisateur.

- Le client Azure Information Protection affiche correctement les étiquettes qui ont été appliquées par les [clients qui prennent en charge l’étiquetage unifié](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

- Les documents s’ouvrent correctement dans Office sans message de récupération lorsque la protection a été supprimée par l’Explorateur de fichiers et avec le bouton droit, PowerShell et le scanneur.

- Quand vous utilisez le paramètre client avancé pour définir une [étiquette par défaut pour Outlook](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook), vous pouvez appliquer une étiquette parent qui a des sous-étiquettes quand toutes ces sous-étiquettes sont désactivées pour l’utilisateur.

- Quand vous utilisez le [paramètre de stratégie](../configure-policy-settings.md) **pour les messages électroniques avec pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes** et l’étiquette avec la classification la plus élevée est configurée pour les autorisations définies par l’utilisateur, le résultat était auparavant que l’étiquette était appliquée à l’e-mail, mais la protection ne l’était pas. Maintenant :
    - Lorsque les autorisations définies par l’utilisateur de l’étiquette sont Outlook (ne pas transférer) : appliquez cette étiquette et sa protection ne pas transférer à l’e-mail.
    - Lorsque les autorisations définies par l’utilisateur de l’étiquette sont uniquement pour Word, Excel, PowerPoint et l’Explorateur de fichiers : n’appliquez pas l’étiquette et n’appliquez pas de protection à l’e-mail.

**Autres modifications :**

- Les types d’informations sensibles suivants ne sont [plus pris en charge](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) pour les étiquettes que vous configurez pour la classification recommandée ou automatique :
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

- Le [paramètre de stratégie](../configure-policy-settings.md) **les utilisateurs doivent fournir une justification pour définir une étiquette de classification inférieure, supprimer une étiquette ou supprimer la protection** ne s’applique plus au scanneur. Le scanneur effectue ces actions lorsque vous configurez le paramètre **Renommer les fichiers** sur **activé** dans le profil du scanneur, puis activez la case à cocher autoriser l’étiquette à passer à une **version antérieure** .

## <a name="next-steps"></a>Étapes suivantes

Vous ne savez pas s’il s’agit du bon client à installer ?  Consultez [choisir le client d’étiquetage à utiliser pour les ordinateurs Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Pour plus d’informations sur l’installation et l’utilisation du client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md)
