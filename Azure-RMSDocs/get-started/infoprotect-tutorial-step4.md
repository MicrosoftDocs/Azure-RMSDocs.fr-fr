---
title: "Didacticiel de démarrage rapide, étape 4 - AIP"
description: "Didacticiel de présentation expliquant comment tester rapidement Azure Information Protection, étape 4 : étiquetage et protection en action."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
ms.openlocfilehash: fb1334a2ee345125db6e2637a59a5ab1a69e62d8
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>Étape 4 : classification, étiquetage et protection en action 

>*S’applique à : Azure Information Protection*

Maintenant que vous avez un document Word ouvert avec le client Azure Information Protection installé, vous allez voir combien il est facile d’étiqueter et de protéger votre document à l’aide de la stratégie que nous avons configurée.

La classification et la protection ont lieu quand vous enregistrez le document, mais avant cela, nous allons utiliser notre document non enregistré pour voir combien il est facile d’appliquer et de modifier les étiquettes.

## <a name="to-manually-change-our-default-label"></a>Pour modifier manuellement notre étiquette par défaut

Dans la barre Information Protection, sélectionnez l’étiquette **Question secrète** pour voir la façon dont les sous-étiquettes s’affichent :

![Didacticiel de démarrage rapide Azure Information Protection, étape 4 : choisir une sous-étiquette](../media/info-protect-sub-labels.png)

Sélectionnez **All Company** (Toutes les sociétés). Vous verrez alors que les autres étiquettes n’apparaissent plus dans la barre maintenant que vous avez sélectionné une étiquette pour ce document. La valeur **Sensitivity** (Niveau de confidentialité) devient **Secret \ All Company** (Question secrète \ Toutes les sociétés) avec une modification correspondante de la couleur de l’étiquette :

![Étape 4 du didacticiel de démarrage rapide Azure Information Protection - Sous-étiquette sélectionnée](../media/info-protect-sub-label-selected.png)

Dans la barre Information Protection, cliquez sur l’icône **Edit Label** (Modifier l’étiquette) à côté de **Secret \ All Company** (Question secrète \ Toutes les sociétés) :

![Didacticiel de démarrage rapide Azure Information Protection, étape 4 : icône Modifier l’étiquette](../media/info-protect-edit-label-selected.png)

Les étiquettes disponibles apparaissent à nouveau.

Sélectionnez maintenant l’étiquette **Personal** (Personnel). Étant donné que vous avez sélectionné une étiquette dont la classification est inférieure à l’étiquette précédemment sélectionnée pour ce document, vous êtes invité à justifier votre choix :

![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de confirmation de l’abaissement](../media/info-protect-lower-justification.png)

Sélectionnez **The previous label no longer applies** (L’étiquette précédente ne s’applique plus), cliquez sur **Confirm** (Confirmer). La valeur **Sensitivity** (Niveau de confidentialité) devient **Personal** (Personnel) et les autres étiquettes sont masquées à nouveau.

## <a name="to-remove-the-classification-completely"></a>Pour supprimer complètement la classification

Dans la barre Information Protection, cliquez à nouveau sur l’icône **Edit Label** (Modifier l’étiquette). Toutefois, au lieu de choisir l’une des étiquettes, cliquez sur l’icône **Delete Label** (Supprimer l’étiquette) :

![Didacticiel de démarrage rapide Azure Information Protection, étape 4 : icône Supprimer](../media/delete-icon-from-personal.png)

Cette fois à l’invite, saisissez « Ce document n’a pas besoin d’être classé », puis cliquez sur **Confirm** (Confirmer).  

La valeur **Sensitivity** (Niveau de confidentialité) indique **Not set** (Non défini), ce qui correspond à ce que les utilisateurs voient initialement si vous ne définissez pas d’étiquette par défaut :

![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : supprimer la classification](../media/sensitivity-not-set.png)


## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Pour afficher une invite de recommandation pour l’étiquetage et la protection automatique

1. Dans le document Word, tapez un numéro de carte de crédit valide, par exemple **4242-4242-4242-4242**. 

2. Enregistrez le document (utilisez n’importe quel nom de fichier et n’importe quel emplacement). 

3. L’invite suivante s’affiche : **It is recommended to label this file as Confidential** (Nous vous recommandons d’étiqueter ce fichier comme Confidentiel). Cliquez sur **Change now** (Modifier maintenant).

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de recommandation](../media/change-now.png)

    Outre le fait que l’étiquette du document est définie sur Confidential (Confidentiel), le filigrane de votre organisation apparaît immédiatement dans la page, et le pied de page **Sensitivity: Confidential** (Niveau de confidentialité : Confidentiel) est également appliqué. 

    Le document est également protégé avec le modèle Azure Rights Management que vous avez spécifié, ce que vous pouvez vérifier en cliquant sur l’onglet **Fichier** et en affichant les informations **Protéger le document**. Si vous avez utilisé le modèle Confidential par défaut, un message précise que l’accès au document est limité aux utilisateurs internes (les utilisateurs extérieurs à votre organisation ne pourront pas l’ouvrir) et que son contenu ne peut pas être copié ou imprimé. En tant que propriétaire du document, vous pouvez le copier et l’imprimer, mais si vous l’envoyez à un autre utilisateur de votre organisation, il ne pourra pas effectuer ces actions.

4. Vous pouvez maintenant fermer ce document.

La classification, l’étiquetage et la protection n’ayant plus de secret pour vous, nous allons voir comment vous pouvez protéger vos documents même quand ils sont partagés avec d’autres personnes dans une autre organisation. Vous pouvez même suivre la façon dont ils sont utilisés et révoquer leur accessibilité.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|Instructions complètes pour l’étiquetage et la protection de fichiers |[Classifier et protéger un fichier ou un e-mail](../rms-client/client-classify-protect.md)|





>[!div class="step-by-step"]
[&#171; Étape 3](infoprotect-tutorial-step3.md)
[Étape 5 &#187;](infoprotect-tutorial-step5.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]