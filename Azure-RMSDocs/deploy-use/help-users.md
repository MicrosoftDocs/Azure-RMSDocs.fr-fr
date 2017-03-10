---
title: "Aider les utilisateurs à protéger des fichiers à l’aide d’Azure RMS - AIP"
description: "Informations vous permettant de fournir de l’aide aux utilisateurs, aux administrateurs et au support technique après le déploiement et la configuration du service Azure Rights Management d’Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b5dfe6e4c77a9b22e98cb2b7997a744730caac1
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Après avoir déployé et configuré Azure Information Protection pour votre organisation, vous pouvez fournir de l’aide et des instructions aux utilisateurs, aux administrateurs et au support technique :

-   **Informations pour les utilisateurs finaux :**

    Expliquez à vos utilisateurs comment et quand protéger des documents et messages électroniques contenant des informations sensibles. Autant que possible, fournissez ces informations pour leurs flux de travail existants afin qu’ils puissent intégrer les étapes supplémentaires à un processus déjà familier, au lieu d’introduire des processus entièrement nouveaux. Pensez à leur faire part des avantages et des risques inhérents à votre activité et proposez-leur des conseils sur la protection des fichiers et des messages électroniques. Si vous avez configuré des [modèles personnalisés](configure-custom-templates.md), fournissez des instructions concernant le modèle à sélectionner si le nom et la description des modèles ne suffisent pas à identifier le bon modèle.

    > [!TIP]
    > Exemples de vidéos à l’attention des utilisateurs finaux :
    >
    > -   [Expérience utilisateur d'Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Révocation et suivi de document Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informations à l'attention des administrateurs :**

    Certaines applications implémentent automatiquement la protection des données à l'aide de stratégies et de paramètres configurés par les administrateurs. Pour ces applications, vous devrez peut-être fournir des instructions aux autres administrateurs qui gèrent ces applications et services. Pour plus d’informations, consultez [Comment les applications prennent en charge le service Azure Rights Management](../understand-explore/applications-support.md) et [Configuration d’applications pour le service Azure Rights Management](configure-applications.md).

-   **Informations de support technique :**

    L'un des outils les plus utiles pour le support technique est l' [Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Les opérateurs du support technique peuvent l'exécuter avec l'option d'administrateur Azure RMS, et demander aux utilisateurs de l'exécuter avec l'option d'utilisateur Azure RMS. Cet outil permet, non seulement d'identifier des problèmes, mais également de les résoudre ou, à défaut, d'enregistrer des journaux de suivi.
    
    Si des utilisateurs exécutent le client Azure Information Protection, les opérateurs du support technique peuvent leur demander d’utiliser l’option **Aide et commentaires**, **Exécuter les diagnostics**, puis de réinitialiser le client. Toutefois, contrairement à l’Analyseur RMS, la réinitialisation ne déconnecte pas l’utilisateur ou n’effectue aucun rebootstrap du client, et aucune mise à jour automatique n’a lieu.

    S’il existe des demandes légitimes d’obtention de droits d’accès complets à des documents protégés, par exemple une demande émanant du service juridique ou d’un responsable après qu’un employé a quitté l’organisation, vérifiez que le support technique dispose des processus nécessaires pour effectuer une telle demande à l’aide de la [fonctionnalité de super utilisateur](configure-super-users.md) d’Azure Rights Management.

    Voici en outre quelques-uns des problèmes classiques que des utilisateurs pourraient signaler :

    -   **Aide à la connexion :**

        Les utilisateurs peuvent être invités à fournir des informations d’identification quand le service Azure Rights Management doit authentifier un utilisateur et qu’il ne peut pas utiliser les informations d’identification mises en cache. Il s’agira du compte professionnel ou scolaire de l’utilisateur et du mot de passe associé à votre client Office 365 ou Azure Active Directory. Ce ne peut pas être un compte Microsoft (anciennement un identifiant Windows Live ID) ou un compte de messagerie personnel, car ceux-ci ne sont pas encore pris en charge par le service Azure Rights Management. Proposez aux utilisateurs et au support technique des instructions sur le compte à utiliser quand des utilisateurs sont invités à entrer des informations d’identification pendant l’utilisation de ces applications avec le service Azure Rights Management.

    -   **Problèmes de protection ou de consommation de contenu :**

        Assurez-vous que les utilisateurs disposent d’instructions appropriées pour les applications qu’ils utilisent, et se servent d’applications et d’appareils pris en charge par le service Azure Rights Management. Pour plus d’informations sur les appareils et les applications pris en charge, consultez [Configuration requise pour Azure Rights Management](../get-started/requirements-azure-rms.md).

        Si des utilisateurs voient une erreur quand ils tentent de protéger ou de consommer du contenu, demandez-leur d'exécuter l' [Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437) en tant qu'utilisateur d'Azure RMS.

        Si des utilisateurs signalent qu'ils peuvent ouvrir du contenu protégé mais ne disposent pas des droits nécessaires, demandez-leur d'exécuter l' [Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437) en tant qu'utilisateur d'Azure RMS, et de télécharger et afficher les modèles. Cela confirme qu'ils ont correctement téléchargé les modèles, et les droits que les modèles fournissent. Le problème peut être que l'utilisateur ne fait pas partie du groupe approprié configuré pour le modèle, ou que le modèle doit être reconfiguré pour l'utilisateur.

Utilisez les sections suivantes pour obtenir des informations spécifiques aux applications afin d'aider les utilisateurs à protéger les documents et les messages électroniques contenant des informations sensibles.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Utilisation de la protection des informations avec le client Azure Information Protection
Le client Azure Information Protection peut être requis pour que les utilisateurs sous Office 2010 protègent et utilisent des documents et des e-mails protégés, mais il est également recommandé pour les ordinateurs et appareils mobiles.

En plus d’aider les utilisateurs à protéger des documents importants, le client Azure Information Protection permet aux utilisateurs de suivre les documents qu’ils ont protégés et, si nécessaire, de révoquer l’accès à ceux-ci.

Pour savoir comment utiliser ce client pour les ordinateurs Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](../rms-client/client-user-guide.md).


## <a name="using-information-protection-with-office-365-office-2016-or-office-2013"></a>Utilisation de la protection des informations avec Office 365, Office 2016 ou Office 2013
Si vous utilisez le service Azure Rights Management et que vous n’avez pas installé le client Azure Information Protection, les utilisateurs ne voient pas la barre Azure Information Protection dans leurs applications de bureau Office, le bouton **Protéger** sur le ruban, ni l’option **Classifier et protéger** dans l’Explorateur de fichiers qui simplifie la protection des fichiers. Ces utilisateurs doivent suivre des instructions similaires aux suivantes.

> [!TIP]
> Pour trouver de l’aide et des instructions spécifiques à une application qui ont trait à l’utilisation de la protection des données avec ces applications, recherchez **IRM**, ainsi que le nom et la version de l’application.

#### <a name="to-protect-a-document-in-word-2013"></a>Pour protéger un document dans Word 2013

1.  Dans Microsoft Word, créez un document.

2.  À partir du menu **Fichier** , cliquez sur **Info**, sur **Protéger le Document**, sur **Restreindre l’accès**, puis choisissez un modèle pour appliquer rapidement les droits d’utilisation appropriés ou sélectionnez **Restreindre l’accès** et sélectionnez vous-même les droits d’utilisation.

    > [!NOTE]
    > Si vous utilisez Rights Management pour la première fois, contactez le service [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Vous serez invité à entrer des informations d’identification pour configurer le client IRM Office.

3.  Enregistrez le document.

Lorsque d'autres personnes ouvriront le document, ils devront d'abord être authentifiés. S'ils ne reçoivent pas l'autorisation pour ouvrir le document, ce dernier ne s'ouvrira pas. S'ils sont autorisés à ouvrir le document, ce dernier s'ouvrira avec les droits d'utilisation restreints qui ont été définis pour cet utilisateur. Par exemple, un droit d'utilisation Affichage uniquement ne permet pas à l'utilisateur de modifier ou d'enregistrer le document, même si ce dernier est d'abord copié vers un autre emplacement. Les droits d'utilisation sont affichés en haut du document grâce à une bannière de restriction. La bannière peut afficher les autorisations appliquées au document, ou un lien pour afficher celles-ci.

#### <a name="to-protect-an-email-message-using-outlook-2013-and-exchange-online"></a>Pour protéger un message électronique à l'aide d'Outlook 2013 et d'Exchange Online

1.  Dans Outlook, créez un message électronique destiné à une personne au sein de votre organisation.

2.  À partir de l’onglet **OPTIONS** , cliquez sur **Autorisation**, puis sélectionnez une option. Par exemple : **Ne pas transférer**, **&lt;Nom de la société&gt; - Confidentiel** ou **&lt;Nom de la société&gt; - Affichage confidentiel uniquement**.

3.  Envoyez le message.

Comme pour l'affichage d'un document protégé, lorsque les destinataires reçoivent le message électronique, ceux-ci sont tout d'abord authentifiés. S'ils sont autorisés à afficher le message électronique, ce dernier s'ouvrira avec les droits d'utilisation restreints qui ont été définis pour cet utilisateur. Par exemple, si vous avez sélectionné **Ne pas transférer**, le bouton Transférer sur le ruban n’est pas disponible.

#### <a name="to-protect-an-email-message-using-the-outlook-web-app"></a>Pour protéger un message électronique à l'aide d'Outlook Web App

1.  Dans Outlook Web App, créez un message électronique destiné à une personne au sein de votre organisation.

2.  Cliquez sur  **…**, puis sur **Définir l’autorisation**et sélectionnez une option. Par exemple : **Ne pas transférer**, **Ne pas répondre à tous**, **&lt;Nom de la société&gt; - Confidentiel** ou **&lt;Nom de la société&gt; - Affichage confidentiel uniquement**.

3.  Envoyez le message.

Comme pour l'affichage d'un document protégé, lorsque les destinataires reçoivent le message électronique, ceux-ci sont tout d'abord authentifiés. S'ils sont autorisés à afficher le message électronique, ce dernier s'ouvrira avec les droits d'utilisation restreints qui ont été définis pour cet utilisateur. Par exemple, si vous avez sélectionné **Ne pas répondre à tous**, l’option **RÉPONDRE À TOUS** dans la fenêtre du message ne sera pas disponible.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

