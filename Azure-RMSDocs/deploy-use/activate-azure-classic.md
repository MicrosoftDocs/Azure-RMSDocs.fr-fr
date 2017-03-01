---
title: "Activer Azure RMS avec le portail Azure Classic - AIP"
description: "Instructions d’activation du service Azure Rights Management quand vous avez accès au portail Azure. Par exemple, vous avez un abonnement à Enterprise Mobility Suite ou êtes abonné à Azure Information Protection Premium."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 444d74c957ec6e243858fcddfaac36951c257a9d
ms.lasthandoff: 02/24/2017


---

# <a name="how-to-activate-azure-rights-management-from-the-azure-classic-portal"></a>Comment activer Azure Rights Management à partir du portail classique Azure

>*S’applique à : Azure Information Protection*


Utilisez ces instructions si vous avez accès au portail Azure. Par exemple, vous avez un abonnement à Enterprise Mobility Suite ou êtes abonné à Azure Information Protection Premium.

> [!TIP]
> Regardez une vidéo de 2 minutes : [Comment activer Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Après avoir créé votre compte Azure, [connectez-vous au portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081). Utilisez un compte d’administrateur général tel que le compte que vous avez utilisé pour obtenir l’abonnement incluant Azure Rights Management.

2.  Dans le volet gauche, cliquez sur **Active Directory**.

3.  Dans la page **Active Directory** , cliquez sur **RIGHTS MANAGEMENT**.

4.  Sélectionnez l’annuaire à gérer pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], cliquez sur **ACTIVER**, puis confirmez votre action.

    > [!NOTE]
    >Si vous voyez une erreur d’activation, il est possible que votre plan de service ou version de produit n’inclue pas le service Azure Rights Management d’Azure Information Protection.
    >
    >Pour activer le service Azure Rights Management, vous devez avoir un [plan Premium Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) ou un [plan Office 365 incluant Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Pour obtenir de l'aide, envoyez un courrier électronique à [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).


**Statut de Rights Management** doit désormais afficher l’état **Actif** et l’option **ACTIVER** est remplacée par **DÉSACTIVER**.

## <a name="rights-management-status-values-and-descriptions-in-the-azure-classic-portal"></a>Descriptions et valeurs d’état du service Rights Management dans le portail Azure Classic
En plus de l'état **Actif** qui indique que le service Rights Management est activé et opérationnel, vous pouvez également voir les états **Inactif**, **Indisponible**ou **Non autorisé**.

|Valeur d'état|Description|
|----------------|---------------|
|**Actif**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est activé et opérationnel.|
|**Inactif**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est désactivé et doit être activé pour permettre à votre organisation de protéger les fichiers.|
|**Indisponible**|Le service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] est indisponible. Réessayez plus tard.|
|**Non autorisé**|Vous n’êtes pas autorisé à consulter l’état du service [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Par exemple, votre compte est verrouillé ou vous êtes l'administrateur global du locataire sélectionné.|

## <a name="next-steps"></a>Étapes suivantes
Retour à [Activation d’Azure Rights Management](activate-service.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
