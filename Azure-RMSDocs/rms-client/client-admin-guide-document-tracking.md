---
title: Suivi des documents pour Azure Information Protection
description: Instructions et informations pour les administrateurs pour configurer et utiliser le suivi des documents pour Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 8153b189a6e4f77e2a4c1f7d630fbb2f32b667f1
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39373734"
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>Guide de l’administrateur : Configuration et utilisation du suivi des documents pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Si votre [abonnement prend en charge le suivi des documents](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), le site de suivi des documents est activé par défaut pour tous les utilisateurs de votre organisation. Le suivi des documents fournit des informations pour les utilisateurs et administrateurs concernant les dates d’accès à un document protégé et, si nécessaire, un document suivi peut être révoqué.

## <a name="using-powershell-to-manage-the-document-tracking-site"></a>Utilisation de PowerShell pour gérer le site de suivi de documents

Les sections suivantes contiennent des informations sur la façon de gérer le site de suivi de documents à l’aide de PowerShell. Pour connaître les instructions d'installation du module PowerShell, consultez [Installation du module PowerShell AADRM](../deploy-use/install-powershell.md). Si vous avez précédemment téléchargé et installé le module, vérifiez le numéro de version en exécutant la commande suivante : `(Get-Module aadrm –ListAvailable).Version`

Pour plus d’informations sur chacune des applets de commande, utilisez les liens fournis.

### <a name="privacy-controls-for-your-document-tracking-site"></a>Contrôles de confidentialité de votre site de suivi de documents

Si l’affichage de toutes les informations de suivi des documents est interdit dans votre organisation pour des raisons de confidentialité, vous pouvez désactiver le suivi des documents à l’aide de l’applet de commande [Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature). 

Cette applet de commande désactive l’accès au site de suivi de documents afin que tous les utilisateurs de votre organisation ne puissent pas effectuer le suivi ou révoquer l’accès à des documents qu’ils ont protégés. Vous pouvez réactiver le suivi des documents à tout moment en utilisant [Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature) et vérifier si le suivi des documents est actuellement activé ou désactivé à l’aide de [Get-AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature). Pour exécuter ces applets de commande, vous devez disposer au minimum de la version **2.3.0.0** du module AADRM pour PowerShell. 

Lorsque le site de suivi des documents est activé, il fournit des informations telles que les adresses de messagerie des personnes qui ont tenté d'accéder aux documents protégés et indique quand ces personnes ont tenté d'y accéder, ainsi que leur emplacement. Ce niveau d’informations peut être utile pour déterminer comment les documents partagés sont utilisés et s’ils doivent être révoqués en cas d’activité suspecte. Toutefois, pour des raisons de confidentialité, vous devrez peut-être désactiver ces informations utilisateur pour une partie ou l’intégralité des utilisateurs. 

Si vous avez des utilisateurs pour lesquels cette activité ne doit pas être suivie par d’autres utilisateurs, ajoutez-les à un groupe qui est stocké dans Azure AD, et spécifiez ce groupe avec l’applet de commande [Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Set-AadrmDoNotTrackUserGroup). Lorsque vous exécutez cette applet de commande, vous devez spécifier un groupe unique. Toutefois, le groupe peut contenir des groupes imbriqués. 

Pour ces membres du groupe, les utilisateurs ne peuvent pas voir les activités sur le site de suivi du document lorsque cette activité est liée à des documents qu’ils partagent avec eux. En outre, aucune notification par e-mail n’est envoyée à l’utilisateur qui a partagé le document.

Lorsque vous utilisez cette configuration, tous les utilisateurs peuvent toujours utiliser le site de suivi de documents et révoquer l’accès à des documents qu’ils ont protégés. Toutefois, ils ne voient pas l’activité des utilisateurs que vous avez spécifiés à l’aide de l’applet de commande Set-AadrmDoNotTrackUserGroup.

Ce paramètre affecte uniquement les utilisateurs finaux. Les administrateurs pour Azure Information Protection peuvent toujours suivre les activités de tous les utilisateurs, même lorsque ces utilisateurs sont spécifiés à l’aide de Set-AadrmDoNotTrackUserGroup. Pour plus d’informations sur la façon dont les administrateurs peuvent suivre les documents pour les utilisateurs, consultez la section [Suivi et révocation de documents pour les utilisateurs](#tracking-and-revoking-documents-for-users).


### <a name="logging-information-from-the-document-tracking-site"></a>Téléchargement des informations de journalisation à partir du site de suivi de documents

Si vous utilisez la version minimale **2.13.0.0** du module AADRM, vous pouvez utiliser les applets de commande suivantes pour télécharger les informations de journalisation à partir du site de suivi de documents :

- [Get-AadrmTrackingLog](/powershell/module/aadrm/Get-AadrmTrackingLog)
    
    Cette applet de commande retourne les informations de suivi relatives aux documents protégés qu’un utilisateur spécifié a protégés (l’émetteur Rights Management) ou auxquels il a accédé. Utilisez cette applet de commande pour vous aider à répondre à la question « Quels documents protégés ont fait l’objet d’un suivi ou d’un accès par un utilisateur spécifié ? »

- [Get-AadrmDocumentLog](/powershell/module/aadrm/Get-AadrmDocumentLog)
    
    Cette applet de commande retourne les informations sur la protection des documents suivis d’un utilisateur spécifié qui a protégé ces documents (l’émetteur Rights Management) ou qui en était le propriétaire Rights Management, ou des documents protégés ayant été configurés pour autoriser l’accès direct par l’utilisateur. Utilisez cette applet de commande pour vous aider à répondre à la question « Comment les documents d’un utilisateur spécifié sont-ils protégés ? »
 
## <a name="destination-urls-used-by-the-document-tracking-site"></a>URL de destination utilisées par le site de suivi de documents

Les URL suivantes sont utilisées pour le suivi des documents et doivent être autorisées sur tous les appareils et services entre les clients qui exécutent le client Azure Information Protection et Internet. Par exemple, ajoutez ces URL aux pare-feu ou à vos sites approuvés si vous utilisez Internet Explorer avec la sécurité renforcée.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Ces URL sont standard pour le service Azure Rights Management, à l’exception de l’URL virtualearth.net utilisée par les cartes Bing pour afficher l’emplacement de l’utilisateur.

## <a name="tracking-and-revoking-documents-for-users"></a>Suivi et révocation de documents pour les utilisateurs

Quand les utilisateurs se connectent au site de suivi des documents, ils peuvent suivre et révoquer des documents qu’ils ont protégés à l’aide du client Azure Information Protection, ou qu’ils ont partagés à l’aide de l’application de partage RMS. Quand vous vous connectez en tant qu’administrateur général Azure AD pour votre abonné, vous pouvez cliquer sur l’icône Administrateur afin passer en mode Administrateur. Les autres rôles d’administrateur ne prennent pas en charge ce mode pour le site de suivi de document. 

![Icône Administrateur du site de suivi de document](../media/tracking-site-admin-icon.png)

Le mode administrateur vous permet d’afficher les documents que les utilisateurs de votre organisation ont choisi de suivre à l’aide du client Azure Information Protection, ou ceux qu’ils ont partagé à l’aide de l’application de partage Rights Management.

> [!NOTE] 
> Si vous ne voyez pas cette icône bien que vous soyez un administrateur général, cela signifie que vous n’avez pas encore partagé de documents. Dans ce cas, utilisez l’URL suivante pour accéder au site de suivi des documents : https://portal.azurerms.com/#/admin

Les actions que vous prenez en mode Administrateur sont auditées et consignées dans les fichiers journaux d’utilisation, et vous devez confirmer pour continuer. Pour plus d’informations sur la journalisation, consultez la section suivante.

Quand vous êtes en mode Administrateur, vous pouvez lancer une recherche par utilisateur ou par document. Si vous effectuez une recherche par utilisateur, vous affichez tous les documents que l’utilisateur spécifié a choisi de suivre à l’aide du client Azure Information Protection ou a partagé à l’aide de l’application de partage Rights Management. 

Si vous effectuez une recherche par document, vous affichez tous les utilisateurs de votre organisation qui ont suivi ce document à l’aide du client Azure Information Protection ou l’ont partagé à l’aide de l’application de partage Rights Management. Vous pouvez ensuite affiner les résultats de la recherche pour suivre les documents que les utilisateurs ont protégé et révoquer ces documents, si nécessaire. 

Pour quitter le mode Administrateur, cliquez sur **X** en regard de **Quitter le mode Administrateur** :

![Quitter le mode administrateur dans le site de suivi des documents](../media/tracking-site-exit-admin-icon.png)

Pour obtenir des instructions sur l’utilisation du site de suivi des documents, consultez [Suivre et révoquer vos documents](client-track-revoke.md) dans le guide de l’utilisateur.

## <a name="usage-logging-for-the-document-tracking-site"></a>Journalisation de l’utilisation du site de suivi des documents

Dans les fichiers journaux d’utilisation, deux champs s’appliquent au suivi des documents : **AdminAction** et **ActingAsUser**.

**AdminAction** Ce champ a la valeur True quand un administrateur utilise le site de suivi des documents en mode Administrateur, par exemple pour révoquer un document au nom d’un utilisateur ou pour voir quand il a été partagé. Ce champ est vide quand un utilisateur se connecte au site de suivi des documents.

**ActingAsUser**: Quand le champ AdminAction a la valeur True, ce champ contient le nom de l’utilisateur au nom duquel l’administrateur agit (comme propriétaire du document ou utilisateur recherché). Ce champ est vide quand un utilisateur se connecte au site de suivi des documents. 

Il existe également des types de demandes qui journalisent la façon dont les utilisateurs et les administrateurs utilisent le site de suivi des documents. Par exemple, **RevokeAccess** est le type de demande quand un utilisateur (ou un administrateur au nom d’un utilisateur) a révoqué un document dans le site de suivi des documents. Utilisez ce type de demande conjointement avec le champ AdminAction pour déterminer si l’utilisateur a révoqué son propre document (le champ AdminAction est vide) ou si un administrateur a révoqué un document au nom d’un d’utilisateur (AdminAction a la valeur True).


Pour plus d’informations sur la journalisation de l’utilisation, consultez [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez configuré le site de suivi des documents pour le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

