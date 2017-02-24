---
title: "Configuration de modèles personnalisés pour le service Azure Rights Management | Azure Information Protection"
description: "Informations et instructions destinées aux administrateurs souhaitant configurer et gérer des modèles de droits d’utilisation. Grâce aux modèles, les utilisateurs et autres administrateurs peuvent appliquer facilement des stratégies à des fichiers sensibles qui limitent l’accès aux utilisateurs autorisés."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: efab4cdc455237b4bb064252dfe6702ec40539d2
ms.openlocfilehash: a5a27e9d1d12381b7c4c945596480171f7265552


---

# <a name="configuring-custom-templates-for-the-azure-rights-management-service"></a>Configuration de modèles personnalisés pour le service Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Une fois [activé](activate-service.md) le service Azure Rights Management, les utilisateurs peuvent automatiquement utiliser les deux modèles par défaut qui leur facilitent l’application de stratégies de gestion des droits aux fichiers sensibles pour en restreindre l’accès aux utilisateurs autorisés de votre organisation. Ces deux modèles incluent les restrictions de stratégie de droits suivantes :

-   Affichage en lecture seule du contenu protégé

    -   Nom d’affichage : **&lt;nom de l’organisation&gt; - Affichage confidentiel uniquement**

    -   Autorisation spécifique : Afficher le contenu

-   Autorisations de lecture ou de modification du contenu protégé

    -   Nom d’affichage : **&lt;nom de l’organisation&gt; - Confidentiel**

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]




<!--HONumber=Feb17_HO2-->


