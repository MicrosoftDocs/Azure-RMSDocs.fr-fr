---
title: Suivi des documents pour Azure Information Protection
description: Instructions et informations pour les administrateurs pour configurer et utiliser le suivi des documents pour Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.subservice: doctrack
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: af0fae810574603dfc947656de8cee3bb0e8b149
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935331"
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>Guide de l’administrateur : Configuration et utilisation du suivi des documents pour Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*
>
> *Instructions pour : [Azure information protection client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Si votre [abonnement prend en charge le suivi des documents](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), le site de suivi des documents est activé par défaut pour tous les utilisateurs de votre organisation. Le suivi des documents fournit des informations pour les utilisateurs et administrateurs concernant les dates d’accès à un document protégé et, si nécessaire, un document suivi peut être révoqué.

## <a name="using-powershell-to-manage-the-document-tracking-site"></a>Utilisation de PowerShell pour gérer le site de suivi de documents

Les sections suivantes contiennent des informations sur la façon de gérer le site de suivi de documents à l’aide de PowerShell. Pour obtenir des instructions d’installation pour le module PowerShell, consultez [installation du module PowerShell AIPService](../install-powershell.md).

Pour plus d’informations sur chacune des applets de commande, utilisez les liens fournis.

### <a name="privacy-controls-for-your-document-tracking-site"></a>Contrôles de confidentialité de votre site de suivi de documents

Si l’affichage de toutes les informations de suivi des documents est interdit dans votre organisation en raison des exigences de confidentialité, vous pouvez désactiver le suivi des documents à l’aide de l’applet de commande [Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) . 

Cette applet de commande désactive l’accès au site de suivi de documents afin que tous les utilisateurs de votre organisation ne puissent pas effectuer le suivi ou révoquer l’accès à des documents qu’ils ont protégés. Vous pouvez réactiver le suivi des documents à tout moment, à l’aide de [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature), et vous pouvez vérifier si le suivi des documents est actuellement activé ou désactivé à l’aide de la [AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature). 

Lorsque le site de suivi des documents est activé, il fournit des informations telles que les adresses de messagerie des personnes qui ont tenté d'accéder aux documents protégés et indique quand ces personnes ont tenté d'y accéder, ainsi que leur emplacement. Ce niveau d’informations peut être utile pour déterminer comment les documents partagés sont utilisés et s’ils doivent être révoqués en cas d’activité suspecte. Toutefois, pour des raisons de confidentialité, vous devrez peut-être désactiver ces informations utilisateur pour une partie ou l’intégralité des utilisateurs. 

Si vous avez des utilisateurs dont l’activité ne doit pas être suivie par d’autres utilisateurs, ajoutez-les à un groupe qui est stocké dans Azure AD et spécifiez ce groupe avec l’applet de commande [Set-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Set-AipServiceDoNotTrackUserGroup) . Lorsque vous exécutez cette applet de commande, vous devez spécifier un groupe unique. Toutefois, le groupe peut contenir des groupes imbriqués. 

Pour ces membres du groupe, les utilisateurs ne peuvent pas voir les activités sur le site de suivi du document lorsque cette activité est liée à des documents qu’ils partagent avec eux. En outre, aucune notification par e-mail n’est envoyée à l’utilisateur qui a partagé le document.

Lorsque vous utilisez cette configuration, tous les utilisateurs peuvent toujours utiliser le site de suivi de documents et révoquer l’accès à des documents qu’ils ont protégés. Toutefois, ils ne voient pas l’activité des utilisateurs que vous avez spécifiés à l’aide de l’applet de commande Set-AipServiceDoNotTrackUserGroup.

Ce paramètre affecte uniquement les utilisateurs finaux. Les administrateurs de Azure Information Protection peuvent toujours suivre les activités de tous les utilisateurs, même lorsque ces utilisateurs sont spécifiés à l’aide de Set-AipServiceDoNotTrackUserGroup. Pour plus d’informations sur la façon dont les administrateurs peuvent suivre les documents pour les utilisateurs, consultez la section [Suivi et révocation de documents pour les utilisateurs](#tracking-and-revoking-documents-for-users).


### <a name="logging-information-from-the-document-tracking-site"></a>Téléchargement des informations de journalisation à partir du site de suivi de documents

Vous pouvez utiliser les applets de commande suivantes pour télécharger les informations de journalisation à partir du site de suivi des documents :

- [Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)
    
    Cette applet de commande retourne les informations de suivi relatives aux documents protégés qu’un utilisateur spécifié a protégés (l’émetteur Rights Management) ou auxquels il a accédé. Utilisez cette applet de commande pour vous aider à répondre à la question « Quels documents protégés ont fait l’objet d’un suivi ou d’un accès par un utilisateur spécifié ? »

- [Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)
    
    Cette applet de commande retourne les informations sur la protection des documents suivis d’un utilisateur spécifié qui a protégé ces documents (l’émetteur Rights Management) ou qui en était le propriétaire Rights Management, ou des documents protégés ayant été configurés pour autoriser l’accès direct par l’utilisateur. Utilisez cette applet de commande pour vous aider à répondre à la question « Comment les documents d’un utilisateur spécifié sont-ils protégés ? »

## <a name="destination-urls-used-by-the-document-tracking-site"></a>URL de destination utilisées par le site de suivi de documents

Les URL suivantes sont utilisées pour le suivi des documents et doivent être autorisées sur tous les appareils et services entre les clients qui exécutent le client Azure Information Protection et Internet. Par exemple, ajoutez ces URL aux pare-feu ou à vos sites approuvés si vous utilisez Internet Explorer avec la sécurité renforcée.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Ces URL sont standard pour le service Azure Rights Management, à l’exception de l’URL virtualearth.net utilisée par les cartes Bing pour afficher l’emplacement de l’utilisateur.

## <a name="tracking-and-revoking-documents-for-users"></a>Suivi et révocation de documents pour les utilisateurs

Quand les utilisateurs se connectent au site de suivi des documents, ils peuvent suivre et révoquer des documents qu’ils ont protégés à l’aide du client Azure Information Protection. Quand vous vous connectez en tant qu’administrateur général Azure AD pour votre abonné, vous pouvez cliquer sur l’icône Administrateur afin passer en mode Administrateur. Les autres rôles d’administrateur ne prennent pas en charge ce mode pour le site de suivi de document. 

![Icône Administrateur du site de suivi de document](../media/tracking-site-admin-icon.png)

Le mode administrateur vous permet de voir les documents que les utilisateurs de votre organisation ont choisi de suivre à l’aide du client Azure Information Protection.

> [!NOTE] 
> Si vous ne voyez pas cette icône bien que vous soyez un administrateur général, cela signifie que vous n’avez pas encore partagé de documents. Dans ce cas, utilisez l’URL suivante pour accéder au site de suivi des documents : https://portal.azurerms.com/#/admin

Les actions que vous prenez en mode Administrateur sont auditées et consignées dans les fichiers journaux d’utilisation, et vous devez confirmer pour continuer. Pour plus d’informations sur la journalisation, consultez la section suivante.

Quand vous êtes en mode Administrateur, vous pouvez lancer une recherche par utilisateur ou par document. Si vous effectuez une recherche par utilisateur, vous voyez tous les documents que l’utilisateur spécifié a choisi de suivre à l’aide du client Azure Information Protection. 

Si vous effectuez une recherche par document, vous voyez tous les utilisateurs de votre organisation qui ont suivi ce document à l’aide du client Azure Information Protection. Vous pouvez ensuite affiner les résultats de la recherche pour suivre les documents que les utilisateurs ont protégé et révoquer ces documents, si nécessaire. 

Pour quitter le mode Administrateur, cliquez sur **X** en regard de **Quitter le mode Administrateur** :

![Quitter le mode administrateur dans le site de suivi des documents](../media/tracking-site-exit-admin-icon.png)

Pour obtenir des instructions sur l’utilisation du site de suivi des documents, consultez [Suivre et révoquer vos documents](client-track-revoke.md) dans le guide de l’utilisateur.

### <a name="using-powershell-to-register-labeled-documents-with-the-document-tracking-site"></a>Utiliser PowerShell pour enregistrer des documents étiquetés sur le site de suivi des documents

Pour pouvoir suivre et révoquer un document, il doit d’abord être enregistré sur le site de suivi des documents. Cette action se produit quand les utilisateurs sélectionnent l’option **Suivre et révoquer** dans l’Explorateur de fichiers ou leurs applications Office lorsqu’ils utilisent le client Azure Information Protection.

Si vous étiquetez et protégez des fichiers pour des utilisateurs à l’aide de la cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), vous pouvez utiliser le paramètre *EnableTracking* pour enregistrer le fichier sur le site de suivi des documents. Exemple :

    Set-AIPFileLabel -Path C:\Projects\ -LabelId ade72bf1-4714-4714-4714-a325f824c55a -EnableTracking

## <a name="usage-logging-for-the-document-tracking-site"></a>Journalisation de l’utilisation du site de suivi des documents

Dans les fichiers journaux d’utilisation, deux champs s’appliquent au suivi des documents : **AdminAction** et **ActingAsUser**.

**AdminAction** Ce champ a la valeur True quand un administrateur utilise le site de suivi des documents en mode Administrateur, par exemple pour révoquer un document au nom d’un utilisateur ou pour voir quand il a été partagé. Ce champ est vide quand un utilisateur se connecte au site de suivi des documents.

**ActingAsUser**: Quand le champ AdminAction a la valeur True, ce champ contient le nom de l’utilisateur au nom duquel l’administrateur agit (comme propriétaire du document ou utilisateur recherché). Ce champ est vide quand un utilisateur se connecte au site de suivi des documents. 

Il existe également des types de demandes qui journalisent la façon dont les utilisateurs et les administrateurs utilisent le site de suivi des documents. Par exemple, **RevokeAccess** est le type de demande quand un utilisateur (ou un administrateur au nom d’un utilisateur) a révoqué un document dans le site de suivi des documents. Utilisez ce type de demande conjointement avec le champ AdminAction pour déterminer si l’utilisateur a révoqué son propre document (le champ AdminAction est vide) ou si un administrateur a révoqué un document au nom d’un d’utilisateur (AdminAction a la valeur True).

Pour plus d’informations sur la journalisation de l’utilisation, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](../log-analyze-usage.md)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez configuré le site de suivi des documents pour le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

