---
title: "Étape 4 du didacticiel de démarrage rapide | Azure Rights Management"
description: "Étape 3 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en environ 30 minutes."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: ce1d0a700e0b69d71f5cb2e93f406124bc0ca581
ms.openlocfilehash: c9ed50317e18e86438b4393ce629d23d433c99fe


---

# Étape 4 : classification, étiquetage et protection en action 

>*S’applique à : Azure Information Protection*

Maintenant que vous avez un document Word ouvert avec le client Azure Information Protection installé, vous allez voir combien il est facile d’étiqueter et de protéger votre document à l’aide de la stratégie que nous avons configurée.

La classification et la protection ont lieu quand vous enregistrez le document, mais avant cela, nous allons utiliser notre document non enregistré pour voir combien il est facile d’appliquer et de modifier les étiquettes.

## Pour modifier manuellement notre étiquette par défaut

Dans la barre Information Protection, sélectionnez l’étiquette **Personal** (Personnel). Vous êtes alors invité à indiquer pourquoi vous abaissez le niveau de classification :

![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de confirmation de l’abaissement](../media/info-protect-lower-justification.png)

Sélectionnez **The previous label no longer applies** (L’étiquette précédente ne s’applique plus), cliquez sur **Confirm** (Confirmer). **Sensitivity** (Niveau de confidentialité) prend la valeur **Personal** (Personnel).

## Pour supprimer complètement la classification

Dans la barre Information Protection, cliquez sur l’icône **Edit label** (Modifier l’étiquette) à côté de **Personal** (Personnel). Les étiquettes disponibles apparaissent. Au lieu de choisir l’une des étiquettes, cliquez sur l’icône **Remove label** (Supprimer l’étiquette). Cliquez sur **OK** pour confirmer, puis indiquez la justification de cette action.  

La valeur **Sensitivity** (Niveau de confidentialité) indique **Not set** (Non défini), ce qui correspond à ce que les utilisateurs voient initialement si vous ne définissez pas d’étiquette par défaut :

![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : supprimer la classification](../media/sensitivity-not-set.png)


## Pour afficher une invite de recommandation pour l’étiquetage et la protection automatique

1. Dans le document Word, tapez un numéro de carte de crédit valide, par exemple **4242-4242-4242-4242**. 

2. Enregistrez le document (utilisez n’importe quel nom de fichier et n’importe quel emplacement). 

3. L’invite suivante s’affiche : **It is recommended to label this file as Confidential** (Nous vous recommandons d’étiqueter ce fichier comme Confidentiel). Cliquez sur **Change now** (Modifier maintenant).

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de recommandation](../media/change-now.png)

    Outre le fait que l’étiquette du document est définie sur Confidential (Confidentiel), le filigrane de votre organisation apparaît immédiatement dans la page, et le pied de page **Sensitivity: Confidential** (Niveau de confidentialité : Confidentiel) est également appliqué. 

    Le document est également protégé avec le modèle Azure Rights Management que vous avez spécifié, ce que vous pouvez vérifier en cliquant sur l’onglet **Fichier** et en affichant les informations **Protéger le document**. Si vous avez utilisé le modèle Confidential par défaut, un message précise que l’accès au document est limité aux utilisateurs internes (les utilisateurs extérieurs à votre organisation ne pourront pas l’ouvrir) et que son contenu ne peut pas être copié ou imprimé. En tant que propriétaire du document, vous pouvez le copier et l’imprimer, mais si vous l’envoyez à un autre utilisateur de votre organisation, il ne pourra pas effectuer ces actions.

La classification, l’étiquetage et la protection n’ayant plus de secret pour vous, nous allons voir comment vous pouvez protéger vos documents même quand ils sont partagés avec d’autres personnes dans une autre organisation. Vous pouvez même suivre la façon dont ils sont utilisés et révoquer leur accessibilité.

>[!div class="step-by-step"]
[&#171; Étape 3](infoprotect-tutorial-step3.md)
[Étape 5 &#187;](infoprotect-tutorial-step5.md)



<!--HONumber=Sep16_HO4-->


