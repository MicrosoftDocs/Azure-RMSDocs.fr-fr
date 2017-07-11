---
title: "Suivi des documents pour Azure Information Protection"
description: Instructions et informations pour les administrateurs pour configurer et utiliser le suivi des documents pour Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 3b7ed22afea6b8575d12f6f83dcfc8419200c003
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="configuring-and-using-document-tracking-for-azure-information-protection" class="xliff"></a>

# Configuration et utilisation du suivi des documents pour Azure Information Protection

>*S’applique à : Services Active Directory Rights Management, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*

Si votre [abonnement prend en charge le suivi des documents](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), le site de suivi des documents est activé par défaut pour tous les utilisateurs de votre organisation. Le suivi des documents fournit des informations pour les utilisateurs et administrateurs concernant les dates d’accès à un document protégé et, si nécessaire, un document suivi peut être révoqué.

<a id="privacy-controls-for-your-document-tracking-site" class="xliff"></a>

## Contrôles de confidentialité de votre site de suivi de documents

Si l’affichage de toutes les informations de suivi des documents est interdit dans votre organisation pour des raisons de confidentialité, vous pouvez désactiver le suivi des documents à l’aide de l’applet de commande [Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature). 

Cette applet de commande désactive l’accès au site de suivi de documents afin que tous les utilisateurs de votre organisation ne puissent pas effectuer le suivi ou révoquer l’accès à des documents qu’ils ont protégés. Vous pouvez réactiver le suivi des documents à tout moment en utilisant [Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature) et vérifier si le suivi des documents est actuellement activé ou désactivé à l’aide de [Get-AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature). Pour exécuter ces applets de commande, vous devez disposer au moins de la version **2.3.0.0** du module Azure Rights Management (AADRM) pour PowerShell. 

Lorsque le site de suivi des documents est activé, il fournit des informations telles que les adresses de messagerie des personnes qui ont tenté d'accéder aux documents protégés et indique quand ces personnes ont tenté d'y accéder, ainsi que leur emplacement. Ce genre d’informations peut être très utile pour déterminer comment les documents partagés sont utilisés et s’ils doivent être révoqués si une activité suspecte est visible. Toutefois, pour des raisons de confidentialité, vous devrez peut-être désactiver ces informations utilisateur pour une partie ou l’intégralité des utilisateurs. 

Si vous avez des utilisateurs qui ne doivent pas avoir le suivi pour cette activité, ajoutez-les à un groupe qui est stocké dans Azure AD, et spécifiez ce groupe avec l’applet de commande [Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Set-AadrmDoNotTrackUserGroup). Lorsque vous exécutez cette applet de commande, vous devez spécifier un groupe unique. Toutefois, le groupe peut contenir des groupes imbriqués. 

Pour ces membres du groupe, leur activité liée à des documents que d’autres ont partagés avec eux n’est pas connectée à votre site de suivi de documents. En outre, aucune notification par e-mail n’est envoyée à l’utilisateur qui a partagé le document.

Lorsque vous utilisez cette configuration, tous les utilisateurs peuvent toujours utiliser le site de suivi de documents et révoquer l’accès à des documents qu’ils ont protégés. Toutefois, ils ne verront pas l’activité pour les utilisateurs que vous avez spécifiés à l’aide de l’applet de commande Set-AadrmDoNotTrackUserGroup.

Vous pouvez utiliser [Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup) si vous n’avez plus besoin de cette option. Ou, pour supprimer sélectivement des utilisateurs, supprimez-les du groupe, mais attention à la [mise en cache de groupe](../plan-design/prepare.md#group-membership-caching-by-azure-rights-management). Vous pouvez vérifier si cette option est actuellement en cours d’utilisation à l’aide de [Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup). Pour exécuter les applets de commande pour cette configuration de groupe, vous devez disposer au moins de la version **2.10.0.0** du module Azure Rights Management (AADRM) pour PowerShell.

Pour plus d’informations sur chacune de ces applets de commande, utilisez les liens fournis. Pour obtenir des instructions d’installation pour le module PowerShell, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md). Si vous avez précédemment téléchargé et installé le module, vérifiez le numéro de version en exécutant la commande suivante : `(Get-Module aadrm –ListAvailable).Version`


<a id="destination-urls-used-by-the-document-tracking-site" class="xliff"></a>

## URL de destination utilisées par le site de suivi de documents

Les URL suivantes sont utilisées pour le suivi des documents et doivent être autorisées sur tous les appareils et services entre les clients qui exécutent le client Azure Information Protection et Internet. Par exemple, ajoutez ces URL aux pare-feu ou à vos sites approuvés si vous utilisez Internet Explorer avec la sécurité renforcée.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Ces URL sont standard pour le service Azure Rights Management, à l’exception de l’URL virtualearth.net utilisée par les cartes Bing pour afficher l’emplacement de l’utilisateur.

<a id="tracking-and-revoking-documents-for-users" class="xliff"></a>

## Suivi et révocation de documents pour les utilisateurs

Quand les utilisateurs se connectent au site de suivi des documents, ils peuvent suivre et révoquer des documents qu’ils ont protégés à l’aide du client Azure Information Protection, ou qu’ils ont partagés à l’aide de l’application de partage RMS. Lorsque vous vous connectez comme administrateur pour Azure Information Protection (administrateur général), vous pouvez cliquer sur l’icône Administrateur pour passer en mode Administrateur et afficher les documents partagés par les utilisateurs de votre organisation :

![Icône Administrateur du site de suivi de document](../media/tracking-site-admin-icon.png)

Les actions que vous prenez en mode Administrateur sont auditées et consignées dans les fichiers journaux d’utilisation, et vous devez confirmer pour continuer. Pour plus d’informations sur la journalisation, consultez la section suivante.

Quand vous êtes en mode Administrateur, vous pouvez lancer une recherche par utilisateur ou par document. Une recherche par utilisateur affiche tous les documents partagés par l’utilisateur spécifié. Une recherche par document affiche tous les utilisateurs de votre organisation qui ont partagé ce document. Vous pouvez ensuite affiner les résultats de la recherche pour effectuer le suivi des documents partagés par les utilisateurs et, si nécessaire, les révoquer. 

Pour quitter le mode Administrateur, cliquez sur **X** en regard de **Quitter le mode Administrateur** :

![Quitter le mode administrateur dans le site de suivi des documents](../media/tracking-site-exit-admin-icon.png)

Pour obtenir des instructions sur l’utilisation du site de suivi des documents, consultez [Suivre et révoquer vos documents](client-track-revoke.md) dans le guide de l’utilisateur.

<a id="usage-logging-for-the-document-tracking-site" class="xliff"></a>

## Journalisation de l’utilisation du site de suivi des documents

Dans les fichiers journaux d’utilisation, deux champs s’appliquent au suivi des documents : **AdminAction** et **ActingAsUser**.

**AdminAction** Ce champ a la valeur True quand un administrateur utilise le site de suivi des documents en mode Administrateur, par exemple pour révoquer un document au nom d’un utilisateur ou pour voir quand il a été partagé. Ce champ est vide quand un utilisateur se connecte au site de suivi des documents.

**ActingAsUser**: Quand le champ AdminAction a la valeur True, ce champ contient le nom de l’utilisateur au nom duquel l’administrateur agit (comme propriétaire du document ou utilisateur recherché). Ce champ est vide quand un utilisateur se connecte au site de suivi des documents. 

Il existe également des types de demandes qui journalisent la façon dont les utilisateurs et les administrateurs utilisent le site de suivi des documents. Par exemple, **RevokeAccess** est le type de demande quand un utilisateur (ou un administrateur au nom d’un utilisateur) a révoqué un document dans le site de suivi des documents. Utilisez ce type de demande conjointement avec le champ AdminAction pour déterminer si l’utilisateur a révoqué son propre document (le champ AdminAction est vide) ou si un administrateur a révoqué un document au nom d’un d’utilisateur (AdminAction a la valeur True).


Pour plus d’informations sur la journalisation de l’utilisation, consultez [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md)



<a id="next-steps" class="xliff"></a>

## Étapes suivantes
Maintenant que vous avez configuré le site de suivi des documents pour le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
