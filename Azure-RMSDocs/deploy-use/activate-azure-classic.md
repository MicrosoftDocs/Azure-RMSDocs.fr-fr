---
# required metadata

title: Comment activer Azure Rights Management à partir du portail classique Azure | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/05/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Comment activer Azure Rights Management à partir du portail classique Azure

*S’applique à : Azure Rights Management*


Utilisez ces instructions si vous avez accès au portail Azure. Par exemple, vous avez un abonnement pour Enterprise Mobility Suite.

> [!TIP]
> Regardez une vidéo de 2 minutes : [Comment activer Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Après avoir créé votre compte Azure, [connectez-vous au portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  Dans le volet gauche, cliquez sur **ACTIVE DIRECTORY**.

3.  Dans la page **active directory**, cliquez sur **RIGHTS MANAGEMENT**.

4.  Sélectionnez l’annuaire à gérer pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], cliquez sur **ACTIVER**, puis confirmez.

---

   REMARQUE : Si vous voyez une erreur d’activation, il est possible que votre plan de services ou votre version de produit n’inclue pas [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

   Utilisez les informations de [Abonnements cloud prenant en charge Azure RMS](../get-started/requirements-subscriptions.md) pour vérifier la prise en charge de RMS. Pour obtenir de l’aide, envoyez un message électronique à [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).

---


**Statut de Rights Management** doit désormais afficher l’état **Actif** et l’option **ACTIVER** est remplacée par **DÉSACTIVER**.

## Descriptions et valeurs d’état du service Rights Management dans le portail Azure Classic
En plus de l’état **Actif** qui indique que le service Rights Management est activé et opérationnel, vous pouvez également voir les états **Inactif**, **Indisponible** ou **Non autorisé**.

|Valeur d'état|Description|
|----------------|---------------|
|**Actif**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est activé et opérationnel.|
|**Inactif**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est désactivé et doit être activé pour permettre à votre organisation de protéger les fichiers.|
|**Indisponible**|Le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est indisponible. Réessayez plus tard.|
|**Non autorisé**|Vous n’êtes pas autorisé à consulter l’état du service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Par exemple, votre compte est verrouillé ou vous êtes l'administrateur global du locataire sélectionné.|

## Étapes suivantes
Retour à [Activation d’Azure Rights Management](activate-service.md).

<!--HONumber=May16_HO1-->


