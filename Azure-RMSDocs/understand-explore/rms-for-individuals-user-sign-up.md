---
title: "Inscription à RMS for individuals - AIP"
description: "Instructions à suivre pour obtenir ce compte gratuit et informations techniques sur le déroulement du processus."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d1c45c2b97fb3f278a8ecd3ebe9fe37af3ea5d0f
ms.sourcegitcommit: 0fa5dd38c9d66ee2ecb47dfdc9f2add12731485e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2017
---
# <a name="how-users-sign-up-for-rms-for-individuals"></a>Inscription à RMS for individuals

>*S’applique à : Azure Information Protection*

Pour obtenir un compte gratuit, demandez-le via la [page Microsoft Azure Information Protection](https://aka.ms/rms-signup) et indiquez votre adresse e-mail professionnelle. Le plus souvent, vous êtes redirigé vers cette page d’inscription après avoir reçu un e-mail avec une pièce jointe protégée. Le message e-mail explique la procédure d’inscription. 

Quand vous suivez ces instructions, vous recevez un e-mail de Microsoft qui vous permet d’effectuer la procédure d’inscription en entrant les détails nécessaires à la création de votre compte. À la fin de cette procédure, la dernière page affiche des liens pour télécharger le client ou la visionneuse Azure Information Protection pour différents appareils, un lien vers le guide de l’utilisateur, ainsi qu’un lien vers la dernière liste des applications offrant une prise en charge native de la protection Rights Management. 

## <a name="to-sign-up-for-rms-for-individuals"></a>Inscription à RMS for individuals

1.  À partir d’un ordinateur Windows ou Mac, ou d’un appareil mobile, accédez à la page [Microsoft Azure Information Protection](https://aka.ms/rms-signup).

2.  Tapez l’adresse e-mail que vous utilisez pour votre organisation, telle que **janetm@contoso.com** ou **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > Les adresses e-mail personnelles ne sont pas prises en charge. Par conséquent, n'indiquez pas de compte Microsoft (anciennement compte Microsoft Live ID) ou tout autre compte personnel que vous pouvez utiliser à votre domicile avec votre fournisseur d'accès à Internet.

3. Cliquez sur **S’inscrire**.

    Microsoft utilise votre adresse e-mail pour vérifier si votre organisation a déjà un [abonnement pour Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) ou un [abonnement Office 365 qui inclut la protection des données à l’aide d’Azure Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Si aucun de ces abonnements n’est détecté, vous n’avez pas besoin de RMS for Individuals. Vous êtes connecté immédiatement et l’inscription en libre-service à RMS for Individuals est annulée. Si aucun abonnement n’est détecté, vous passez à l’étape suivante.

4. Attendez qu'un e-mail de confirmation soit envoyé à l'adresse que vous avez indiquée. Il provient de l’équipe Office 365 (support@email.microsoftonline.com) et présente l’objet suivant : **Terminer l’inscription à Microsoft Azure Information Protection**.

5. À la réception de l’e-mail, cliquez sur **Oui, c’est moi** pour vérifier votre adresse e-mail et terminer le processus d’inscription.

6. Dans la page **Dernière chose...** qui s’affiche, vous allez maintenant entrer les informations de votre compte. Tapez vos nom et prénom, entrez et confirmez le mot de passe de votre choix, puis cliquez sur **Démarrer**.

7. Une fois votre compte créé, une nouvelle page Microsoft Azure Information Protection s’affiche. Dans celle-ci, vous pouvez soit télécharger et installer le client Azure Information Protection, soit cliquer sur le lien [Guide de l’utilisateur](../rms-client/client-user-guide.md) pour obtenir des guides pratiques pour les ordinateurs Windows.

Votre compte étant créé, vous pouvez à présent protéger des fichiers et lire des fichiers protégés par d'autres personnes. Si vous êtes invité à vous connecter pour protéger des fichiers ou utiliser des fichiers protégés, entrez l’adresse e-mail et le mot de passe que vous avez utilisés pour créer le compte RMS for Individuals.

## <a name="technical-overview-of-the-sign-up-process"></a>Présentation technique du processus d’inscription
RMS for Individuals utilise un processus d’inscription en libre-service dont se servent également d’autres services recourant à la technologie cloud de Microsoft pour l’authentification des utilisateurs.

Voici ce qui se passe en arrière-plan quand un utilisateur s'inscrit à RMS for individuals alors que son organisation n'a pas d'abonnement Office 365 ou Azure, et donc pas d'annuaire dans Azure pour authentifier les utilisateurs :

1. Lorsque le premier utilisateur d'une organisation demande un abonnement RMS for Individuals, le nom de domaine figurant dans son adresse de messagerie est vérifié afin de déterminer s'il est déjà associé à un client Azure. À défaut de client existant, un client est automatiquement créé pour l'organisation, ainsi qu'un répertoire Azure contenant un compte pour ce premier utilisateur. Contrairement à un abonnement payant à Azure ou à un essai gratuit, le premier compte n’est pas un compte d’administrateur général, mais d’utilisateur standard. Le nouveau compte utilise l'adresse de messagerie et le mot de passe fournis par l'utilisateur.

    > [!NOTE]
    > Certains noms de domaine ne peuvent pas être utilisés pour créer l'annuaire. Ils ne peuvent donc pas non plus être utilisés pour RMS for individuals.

    Si un locataire est détecté, son compte est vérifié pour déterminer s’il dispose déjà d’un abonnement Azure Information Protection. À défaut, l'abonnement gratuit à RMS for Individuals peut être ajouté.

2. L'organisation reçoit un abonnement RMS for Individuals. Azure peut désormais authentifier cet utilisateur qui peut ensuite protéger des fichiers et lire des fichiers protégés par d’autres utilisateurs à l’aide du service Azure Rights Management. Pour protéger des fichiers et lire des fichiers protégés, l’utilisateur doit disposer d’une application compatible RMS, notamment l’une des applications Office ou le [client Azure Information Protection](../rms-client/aip-client.md) gratuit.

3. Lorsque le deuxième utilisateur de la même organisation demande un abonnement RMS for individuals, un nouveau compte utilisateur est ajouté à l'annuaire Azure créé précédemment en utilisant l'abonnement RMS for individuals de l'organisation. Cet utilisateur a les mêmes droits que le premier (il peut protéger des fichiers et lire des fichiers protégés). Mais en plus de cela, ces deux utilisateurs peuvent à présent collaborer de façon plus sécurisée et plus simple grâce à des modèles par défaut permettant de restreindre l’accès à l’annuaire Azure de l’organisation.

4. Les utilisateurs suivants de la même organisation procèdent de même, en ajoutant des comptes d’utilisateur à l’annuaire Azure de l’organisation lors de l’inscription. Plus il y a de comptes associés à l'annuaire, plus le nombre d'utilisateurs pouvant collaborer en toute sécurité est important. Cela permet d'empêcher simplement que des personnes non autorisées lisent des fichiers auxquels elles ne devraient pas avoir accès.

Grâce à ce processus, aucun frais n'est imputé à l'organisation et aucune intervention du service informatique n'est requise. Cependant, le département informatique peut choisir d’effectuer l’une des actions suivantes :

- **Gérer les comptes et le processus d’inscription** : les administrateurs informatiques peuvent s’approprier l’annuaire et les comptes créés automatiquement dans Azure. Ils peuvent ensuite gérer les comptes en implémentant des solutions d'intégration d'annuaire, telles que la synchronisation des mots de passe et l'authentification unique. Ils peuvent également empêcher des utilisateurs de créer des comptes ou de s'inscrire à RMS for Individuals.
    
    Pour plus d’informations, consultez [Contrôle administrateur des comptes créés pour RMS for individuals](rms-for-individuals-take-control.md).

- **Gérer Rights Management**: Les administrateurs informatiques peuvent convertir l'abonnement RMS for individuals de l'organisation en abonnement payant incluant Azure Rights Management. Dans ce cas, l'annuaire et les comptes Azure existants sont préservés afin d'assurer une transition transparente pour les utilisateurs de RMS for individuals. Les fichiers que les utilisateurs ont protégés le restent, avec les mêmes stratégies, et les personnes autorisées peuvent continuer à y accéder de la même manière.
    
    Cette conversion permet à l'organisation d'intégrer Rights Management dans ses flux de travaux, ses services et ses magasins de données. Vous pouvez en outre gérer Rights Management, puisque vous contrôlez la clé de locataire de l'organisation pour Azure Rights Management. Vous pouvez à présent exécuter les actions suivantes :
    
    - Configurer Exchange et SharePoint pour la prise en charge d’Azure Rights Management, même si ces services s’exécutent en local. Exchange et SharePoint sont pris en charge en mode natif pour les services en ligne et sont pris en charge par un connecteur pour les serveurs locaux. Pour plus d'informations, consultez les rubriques suivantes :
    
        - Les sections Exchange Online et SharePoint Online de [Office 365 : configuration pour les clients et services en ligne](../deploy-use/configure-office365.md)
        
        - [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md)
        
    - Exécuter la découverte électronique sur les données de votre entreprise pour que les utilisateurs et les services autorisés puissent, si nécessaire, déchiffrer les fichiers protégés. Pour plus d’informations, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).
    
    - Journaliser l’activité du service Rights Management. La journalisation offre des informations précieuses puisque vous pouvez non seulement savoir quels fichiers sont protégés et qui y accède, mais également identifier le comportement potentiellement suspect de personnes non autorisées. Pour plus d’informations, consultez [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md).
    
    - Offrir aux utilisateurs la possibilité de suivre et de révoquer leurs documents protégés, si ces fonctionnalités sont prises en charge par votre abonnement. Pour plus d’informations, consultez [Suivre et révoquer vos documents](../rms-client/client-track-revoke.md) dans le [guide d’utilisation d’Azure Information Protection](../rms-client/client-user-guide.md).
    
    - Implémenter une solution BYOK (Bring Your Own Key) pour que votre clé de locataire pour Azure Information Protection soit créée et gérée par vous. Pour plus d’informations, consultez [Planning and implementing your Azure Information Protection tenant key](../plan-design/plan-implement-tenant-key.md) (Planification et implémentation de la clé de locataire Azure Information Protection).


## <a name="next-steps"></a>Étapes suivantes
Consultez [Contrôle administrateur des comptes créés pour RMS for individuals](rms-for-individuals-take-control.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]