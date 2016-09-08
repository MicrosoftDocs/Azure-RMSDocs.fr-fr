---
title: "Application de partage Rights Management &colon; Historique de publication des versions | Azure RMS"
description: "L’équipe Rights Management met régulièrement à jour l’application de partage du même nom à l’aide de correctifs et de nouvelles fonctionnalités. Pour déterminer les nouveautés ou modifications apportées à une version, utilisez les informations suivantes. La dernière version est répertoriée en première position."
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 060324fd6f0a87839ff267b540b9e5024498c242


---

# Application de partage Rights Management : Historique de publication des versions

>*S’applique à : Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

L’équipe Rights Management met régulièrement à jour l’application de partage du même nom à l’aide de correctifs et de nouvelles fonctionnalités. Pour déterminer les nouveautés ou modifications apportées à une version, utilisez les informations suivantes. La dernière version est répertoriée en première position.

Les versions antérieures au 1er janvier 2015 ne sont pas répertoriées.

> [!NOTE]
> Si vous avez des commentaires ou une question concernant l’application de partage RMS, envoyez un message électronique à [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question).

## Version 1.0.2217.0

**Publiée le** : 13/07/2016

**Correctifs** :

- Les utilisateurs des organisations qui utilisent la fédération et l’authentification multifacteur ne reçoivent plus l’erreur 0x800704DC quand ils protègent du contenu.



## Version 1.0.2191.0
**Publiée le** : 16/06/2016

**Correctifs** :

- Le site de suivi des documents affiche maintenant le nombre correct d’affichages pour chaque document suivi.

- Les modèles pour tous les paramètres régionaux sont désormais affichés comme étant disponibles pour les utilisateurs.

- Après avoir utilisé le partage protégé pour un fichier PowerPoint, les modifications apportées à la version locale du fichier sont désormais enregistrées correctement.

- Petit nombre de bogues mineurs et améliorations pour les messages d’erreur.


## Version 1.0.2004.0
**Publiée le** : 11/12/2015

**Correctifs** :

-   Seuls le propriétaire du fichier et les personnes avec des niveaux d’autorisation de **copropriétaire** peuvent ôter la protection des fichiers. Auparavant, le propriétaire et les personnes avec des niveaux d’autorisation de **coauteur** et de **copropriétaire** pouvaient ôter la protection de fichiers.

-   Protection native pour les fichiers **.tif** (en plus des fichiers .tiff), pour produire un fichier **.ptif** en lecture seule protégé par RMS.

-   Améliorations pour les messages d’erreur (précision et clarté).

-   Amélioration des performances de chiffrement et de déchiffrement de contenu.

**Nouvelles fonctionnalités** :

-   Prise en charge de l’installation sans intervention de l’administrateur, afin que des utilisateurs standard puissent installer l’application de partage RMS.

    Certaines restrictions s’appliquent aux utilisateurs standards exécutant Office 2010. Pour plus d’informations, consultez la section [Si vous n’êtes pas un administrateur local et que vous utilisez Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010) dans les instructions de l’utilisateur [Télécharger et installer l’application de partage Rights Management](install-sharing-app.md).

## Version 1.0.1908.0
**Publiée le** : 16/9/2015

**Correctifs** :

-   Prise en charge de Multi-Factor Authentication (MFA) pour Azure RMS, ayant également pour effet d’éliminer la dépendance vis-à-vis de l’Assistant de connexion Microsoft pour les applications qui utilisent l’authentification moderne.

    Pour plus d’informations, consultez la section [Multi-Factor authentication (MFA) et Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) à partir de [Configuration requise pour Azure Rights Management](../get-started/requirements-azure-rms.md).

## Version 1.0.1784.0
**Publiée le** : 30/7/2015

**Correctifs** :

-   La valeur par défaut de l’intervalle d’actualisation pour les modèles de stratégie des droits est réduite de 7 à 1 jour.

-   Petit nombre de bogues mineurs et régressions.

## Version 1.0.1770.0
**Publiée le** : 25/4/2015

**Correctifs** :

-   Désormais, seul le propriétaire et les copropriétaires d’un fichier peuvent supprimer sa protection. Des coauteurs ne le peuvent pas.

-   Des fichiers se trouvant sur un partage réseau peuvent désormais être protégés.

**Nouvelles fonctionnalités** :

-   Prise en charge du suivi et de la révocation de documents. Pour plus d’informations, consultez [Suivre et révoquer vos documents lorsque vous utilisez l’application de partage RMS](sharing-app-track-revoke.md).

-   Prise en charge de modèle lorsque vous choisissez **Partage protégé**:

    -   Vous pouvez désormais sélectionner des modèles.

    -   À la place du curseur, vous voyez une zone de liste contenant des modèles et des autorisations personnalisées.

    -   Vous ne voyez plus les options **Autoriser l’utilisation sur tous les périphériques** et **Appliquer les restrictions d’utilisation**. Au lieu de cela, l’option **Protection générique** est automatiquement sélectionnée en fonction du type de fichier.

    Pour plus d’informations, consultez [Options de boîte de dialogue pour l’application de partage Rights Management](sharing-app-dialog-box.md).

## Version 1.0.1667.0
**Publiée le** : 19/1/2015

**Correctifs** :

-   Prise en charge des polices de caractères chinois dans la visionneuse PPDF de l’application de partage RMS.

-   Gestion des erreurs et messagerie améliorées.

-   Résolution d’un problème lié à la notification automatique de mise à jour quand une version plus récente de l’application est disponible en téléchargement.

**Nouvelles fonctionnalités** :

-   **Prise en charge pour plusieurs domaines de messagerie dans votre organisation** : Si vous utilisez AD RMS et que des utilisateurs au sein de votre organisation disposent de plusieurs domaines de messagerie, cette mise à jour leur permet de consommer du contenu protégé par des utilisateurs d’autres domaines au sein de votre organisation. Pour plus d’informations, consultez la section [AD RMS uniquement : Prise en charge de plusieurs domaines de messagerie au sein de votre organisation](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization) du [Guide de l’administrateur de l’application de partage Rights Management](sharing-app-admin-guide.md).




<!--HONumber=Aug16_HO4-->


