---
title: "Comment activer Azure Rights Management à partir du portail classique Azure | Azure RMS"
description: "Instructions d’activation d’Azure RMS quand vous avez accès au portail Azure. Par exemple, vous avez un abonnement à Enterprise Mobility Suite ou êtes abonné à Azure Rights Management Premium."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: ab3b5d71e8cee2ece7fad4c9c3017de7d6eca979


---

# Comment activer Azure Rights Management à partir du portail classique Azure

>*S’applique à : Azure Rights Management*


Utilisez ces instructions si vous avez accès au portail Azure. Par exemple, vous avez un abonnement à Enterprise Mobility Suite ou êtes abonné à Azure Rights Management Premium.

> [!TIP]
> Regardez une vidéo de 2 minutes : [Comment activer Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Après avoir créé votre compte Azure, [connectez-vous au portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081). Utilisez un compte d’administrateur général tel que le compte que vous avez utilisé pour obtenir l’abonnement incluant Azure Rights Management.

2.  Dans le volet gauche, cliquez sur **Active Directory**.

3.  Dans la page **Active Directory** , cliquez sur **RIGHTS MANAGEMENT**.

4.  Sélectionnez l’annuaire à gérer pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], cliquez sur **ACTIVER**, puis confirmez votre action.

    > [!NOTE]
    >Si vous voyez une erreur d’activation, il est possible que votre plan de services ou votre version de produit n’inclue pas [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].
    >
    >Utilisez les informations de [Abonnements cloud prenant en charge Azure RMS](../get-started/requirements-subscriptions.md) pour vérifier la prise en charge de RMS. Pour obtenir de l'aide, envoyez un courrier électronique à [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).


**Statut de Rights Management** doit désormais afficher l’état **Actif** et l’option **ACTIVER** est remplacée par **DÉSACTIVER**.

## Descriptions et valeurs d’état du service Rights Management dans le portail Azure Classic
En plus de l'état **Actif** qui indique que le service Rights Management est activé et opérationnel, vous pouvez également voir les états **Inactif**, **Indisponible**ou **Non autorisé**.

|Valeur d'état|Description|
|----------------|---------------|
|**Actif**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est activé et opérationnel.|
|**Inactif**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est désactivé et doit être activé pour permettre à votre organisation de protéger les fichiers.|
|**Indisponible**|Le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est indisponible. Réessayez plus tard.|
|**Non autorisé**|Vous n’êtes pas autorisé à consulter l’état du service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Par exemple, votre compte est verrouillé ou vous êtes l'administrateur global du locataire sélectionné.|

## Étapes suivantes
Retour à [Activation d’Azure Rights Management](activate-service.md)


<!--HONumber=Aug16_HO4-->


