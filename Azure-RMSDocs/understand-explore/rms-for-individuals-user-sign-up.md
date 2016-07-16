---
title: "Inscription des utilisateurs à RMS for individuals | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 19252180802c69d6e5d6bf22c71ff3bcba96fb36


---

# Inscription à RMS for individuals

*S’applique à : Azure Rights Management*

Pour obtenir un compte gratuit, les utilisateurs accèdent à la [page Microsoft Rights Management](https://portal.aadrm.com/) et en font la demande en indiquant leur adresse e-mail professionnelle ou scolaire. 

Le plus souvent, les utilisateurs sont dirigés vers cette page d’inscription après avoir reçu un e-mail avec pièce jointe protégée, qui contient des instructions sur la manière de s’inscrire. Ils reçoivent en retour un e-mail de Microsoft qui leur permet de mener à bien l’inscription en entrant les détails nécessaires à la création de leur compte. Ils reçoivent ensuite une confirmation par e-mail de Microsoft, ultime e-mail qui les dirige vers la page de téléchargement de l’application de partage pour différents appareils, et qui contient un lien vers le guide de l’utilisateur.

## Inscription à RMS for individuals

1.  À l'aide d'un ordinateur Windows ou Mac, accédez à la page [Microsoft Rights Management](https://portal.aadrm.com).

2.  Entrez l'adresse de messagerie que vous utilisez au sein de votre organisation, par exemple, **janetm@contoso.com** ou **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > Les adresses e-mail personnelles ne sont pas prises en charge. Par conséquent, n'indiquez pas de compte Microsoft (anciennement compte Microsoft Live ID) ou tout autre compte personnel que vous pouvez utiliser à votre domicile avec votre fournisseur d'accès à Internet.

3.  Cliquez sur **Mise en route**.

    Microsoft utilise votre adresse de messagerie pour vérifier si votre organisation possède déjà un [abonnement payant qui inclut Azure RMS](../get-started/requirements-subscriptions.md). Si tel est le cas, vous n'avez pas besoin de RMS for Individuals. Vous êtes connecté immédiatement et l'inscription en libre-service à RMS for Individuals est annulée. Si aucun abonnement payant pour Azure RMS n'est trouvé, vous passez à l'étape suivante.

4.  Attendez qu'un e-mail de confirmation soit envoyé à l'adresse que vous avez indiquée. Il doit provenir de Microsoft (DoNotReply@microsoft.com) et sont objet est **Microsoft RMS**.

5.  Cliquez ensuite sur le lien figurant dans les instructions pour terminer l'inscription.

6.  Ce lien vous permet d'accéder à une nouvelle page **Microsoft Rights Management** dans laquelle vous pouvez entrer les informations relatives à votre compte. Tapez vos nom et prénom, entrez et confirmez le mot de passe de votre choix, sélectionnez votre pays dans la liste déroulante (ou le pays le plus proche si le vôtre n'y figure pas), puis cliquez sur **Créer**.

7.  Vous devez alors recevoir un autre e-mail de Microsoft, vous confirmant que votre compte est prêt à l'emploi.

8.  Lorsque vous recevez le message électronique, cliquez sur le lien de connexion pour lire les instructions de téléchargement et d'installation de l'application de partage, ou cliquez sur le lien Aide pour lire le guide de l'utilisateur de celle-ci.

Votre compte étant créé, vous pouvez à présent protéger des fichiers et lire des fichiers protégés par d'autres personnes. Lorsque vous êtes invité à vous connecter pour protéger des fichiers ou lire des fichiers protégés, entrez l'adresse e-mail et le mot de passe utilisés lors de la création du compte RMS for Individuals.

## Présentation technique du processus d’inscription
RMS for Individuals utilise un processus d'inscription en libre-service dont se servent également d'autres services recourant à la technologie cloud de Microsoft pour l'authentification des utilisateurs.

Voici ce qui se passe en arrière-plan quand un utilisateur s'inscrit à RMS for individuals alors que son organisation n'a pas d'abonnement Office 365 ou Azure, et donc pas d'annuaire dans Azure pour authentifier les utilisateurs :

1.  Lorsque le premier utilisateur d'une organisation demande un abonnement RMS for Individuals, le nom de domaine figurant dans son adresse de messagerie est vérifié afin de déterminer s'il est déjà associé à un client Azure. À défaut de client existant, un client est automatiquement créé pour l'organisation, ainsi qu'un répertoire Azure contenant un compte pour ce premier utilisateur. Contrairement à un abonnement payant à Azure, le premier compte n'est pas un compte d'administrateur général, mais d'utilisateur standard. Le nouveau compte utilise l'adresse de messagerie et le mot de passe fournis par l'utilisateur.

    > [!NOTE]
    > Certains noms de domaine ne peuvent pas être utilisés pour créer l'annuaire. Ils ne peuvent donc pas non plus être utilisés pour RMS for individuals. La liste des noms de domaines bloqués figure dans le fichier JSON (JavaScript Objet Notation) [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Si un client est trouvé, son compte est vérifié pour voir s'il dispose déjà un abonnement Azure RMS. À défaut, l'abonnement gratuit à RMS for Individuals peut être ajouté.

2.  L'organisation reçoit un abonnement RMS for Individuals. Désormais, Azure peut authentifier cet utilisateur qui peut ensuite protéger des fichiers et lire des fichiers protégés par d'autres grâce à Azure Rights Management. Pour protéger des fichiers et lire des fichiers protégés, l’utilisateur doit disposer d’une application compatible RMS, telle que l’[application de partage Rights Management](../rms-client/sharing-app-windows.md) disponible gratuitement.

3.  Lorsque le deuxième utilisateur de la même organisation demande un abonnement RMS for individuals, un nouveau compte utilisateur est ajouté à l'annuaire Azure créé précédemment en utilisant l'abonnement RMS for individuals de l'organisation. Ce deuxième utilisateur a les mêmes droits que le premier (protéger des fichiers et lire des fichiers protégés), mais, en plus de cela, les deux utilisateurs peuvent désormais collaborer plus aisément en toute sécurité, car ils peuvent rapidement appliquer des modèles par défaut à des fichiers, qui restreignent l'accès aux comptes figurant dans l'annuaire Azure de leur organisation.

4.  Les utilisateurs suivants de la même organisation procèdent de même, en ajoutant des comptes d'utilisateur (lors de l'inscription) à l'annuaire Azure de l'organisation. Plus il y a de comptes associés à l'annuaire, plus le nombre d'utilisateurs pouvant collaborer en toute sécurité est important. Cela permet d'empêcher simplement que des personnes non autorisées lisent des fichiers auxquels elles ne devraient pas avoir accès.

Grâce à ce processus, aucun frais n'est imputé à l'organisation et aucune intervention du service informatique n'est requise. Cependant, le département informatique peut choisir d'effectuer l'une des actions suivantes :

-   **Gérer les comptes et le processus d’inscription** : les administrateurs informatiques peuvent s’approprier l’annuaire et les comptes créés automatiquement dans Azure. Ils peuvent ensuite gérer les comptes en implémentant des solutions d'intégration d'annuaire, telles que la synchronisation des mots de passe et l'authentification unique. Ils peuvent également empêcher des utilisateurs de créer des comptes ou de s'inscrire à RMS for Individuals.

    Pour plus d’informations, consultez [Contrôle administrateur des comptes créés pour RMS for individuals](rms-for-individuals-take-control.md).

-   **Gérer Rights Management**: Les administrateurs informatiques peuvent convertir l'abonnement RMS for individuals de l'organisation en abonnement payant incluant Azure Rights Management. Dans ce cas, l'annuaire et les comptes Azure existants sont préservés afin d'assurer une transition transparente pour les utilisateurs de RMS for individuals. Les fichiers que les utilisateurs ont protégés le restent, avec les mêmes stratégies, et les personnes autorisées peuvent continuer à y accéder de la même manière.

    Cette conversion permet à l'organisation d'intégrer Rights Management dans ses flux de travaux, ses services et ses magasins de données. Vous pouvez en outre gérer Rights Management, puisque vous contrôlez la clé de locataire de l'organisation pour Azure Rights Management. Vous pouvez à présent exécuter les actions suivantes :

    -   Configurer Exchange et SharePoint pour la prise en charge d’Azure Rights Management, même si ces éléments s’exécutent en local. Exchange et SharePoint sont pris en charge en mode natif pour les services en ligne et sont pris en charge par un connecteur pour les serveurs locaux. Pour plus d'informations, consultez les rubriques suivantes :

        -   Les sections Exchange Online et SharePoint Online de [Office 365 : configuration pour les clients et services en ligne](../deploy-use/configure-office365.md)

        -   [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md)

    -   Exécuter le processus eDiscovery sur les données de votre organisation, afin de pouvoir déchiffrer, si nécessaire, les fichiers qui ont été protégés à l'aide de Rights Management. Pour plus d’informations, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

    -   Consigner l'ensemble de l'activité liée à Rights Management de votre organisation. Il s'agit d'informations précieuses puisque vous pouvez non seulement savoir quels fichiers sont protégés et qui y accède, mais également identifier le comportement potentiellement suspect de personnes non autorisées. Pour plus d’informations, consultez [Journalisation et analyse de l’utilisation d’Azure Rights Management](../deploy-use/log-analyze-usage.md).

    -   Offrir aux utilisateurs la possibilité de suivre et révoquer leurs documents protégés, si ces fonctionnalités sont prises en charge par votre [abonnement Azure RMS](https://technet.microsoft.com/dn858608). Pour plus d’informations, consultez [Suivre et révoquer des fichiers](../rms-client/sharing-app-track-revoke.md) dans le [Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md).

    -   Implémenter une solution Bring you own key (BYOK) afin que votre clé de locataire pour Azure Rights Management soit générée en local selon vos stratégies informatiques, puis transférée en toute sécurité à Microsoft grâce à un module de sécurité matériel (HSM). Pour plus d’informations, consultez [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md).


## Étapes suivantes
Consultez [Contrôle administrateur des comptes créés pour RMS for individuals](rms-for-individuals-take-control.md).





<!--HONumber=Jun16_HO4-->


