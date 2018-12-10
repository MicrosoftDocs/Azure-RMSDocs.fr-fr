---
title: Aider les utilisateurs à protéger des fichiers à l’aide d’Azure RMS - AIP
description: Informations vous permettant de fournir de l’aide aux utilisateurs, aux administrateurs et au support technique après le déploiement et la configuration du service Azure Rights Management d’Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/06/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 43bc10ce43a4ba7a26958e562c4acc6e245ad76a
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53024074"
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Après avoir déployé et configuré Azure Information Protection pour votre organisation, vous pouvez fournir de l’aide et des instructions aux utilisateurs, aux administrateurs et au support technique :

-   **Informations à l’attention des utilisateurs finaux**
    
    Expliquez à vos utilisateurs comment et quand protéger des documents et messages électroniques contenant des informations sensibles. Autant que possible, fournissez ces informations pour leurs flux de travail existants afin qu’ils puissent intégrer les étapes supplémentaires à un processus déjà familier, au lieu d’introduire des processus nouveaux. Pensez à leur faire part des avantages et des risques inhérents à votre activité et proposez-leur des conseils sur la protection des fichiers et des messages électroniques. Si vous avez configuré des [modèles](configure-policy-templates.md), fournissez des instructions concernant le modèle à sélectionner si le nom et la description des modèles ne suffisent pas à identifier le bon modèle.
    
    > [!TIP]
    > Exemples de vidéos à l’attention des utilisateurs finaux :
    > -   [Microsoft Azure Information Protection](https://youtu.be/ToShAUdlrPo?list=PL8nfc9haGeb6qSm1kLU8n3Zqg398764h5)
    > -   [Révocation et suivi de document Azure RMS](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informations à l’attention des administrateurs**
    
    Certaines applications implémentent automatiquement la protection des données à l'aide de stratégies et de paramètres configurés par les administrateurs. Pour ces applications, vous devrez peut-être fournir des instructions aux autres administrateurs qui gèrent ces applications et services. 
    
    Pour plus d’informations, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md) et [Configuration d’applications pour le service Azure Rights Management](configure-applications.md).
    
-   **Informations de support technique**
    
    Si les utilisateurs disposent du client Azure Information Protection, les opérateurs du support technique peuvent leur demander d’utiliser l’option **Aide et commentaires** pour savoir si l’édition d’Office prend ou non en charge la protection et obtenir le compte d’utilisateur actuellement connecté. Vous pouvez également utiliser cette option pour collecter des fichiers journaux et réinitialiser le client. Pour plus d’informations, consultez le guide de l’administrateur : [Vérifications et résolution des problèmes liés à l’installation](./rms-client/client-admin-guide.md#installation-checks-and-troubleshooting).
    
    S’il existe des demandes légitimes d’obtention de droits d’accès complets à des documents protégés, vérifiez que le support technique dispose des processus nécessaires pour effectuer une telle demande à l’aide de la [fonctionnalité de super utilisateur](configure-super-users.md) d’Azure Rights Management. Par exemple, ces demandes peuvent émaner du service juridique ou d’un responsable après le départ d’un employé.
    
    Voici en outre certaines catégories de problèmes que les utilisateurs peuvent signaler :
    
    - **Aide à la connexion**
        
        Les utilisateurs peuvent être invités à fournir des informations d’identification quand le service Azure Rights Management doit authentifier un utilisateur et qu’il ne peut pas utiliser les informations d’identification mises en cache. Les informations d’identification nécessaires correspondent généralement au compte professionnel ou scolaire de l’utilisateur et au mot de passe associé au client (tenant) Office 365 ou Azure Active Directory. Même si le service Azure Rights Management peut authentifier des comptes Azure AD, certaines applications peuvent également ouvrir du contenu protégé lorsqu’un compte Microsoft est utilisé pour l’authentification. [Plus d’informations](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 
        
        Donnez aux utilisateurs et au support technique des instructions sur le compte à utiliser quand des utilisateurs sont invités à entrer des informations d’identification quand ils ont des applications utilisant le service Azure Rights Management.
        
    - **Problèmes de protection ou de consommation de contenu**
        
        Vérifiez que les utilisateurs disposent d’instructions appropriées pour les applications qu’ils utilisent, et se servent d’applications et d’appareils pris en charge par le service Azure Rights Management. Pour plus d’informations sur les appareils et les applications pris en charge, consultez [Configuration requise pour Azure Rights Management](requirements.md).
        
        Pour vérifier qu’un utilisateur ou un groupe est autorisé par Azure Active Directory à protéger ou à utiliser du contenu protégé, servez-vous des vérifications mentionnées dans la rubrique [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).
        
        Si un utilisateur vous signale qu’il peut ouvrir du contenu protégé alors qu’il n’a pas les autorisations nécessaires, il est possible que l’utilisateur ne soit pas dans le bon groupe configuré pour le modèle Rights Management. Il est également possible que le [modèle doive être reconfiguré](configure-policy-templates.md) pour l’utilisateur ou le groupe. 
        
        Si les droits dont disposent les utilisateurs ne sont pas ceux attendus, vérifiez leur description et les implémentations spécifiques à l’application dans le [tableau des droits d’utilisation](configure-usage-rights.md#usage-rights-and-descriptions).

Utilisez les sections suivantes pour obtenir des informations spécifiques aux applications afin d’aider les utilisateurs à protéger les documents et les e-mails.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Utilisation de la protection des informations avec le client Azure Information Protection

Si les utilisateurs disposent d’Office 2010, le client Azure Information Protection (ou l’ancienne application, c’est-à-dire l’application de partage RMS) est nécessaire pour protéger et utiliser des documents et des e-mails protégés. Cependant, le client Azure Information Protection est recommandé pour tous les ordinateurs et appareils mobiles qui prennent en charge ce service.

En plus d’aider les utilisateurs à protéger des documents et des e-mails, le client Azure Information Protection leur permet d’effectuer le suivi des documents qu’ils ont protégés. Les documents suivis peuvent également être révoqués si les utilisateurs précédemment autorisés ne doivent plus y avoir accès.

Pour savoir comment utiliser ce client pour les ordinateurs Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](./rms-client/client-user-guide.md).


## <a name="using-information-protection-with-office365-office-2016-or-office2013"></a>Utilisation de la protection des informations avec Office 365, Office 2016 ou Office 2013
Si vous utilisez le service Azure Rights Management et que vous n’avez pas installé le client Azure Information Protection, les utilisateurs ne voient pas la barre Azure Information Protection dans leurs applications Office pour poste de travail. Ils ne voient pas non plus le bouton **Protéger** sur le ruban, ni **Classer et protéger** dans l’Explorateur de fichiers. Ces ajouts facilitent la protection des documents et des e-mails. Ces utilisateurs doivent suivre des instructions similaires aux suivantes.

> [!TIP]
> Pour trouver de l’aide et des instructions spécifiques à une application qui ont trait à l’utilisation de la protection des données avec ces applications, recherchez **IRM**, ainsi que le nom et la version de l’application.

#### <a name="to-protect-a-document-in-word2013"></a>Pour protéger un document dans Word 2013

1.  Dans Microsoft Word, créez un document.

2.  Dans le menu **Fichier**, cliquez sur **Info**, cliquez sur **Protéger le document**, puis cliquez sur **Restreindre l’accès**.

3. Choisissez un modèle pour appliquer rapidement les droits d’utilisation appropriés ou sélectionnez **Restreindre l’accès** et sélectionnez vous-même les droits d’utilisation.

    > [!NOTE]
    > Si vous utilisez Rights Management pour la première fois sur votre ordinateur, l’option **Restreindre l’accès** va se connecter au service Azure Rights Management et vous serez invité à entrer vos informations d’identification pour configurer le client IRM Office. Vous pouvez ensuite choisir un modèle ou des droits d’utilisation.

3.  Enregistrez le document.

Lorsque d'autres personnes ouvriront le document, ils devront d'abord être authentifiés. S'ils ne reçoivent pas l'autorisation pour ouvrir le document, ce dernier ne s'ouvrira pas. S’ils sont autorisés à ouvrir le document, ce dernier s’ouvrira avec les [droits d’utilisation](configure-usage-rights.md) restreints qui ont été définis pour cet utilisateur. 

Par exemple, un droit d'utilisation Affichage uniquement ne permet pas à l'utilisateur de modifier ou d'enregistrer le document, même si ce dernier est d'abord copié vers un autre emplacement. 

Les droits d'utilisation sont affichés en haut du document grâce à une bannière de restriction. La bannière peut afficher les autorisations appliquées au document, ou un lien pour afficher celles-ci.

#### <a name="to-protect-an-email-message-using-outlook2013-and-exchange-online"></a>Pour protéger un message électronique à l'aide d'Outlook 2013 et d'Exchange Online

1.  Dans Outlook, créez un e-mail adressé à un destinataire au sein de votre organisation.

2.  À partir de l’onglet **OPTIONS** , cliquez sur **Autorisation**, puis sélectionnez une option. Par exemple : **Ne pas transférer**, **\<Nom de la société>- Confidentiel** ou **\<Nom de la société>- Affichage confidentiel uniquement**.

3.  Envoyez le message.

Comme pour l’affichage d’un document protégé, lorsque les destinataires ouvrent l’e-mail protégé, ceux-ci sont tout d’abord authentifiés. S’ils sont autorisés à afficher le message électronique, ce dernier s’ouvrira avec les [droits d’utilisation](configure-usage-rights.md) restreints qui ont été définis pour cet utilisateur. 

Par exemple, si l’e-mail est protégé à l’aide de l’option **Ne pas transférer**, le bouton Transférer n’est pas disponible dans le ruban.

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>Pour protéger un e-mail à l’aide d’Outlook sur le web

1.  Dans Outlook sur le web, créez un e-mail destiné à une personne de votre organisation.

2.  Cliquez sur  **…**, puis sur **Définir l’autorisation**et sélectionnez une option. Par exemple : **Ne pas transférer** ou **Ne pas répondre à tous**. Ou **\<Nom de la société> - Confidentiel** ou **\<Nom de la société> - Affichage confidentiel uniquement**.

3.  Envoyez le message.

Comme pour un document protégé, les destinataires sont authentifiés avant de pouvoir ouvrir l’e-mail. S’ils sont autorisés à afficher le message électronique, ce dernier s’ouvrira avec les [droits d’utilisation](configure-usage-rights.md) restreints qui ont été définis pour cet utilisateur. 

Par exemple, si vous avez sélectionné **Ne pas répondre à tous**, l’option **RÉPONDRE À TOUS** dans la fenêtre du message ne sera pas disponible.


