---
title: "Suivi des documents pour Azure Information Protection"
description: Instructions et informations pour les administrateurs pour configurer et utiliser le suivi des documents pour Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: f47b177ece91f775d53c72d379d6ffa3a2f3c98b
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="configuring-and-using-document-tracking-for-azure-information-protection"></a>Configuration et utilisation du suivi des documents pour Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

Si votre [abonnement prend en charge le suivi des documents](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), le site de suivi des documents est activé par défaut pour tous les utilisateurs de votre organisation. Le suivi des documents fournit des informations telles que les adresses de messagerie des personnes qui ont tenté d'accéder aux documents protégés que les utilisateurs ont partagés et indique quand ces personnes ont tenté d'y accéder, ainsi que leur emplacement. Si l’affichage de ces informations est interdit dans votre organisation pour des raisons de confidentialité, vous pouvez désactiver l’accès au site de suivi des documents à l’aide de l’applet de commande [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). Vous pouvez réactiver l’accès au site à tout moment en utilisant [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) et vérifier si l’accès est actuellement activé ou désactivé à l’aide de [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

Pour exécuter ces applets de commande, vous devez disposer au moins de la version **2.3.0.0** du module Azure Rights Management pour Windows PowerShell. Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

> [!TIP]
> Si vous avez précédemment téléchargé et installé le module, vérifiez le numéro de version en exécutant la commande suivante : `(Get-Module aadrm –ListAvailable).Version`

Les URL suivantes sont utilisées pour le suivi des documents et doivent être autorisées (par exemple, ajoutez-les à vos sites approuvés si vous utilisez Internet Explorer avec sécurité renforcée) :

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > Cette URL est pour Bing Maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## <a name="tracking-and-revoking-documents-for-users"></a>Suivi et révocation de documents pour les utilisateurs

Quand les utilisateurs se connectent au site de suivi des documents, ils peuvent suivre et révoquer des documents qu’ils ont protégés à l’aide du client Azure Information Protection, ou qu’ils ont partagés à l’aide de l’application de partage RMS. Lorsque vous vous connectez comme administrateur pour Azure Information Protection (administrateur général), vous pouvez cliquer sur l’icône Administrateur pour passer en mode Administrateur et afficher les documents partagés par les utilisateurs de votre organisation :

![Icône Administrateur du site de suivi de document](../media/tracking-site-admin-icon.png)

Les actions que vous prenez en mode Administrateur sont auditées et consignées dans les fichiers journaux d’utilisation, et vous devez confirmer pour continuer. Pour plus d’informations sur la journalisation, consultez la section suivante.

Quand vous êtes en mode Administrateur, vous pouvez lancer une recherche par utilisateur ou par document. Une recherche par utilisateur affiche tous les documents partagés par l’utilisateur spécifié. Une recherche par document affiche tous les utilisateurs de votre organisation qui ont partagé ce document. Vous pouvez ensuite affiner les résultats de la recherche pour effectuer le suivi des documents partagés par les utilisateurs et, si nécessaire, les révoquer. 

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

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
