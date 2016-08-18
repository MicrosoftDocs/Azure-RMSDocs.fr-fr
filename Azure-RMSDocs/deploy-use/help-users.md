---
# required metadata

title: Aider les utilisateurs à protéger des fichiers en utilisant Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Aide aux utilisateurs sur la protection de fichiers grâce à Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Après avoir déployé et configuré Azure Rights Management (Azure RMS) pour votre organisation, fournissez de l'aide et des instructions aux utilisateurs, aux administrateurs et au support technique :

-   **Informations pour les utilisateurs finaux :**

    Expliquez à vos utilisateurs comment et quand protéger des documents et messages électroniques contenant des informations sensibles. Autant que possible, fournissez ces informations pour leurs flux de travail existants afin qu'ils puissent intégrer les étapes supplémentaires dans un processus déjà familier, au lieu d'introduire des processus entièrement nouveaux. Pensez à leur faire part des avantages et des risques inhérents à votre activité et proposez-leur des conseils sur la protection des fichiers et des messages électroniques. Si vous avez configuré des [modèles personnalisés](configure-custom-templates.md), fournissez des instructions concernant le modèle à sélectionner si le nom et la description des modèles ne suffisent pas à identifier le bon modèle.

    > [!TIP] Exemples de vidéos à l’attention des utilisateurs finaux :
    >
    > -   [Expérience utilisateur d'Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Suivi et révocation de documents Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informations à l'attention des administrateurs :**

    Certaines applications implémentent automatiquement la protection des données à l'aide de stratégies et de paramètres configurés par les administrateurs. Pour ces applications, vous devrez peut-être fournir des instructions aux autres administrateurs qui gèrent ces applications et services. Pour plus d’informations, consultez [Comment les applications prennent en charge Azure Rights Management](../understand-explore/applications-support.md) et [Configuration d’applications pour Azure Rights Management](configure-applications.md).

-   **Informations de support technique :**

    L'un des outils les plus utiles pour le support technique est l' [Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Les opérateurs du support technique peuvent l'exécuter avec l'option d'administrateur Azure RMS, et demander aux utilisateurs de l'exécuter avec l'option d'utilisateur Azure RMS. Cet outil permet, non seulement d'identifier des problèmes, mais également de les résoudre ou, à défaut, d'enregistrer des journaux de suivi.

    S’il existe des demandes légitimes d’obtention de droits d’accès complets à des documents protégés, par exemple une demande émanant du service juridique ou d’un responsable après qu’un employé a quitté l’organisation, vérifiez que le support technique dispose des processus nécessaires pour effectuer une telle demande à l’aide de la [fonctionnalité de super utilisateur](configure-super-users.md) d’Azure RMS.

    Voici en outre quelques-uns des problèmes classiques que des utilisateurs pourraient signaler :

    -   **Aide à la connexion :**

        Les utilisateurs peuvent être invités à fournir des informations d'identification quand Azure RMS doit authentifier un utilisateur et qu'il ne peut pas utiliser les informations d'identification mises en cache. Il s’agira du compte professionnel ou scolaire de l’utilisateur et du mot de passe associé à votre client Office 365 ou Azure Active Directory. et non d'un compte Microsoft (anciennement un identifiant Windows Live ID) ou d'un compte de messagerie personnel, car ceux-ci ne sont pas encore pris en charge par Azure RMS. Proposez aux utilisateurs et au support technique des instructions sur le compte à utiliser quand des utilisateurs sont invités à entrer des informations d'identification lors de l'utilisation de ces applications avec Azure RMS.

    -   **Problèmes de protection ou de consommation de contenu :**

        Assurez-vous que les utilisateurs disposent d'instructions appropriées pour les applications qu'ils utilisent, et se servent d'applications et d'appareils pris en charge par Azure RMS. Pour plus d’informations sur les appareils et les applications pris en charge, consultez [Configuration requise pour Azure Rights Management](../get-started/requirements-azure-rms.md).

        Si des utilisateurs voient une erreur quand ils tentent de protéger ou de consommer du contenu, demandez-leur d'exécuter l' [Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437) en tant qu'utilisateur d'Azure RMS.

        Si des utilisateurs signalent qu'ils peuvent ouvrir du contenu protégé mais ne disposent pas des droits nécessaires, demandez-leur d'exécuter l' [Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437) en tant qu'utilisateur d'Azure RMS, et de télécharger et afficher les modèles. Cela confirme qu'ils ont correctement téléchargé les modèles, et les droits que les modèles fournissent. Le problème peut être que l'utilisateur ne fait pas partie du groupe approprié configuré pour le modèle, ou que le modèle doit être reconfiguré pour l'utilisateur.

Utilisez les sections suivantes pour obtenir des informations spécifiques aux applications afin d'aider les utilisateurs à protéger les documents et les messages électroniques contenant des informations sensibles.

## Utilisation de la protection des données avec l'application de partage Rights Management
L'application de partage Rights Management (RMS) est nécessaire pour que les utilisateurs puissent protéger du contenu et utiliser du contenu protégé s'ils utilisent Office 2010. Son utilisation est également recommandée pour tous les ordinateurs et appareils mobiles qui prennent en charge Azure RMS.

En plus d'aider les utilisateurs à protéger des documents importants, l'application de partage RMS permet aux utilisateurs de suivre les documents qu'ils ont protégés et, si nécessaire, de révoquer l'accès à ceux-ci.

Pour obtenir des instructions sur l’utilisation de cette application pour les ordinateurs Windows, consultez le [Guide de l’utilisateur de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md).

Pour les appareils mobiles, consultez la [FAQ relative à l’application de partage Microsoft Rights Management pour plateformes mobiles](http://technet.microsoft.com/dn451248).

> [!TIP] Pour obtenir un exemple de scénario complexe avec des captures d’écran, consultez [Partage en toute sécurité de pièces jointes avec des utilisateurs mobiles](../understand-explore/what-admins-users-see.md#users-safely-share-attachments-with-mobile-users).

## Utilisation de la protection des informations avec Office 365, Office 2016 ou Office 2013
Si vous utilisez Azure RMS et que vous n’avez pas installé l’application de partage Rights Management, les utilisateurs ne voient pas le bouton **Partage protégé** sur le ruban ni **Protéger sur place** dans l’Explorateur de fichiers, qui leur permettent de protéger des fichiers plus facilement. Ces utilisateurs doivent suivre des instructions similaires à celle-ci.

> [!TIP] Pour trouver de l’aide et des instructions spécifiques à une application qui ont trait à l’utilisation de la protection des données avec ces applications, recherchez **IRM**, ainsi que le nom et la version de l’application.

#### Pour protéger un document dans Word 2013

1.  Dans Microsoft Word, créez un document.

2.  À partir du menu **Fichier** , cliquez sur **Info**, sur **Protéger le Document**, sur **Restreindre l’accès**, puis choisissez un modèle pour appliquer rapidement les droits d’utilisation appropriés ou sélectionnez **Restreindre l’accès** et sélectionnez vous-même les droits d’utilisation.

    > [!NOTE] Si vous utilisez Rights Management pour la première fois, contactez le service [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Vous serez invité à entrer des informations d’identification pour configurer le client IRM Office.

3.  Enregistrez le document.

Lorsque d'autres personnes ouvriront le document, ils devront d'abord être authentifiés. S'ils ne reçoivent pas l'autorisation pour ouvrir le document, ce dernier ne s'ouvrira pas. S'ils sont autorisés à ouvrir le document, ce dernier s'ouvrira avec les droits d'utilisation restreints qui ont été définis pour cet utilisateur. Par exemple, un droit d'utilisation Affichage uniquement ne permet pas à l'utilisateur de modifier ou d'enregistrer le document, même si ce dernier est d'abord copié vers un autre emplacement. Les droits d'utilisation sont affichés en haut du document grâce à une bannière de restriction. La bannière peut afficher les autorisations appliquées au document, ou un lien pour afficher celles-ci.

#### Pour protéger un message électronique à l'aide d'Outlook 2013 et d'Exchange Online

1.  Dans Outlook, créez un message électronique destiné à une personne au sein de votre organisation.

2.  À partir de l’onglet **OPTIONS** , cliquez sur **Autorisation**, puis sélectionnez une option. Par exemple : **Ne pas transférer**, **&lt;Nom de la société&gt; - Confidentiel** ou **&lt;Nom de la société&gt; - Affichage confidentiel uniquement**.

3.  Envoyez le message.

Comme pour l'affichage d'un document protégé, lorsque les destinataires reçoivent le message électronique, ceux-ci sont tout d'abord authentifiés. S'ils sont autorisés à afficher le message électronique, ce dernier s'ouvrira avec les droits d'utilisation restreints qui ont été définis pour cet utilisateur. Par exemple, si vous avez sélectionné **Ne pas transférer**, le bouton Transférer sur le ruban n’est pas disponible.

#### Pour protéger un message électronique à l'aide d'Outlook Web App

1.  Dans Outlook Web App, créez un message électronique destiné à une personne au sein de votre organisation.

2.  Cliquez sur  **…**, puis sur **Définir l’autorisation**et sélectionnez une option. Par exemple : **Ne pas transférer**, **Ne pas répondre à tous**, **&lt;Nom de la société&gt; - Confidentiel** ou **&lt;Nom de la société&gt; - Affichage confidentiel uniquement**.

3.  Envoyez le message.

Comme pour l'affichage d'un document protégé, lorsque les destinataires reçoivent le message électronique, ceux-ci sont tout d'abord authentifiés. S'ils sont autorisés à afficher le message électronique, ce dernier s'ouvrira avec les droits d'utilisation restreints qui ont été définis pour cet utilisateur. Par exemple, si vous avez sélectionné **Ne pas répondre à tous**, l’option **RÉPONDRE À TOUS** dans la fenêtre du message ne sera pas disponible.




<!--HONumber=Jun16_HO2-->


