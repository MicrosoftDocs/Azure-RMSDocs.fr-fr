---
title: Aider les utilisateurs à protéger des fichiers à l’aide d’Azure RMS - AIP
description: Informations vous permettant de fournir de l’aide aux utilisateurs, aux administrateurs et au support technique après le déploiement et la configuration du service Azure Rights Management d’Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1a52e867d72b2dabc910bfb4e0378c04ed03a5ab
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809507"
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Après avoir déployé et configuré Azure Information Protection pour votre organisation, vous pouvez fournir de l’aide et des instructions aux utilisateurs, aux administrateurs et au support technique :

-   **Informations à l’attention des utilisateurs finaux**
    
    Expliquez à vos utilisateurs comment et quand protéger des documents et messages électroniques contenant des informations sensibles. Autant que possible, fournissez ces informations pour leurs flux de travail existants afin qu’ils puissent intégrer les étapes supplémentaires à un processus déjà familier, au lieu d’introduire des processus nouveaux. Pensez à leur faire part des avantages et des risques inhérents à votre activité et proposez-leur des conseils sur la protection des fichiers et des messages électroniques. 

    Si vous avez le client classique AIP et que vous avez configuré des [modèles](configure-policy-templates.md), fournissez des instructions sur l’option à sélectionner si le nom et la description du modèle ne suffisent pas à en choisir un.
    
    > [!TIP]
    > Exemples de vidéos à l’attention des utilisateurs finaux :
    > -   [Microsoft Azure Information Protection](https://youtu.be/ToShAUdlrPo?list=PL8nfc9haGeb6qSm1kLU8n3Zqg398764h5)
    > -   [Révocation et suivi de document Azure RMS](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informations à l’attention des administrateurs**
    
    Certaines applications implémentent automatiquement la protection des données à l'aide de stratégies et de paramètres configurés par les administrateurs. Pour ces applications, vous devrez peut-être fournir des instructions aux autres administrateurs qui gèrent ces applications et services. 
    
    Pour plus d’informations, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md) et [Configuration d’applications pour le service Azure Rights Management](configure-applications.md).
    
-   **Informations sur le support technique**
    
    Si les utilisateurs disposent du client Azure Information Protection, les opérateurs du support technique peuvent leur demander d’utiliser l’option **Aide et commentaires** pour savoir si l’édition d’Office prend ou non en charge la protection et obtenir le compte d’utilisateur actuellement connecté. Vous pouvez également utiliser cette option pour collecter des fichiers journaux et réinitialiser le client. Pour plus d’informations, consultez le guide de l’administrateur : [Vérifications et résolution des problèmes liés à l’installation](./rms-client/clientv2-admin-guide.md#installation-checks-and-troubleshooting).
    
    S’il existe des demandes légitimes d’avoir un accès complet aux documents protégés, assurez-vous que le support technique a des processus pour demander cet accès à l’aide de la [fonctionnalité de super utilisateur](configure-super-users.md)Azure information protection. Par exemple, ces demandes peuvent émaner du service juridique ou d’un responsable après le départ d’un employé.
    
    Voici en outre certaines catégories de problèmes que les utilisateurs peuvent signaler :
    
    - **Aide sur la connexion**
        
        Les utilisateurs peuvent être invités à fournir des informations d’identification quand le service Azure Rights Management doit authentifier un utilisateur et qu’il ne peut pas utiliser les informations d’identification mises en cache. Les informations d’identification nécessaires correspondent généralement au compte professionnel ou scolaire de l’utilisateur et au mot de passe associé à votre locataire Office 365 ou Azure Active Directory. Même si le service Azure Rights Management peut authentifier des comptes Azure AD, certaines applications peuvent également ouvrir du contenu protégé lorsqu’un compte Microsoft est utilisé pour l’authentification. [Plus d’informations](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 
        
        Donnez aux utilisateurs et au support technique des instructions sur le compte à utiliser quand des utilisateurs sont invités à entrer des informations d’identification quand ils ont des applications utilisant le service Azure Rights Management.
        
    - **Problèmes de protection ou de consommation de contenu**
        
        Vérifiez que les utilisateurs disposent d’instructions appropriées pour les applications qu’ils utilisent, et se servent d’applications et d’appareils pris en charge par le service Azure Rights Management. Pour plus d’informations sur les applications et les appareils pris en charge, consultez [Configuration requise pour Azure information protection](requirements.md).
        
        Pour vérifier qu’un utilisateur ou un groupe est autorisé par Azure Active Directory à protéger ou à utiliser du contenu protégé, servez-vous des vérifications mentionnées dans la rubrique [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).
        
        Si les droits dont disposent les utilisateurs ne sont pas ceux attendus, vérifiez leur description et les implémentations spécifiques à l’application dans le [tableau des droits d’utilisation](configure-usage-rights.md#usage-rights-and-descriptions).

        **Client classique uniquement**: si les utilisateurs indiquent qu’ils peuvent ouvrir du contenu protégé mais qu’ils n’ont pas les droits dont ils ont besoin, le problème peut être que l’utilisateur ne se trouve pas dans le groupe correct configuré pour un modèle de Rights Management. Il est également possible que le [modèle doive être reconfiguré](configure-policy-templates.md) pour l’utilisateur ou le groupe. 
        
        
Utilisez les sections suivantes pour obtenir des informations spécifiques aux applications afin d’aider les utilisateurs à protéger les documents et les e-mails.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Utilisation de la protection des informations avec le client Azure Information Protection

Si les utilisateurs ont Office 2010, le client Azure Information Protection est nécessaire pour protéger et utiliser des documents et des e-mails protégés. Cependant, le client Azure Information Protection est recommandé pour tous les ordinateurs et appareils mobiles qui prennent en charge ce service.

En plus d’aider les utilisateurs à protéger des documents et des e-mails, le client Azure Information Protection leur permet d’effectuer le suivi des documents qu’ils ont protégés. Les documents suivis peuvent également être révoqués si les utilisateurs précédemment autorisés ne doivent plus y avoir accès.

Pour savoir comment utiliser ce client pour les ordinateurs Windows, consultez le [Guide de l’utilisateur du client Azure Information Protection](./rms-client/clientv2-user-guide.md).


## <a name="using-information-protection-with-office-365-office-2019-office-2016-or-office-2013"></a>Utilisation de la protection des informations avec Office 365, Office 2019, Office 2016 ou Office 2013

Si vous utilisez le service Azure Rights Management et que vous n’avez pas installé le client Azure Information Protection, les utilisateurs ne voient pas la barre Azure Information Protection dans leurs applications Office pour poste de travail. Ils ne voient pas non plus le bouton **sensibilité** sur le ruban, ni **classer et protéger** à partir de l’Explorateur de fichiers. Ces ajouts facilitent la protection des documents et des e-mails. Ces utilisateurs doivent suivre des instructions similaires aux suivantes.

> [!TIP]
> Pour trouver de l'aide et des instructions spécifiques à une application qui ont trait à l'utilisation de la protection des données avec ces applications, recherchez « **IRM** » ainsi que le nom et la version de l'application.

#### <a name="to-protect-a-document-in-word-from-office-365-proplus"></a>Pour protéger un document dans Word d’Office 365 ProPlus

1.  Dans Microsoft Word, créez un document.

2.  Dans le menu **fichier** : **info**  >  **protéger document**  >   **restreindre l’accès**.

3. Choisissez un modèle pour appliquer rapidement les droits d’utilisation appropriés ou sélectionnez **Restreindre l’accès** et sélectionnez vous-même les droits d’utilisation.

    > [!NOTE]
    > Si vous utilisez Rights Management pour la première fois sur votre ordinateur, l’option **Restreindre l’accès** va se connecter au service Azure Rights Management et vous serez invité à entrer vos informations d’identification pour configurer le client IRM Office. Vous pouvez ensuite choisir un modèle ou des droits d’utilisation.

3.  Enregistrez le document.

Lorsque d'autres personnes ouvriront le document, ils devront d'abord être authentifiés. S'ils ne reçoivent pas l'autorisation pour ouvrir le document, ce dernier ne s'ouvrira pas. S’ils sont autorisés à ouvrir le document, il s’ouvre avec les [droits d’utilisation](configure-usage-rights.md) restreints qui ont été spécifiés pour cet utilisateur. 

Par exemple, un droit d'utilisation Affichage uniquement ne permet pas à l'utilisateur de modifier ou d'enregistrer le document, même si ce dernier est d'abord copié vers un autre emplacement. 

Les droits d'utilisation sont affichés en haut du document grâce à une bannière de restriction. La bannière peut afficher les autorisations appliquées au document, ou un lien pour afficher celles-ci.

#### <a name="to-protect-an-email-message-using-outlook-from-office-365-proplus-connecting-to-exchange-online"></a>Pour protéger un e-mail à l’aide d’Outlook d’Office 365 ProPlus, en se connectant à Exchange Online

1.  Dans Outlook, créez un e-mail adressé à un destinataire au sein de votre organisation.

2.  Sous l’onglet **options** : **autorisation** > sélectionnez une option. Par exemple : **ne pas transférer**, ou **\<Company Name> -confidentiel** ou **\<Company Name> confidentiel uniquement**.

3.  Envoyez le message.

Comme pour l’affichage d’un document protégé, lorsque les destinataires ouvrent l’e-mail protégé, ceux-ci sont tout d’abord authentifiés. S’ils sont autorisés à voir le message électronique, ils s’ouvrent avec les [droits d’utilisation](configure-usage-rights.md) restreints qui ont été spécifiés pour cet utilisateur. 

Par exemple, si l’e-mail est protégé à l’aide de l’option **Ne pas transférer**, le bouton Transférer n’est pas disponible dans le ruban.

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>Pour protéger un e-mail à l’aide d’Outlook sur le web

1. Dans Outlook sur le web, créez un e-mail destiné à une personne de votre organisation.

2. Sélectionnez **Protéger**. Si la valeur par défaut n’a pas été modifiée par un administrateur, l’option **Ne pas transférer** est sélectionnée automatiquement. Si vous souhaitez modifier la valeur par défaut, sélectionnez **modifier les autorisations** , puis sélectionnez une option dans la liste déroulante. Par exemple : **chiffrer** ou **\<Company Name> confidentiel**.

3. Envoyez le message.

Comme pour un document protégé, les destinataires sont authentifiés avant de pouvoir ouvrir l’e-mail. S’ils sont autorisés à voir le message électronique, ils s’ouvrent avec les [droits d’utilisation](configure-usage-rights.md) restreints qui ont été spécifiés pour cet utilisateur. 

Par exemple, avec l’option par défaut **Ne pas transférer**, l’option **Transférer** n’est pas disponible dans la fenêtre de message.
