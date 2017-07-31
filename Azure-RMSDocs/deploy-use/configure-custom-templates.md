---
title: "Configurer des modèles personnalisés pour Azure RMS - AIP"
description: "Informations et instructions destinées aux administrateurs souhaitant configurer et gérer des modèles de droits d’utilisation. Grâce aux modèles, les utilisateurs et autres administrateurs peuvent appliquer facilement des stratégies à des fichiers sensibles qui limitent l’accès aux utilisateurs autorisés."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6c3f066a373d253d8488c805828a65513370e3a4
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2017
---
# <a name="configuring-custom-templates-for-the-azure-rights-management-service"></a>Configuration de modèles personnalisés pour le service Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Une fois que le service Azure Rights Management a été [activé](activate-service.md), les utilisateurs peuvent utiliser automatiquement deux modèles par défaut. Ces modèles leur permettent d’appliquer facilement des stratégies de gestion des droits à des fichiers sensibles qui limitent l’accès aux utilisateurs autorisés de votre organisation. Ces deux modèles incluent les restrictions de stratégie de droits suivantes :

-   Affichage en lecture seule du contenu protégé

    -   Nom d’affichage : **&lt;nom de l’organisation&gt; - Affichage confidentiel uniquement** ou **Hautement confidentiel \ Tous les employés**

    -   Autorisation spécifique : Afficher le contenu

-   Autorisations de lecture ou de modification du contenu protégé

    -   Nom d’affichage : **&lt;nom de l’organisation&gt; - Confidentiel** ou **Confidentiel \ Tous les employés**

    -   Autorisations spécifiques : Afficher le contenu, Enregistrer le fichier, Modifier le contenu, Afficher les droits affectés, Autoriser les macros, Transférer, Répondre, Répondre à tous

En outre, le [client Azure Information Protection ](../rms-client/aip-client.md) permet aux utilisateurs de définir leur propre jeu d’autorisations. Et pour le client Outlook et Outlook Web Access, les utilisateurs peuvent sélectionner l’option [Ne pas transférer](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails).

Les modèles par défaut peuvent suffire à de nombreuses organisations. Mais si vous souhaitez créer vos propres modèles de stratégie de droits personnalisés, rien ne vous empêche de le faire. Les raisons justifiant la création d'un modèle personnalisé sont les suivantes :

-   Vous voulez un modèle pour octroyer des droits à un sous-ensemble d'utilisateurs au sein de l'organisation plutôt qu'à tous les utilisateurs.

-   Vous voulez que seul un sous-ensemble d'utilisateurs, plutôt que tous les utilisateurs de l'organisation, puissent afficher et sélectionner un modèle (modèle départemental) à partir d'applications.

-   Vous voulez définir des droits personnalisés pour un modèle, par exemple Affichage et Modification, mais pas Copie et Impression.

-   Vous voulez configurer d'autres options dans un modèle, notamment une date d'expiration et l'accessibilité du contenu sans connexion Internet.

Pour que les utilisateurs puissent sélectionner un modèle personnalisé qui contient des paramètres comme ceux-là, vous devez d'abord créer un modèle personnalisé, le configurer, puis le publier. Même si vous n’aurez probablement besoin que de quelques modèles, vous pouvez enregistrer au maximum 500 modèles personnalisés dans Azure. 

Utilisez les informations suivantes pour vous aider à configurer et utiliser des modèles personnalisés :

-   [Comment créer, configurer et publier un modèle personnalisé](create-template.md)

-   [Comment copier un modèle](copy-template.md)

-   [Comment supprimer (archiver) des modèles](remove-template.md)

-   [Comment actualiser les modèles pour les utilisateurs](refresh-templates.md)

-   [Utiliser PowerShell pour gérer les modèles](configure-templates-with-powershell.md)

> [!TIP]
> Les modèles et de nouvelles options de configuration de la protection Gestion des droits Azure sont déplacés vers le portail Azure. Cette fonctionnalité est actuellement en version préliminaire. Pour plus d’informations, consultez l’annonce de blog suivante : [L’administration unifiée d’Azure Information Protection est maintenant disponible en préversion](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/) 


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

