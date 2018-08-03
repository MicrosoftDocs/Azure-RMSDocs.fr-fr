---
title: Didacticiel de démarrage rapide, étape 4 - AIP
description: 'Didacticiel de présentation expliquant comment tester rapidement Azure Information Protection, étape 4 : étiquetage et protection en action.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
ms.openlocfilehash: 965725410fd3435f2468810b5cafcbfa91c4fa5b
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39475116"
---
# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>Étape 4 : classification, étiquetage et protection en action 

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Maintenant que vous avez un document Word ouvert avec le client Azure Information Protection installé, vous allez voir combien il est facile d’étiqueter et de protéger votre document à l’aide de la stratégie que nous avons configurée.

La classification et la protection ont lieu quand vous enregistrez le document, mais avant cela, nous allons utiliser notre document non enregistré pour voir combien il est facile d’appliquer et de modifier les étiquettes.

## <a name="to-manually-change-our-default-label"></a>Pour modifier manuellement notre étiquette par défaut

Dans la barre Information Protection, sélectionnez la dernière étiquette pour voir comment les sous-étiquettes s’affichent :

![Didacticiel de démarrage rapide Azure Information Protection, étape 4 : choisir une sous-étiquette](./media/info-protect-sub-labelsv2.png)

Sélectionnez une de ces sous-étiquettes. Vous voyez alors que les autres étiquettes n’apparaissent plus dans la barre maintenant que vous avez sélectionné une étiquette pour ce document. La valeur **Sensibilité** change pour montrer le nom de l’étiquette et de la sous-étiquette avec une modification correspondante de la couleur de l’étiquette. Par exemple :

![Étape 4 du didacticiel de démarrage rapide Azure Information Protection - Sous-étiquette sélectionnée](./media/info-protect-sub-label-selectedv2.png)

Dans la barre Information Protection, cliquez sur l’icône **Modifier l’étiquette** en regard de la valeur de l’étiquette actuellement sélectionnée :

![Didacticiel de démarrage rapide Azure Information Protection, étape 4 : icône Modifier l’étiquette](./media/info-protect-edit-label-selectedv2.png)

Les étiquettes disponibles apparaissent à nouveau.

Sélectionnez maintenant la première étiquette, **Personnel**. Étant donné que vous avez sélectionné une étiquette dont la classification est inférieure à l’étiquette précédemment sélectionnée pour ce document, vous êtes invité à justifier votre choix :

![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de confirmation de l’abaissement](./media/info-protect-lower-justification.png)

Sélectionnez **L’étiquette précédente ne s’applique plus** et cliquez sur **Confirmer**. La valeur **Sensibilité** devient **Personnel** et les autres étiquettes sont masquées à nouveau.

## <a name="to-remove-the-classification-completely"></a>Pour supprimer complètement la classification

Dans la barre Information Protection, cliquez à nouveau sur l’icône **Modifier l’étiquette**. Toutefois, au lieu de choisir l’une des étiquettes, cliquez sur l’icône **Supprimer l’étiquette** :

![Didacticiel de démarrage rapide Azure Information Protection, étape 4 : icône Supprimer](./media/delete-icon-from-personalv2.png)

Cette fois à l’invite, entrez « Ce document n’a pas besoin d’être classé » et cliquez sur **Confirmer**.  

La valeur **Sensibilité** indique **Non défini**, ce qui correspond à ce que voient les utilisateurs au départ si vous ne définissez pas d’étiquette par défaut.

## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Pour afficher une invite de recommandation pour l’étiquetage et la protection automatique

1. Dans le document Word, tapez un numéro de carte de crédit valide, par exemple **4242-4242-4242-4242**. 

2. Enregistrez le document localement avec un nom de fichier. 

3. Vous voyez maintenant une invite à appliquer l’étiquette que vous avez configurée pour la protection quand des numéros de carte de crédit sont détectés. Si nous n’avez pas accepté la recommandation, notre paramètre de stratégie nous permet de la rejeter en sélectionnant **Abandonner**. En donnant une recommandation mais en permettant à un utilisateur de l’ignorer, vous réduisez les faux positifs quand vous utilisez la classification automatique. Pour ce didacticiel, cliquez sur **Modifier maintenant**.

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de recommandation](./media/change-nowv2.png)

    Outre le fait que le document montre maintenant que notre étiquette configurée est appliquée (par exemple **Confidentiel\Finance**), vous voyez immédiatement en filigrane le nom de votre entreprise à travers la page, et le pied de page **Classé confidentiel** est également appliqué. 

    Le document est aussi protégé par les autorisations que vous avez spécifiées pour cette étiquette. Vous pouvez vérifier que le document est protégé en cliquant sur l’onglet **Fichier** et en examinant les informations sous **Protéger le document**. Vous voyez que le document est protégé par **Confidentiel\Finance** et avez accès à la description de l’étiquette. 
    
    En raison de la configuration de protection de l’étiquette, seuls les employés peuvent ouvrir le document et certaines actions uniquement leur sont accessibles. Par exemple, parce qu’ils n’ont pas les autorisations pour imprimer, copier et extraire du contenu, ils ne peuvent pas imprimer le document ni copier son contenu. Ces restrictions permettent d’éviter la perte de données. En tant que propriétaire du document, vous pouvez l’imprimer et copier son contenu, mais si vous l’envoyez par e-mail à un autre utilisateur de votre organisation, il ne peut pas effectuer ces actions.

4. Vous pouvez maintenant fermer ce document.

La classification, l’étiquetage et la protection n’ayant plus de secret pour vous, nous allons voir comment vous pouvez protéger vos documents même quand ils sont partagés avec d’autres personnes dans une autre organisation. Vous pouvez même suivre la façon dont ils sont utilisés et révoquer leur accessibilité.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|Instructions complètes pour l’étiquetage et la protection de fichiers |[Classifier et protéger un fichier ou un e-mail](./rms-client/client-classify-protect.md)|
|Emplacement des journaux de l’activité d’étiquetage |[Journalisation de l’utilisation du client Azure Information Protection](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)|


>[!div class="step-by-step"]
[&#171; Étape 3](infoprotect-tutorial-step3.md)
[Étape 5 &#187;](infoprotect-tutorial-step5.md)
