---
title: "Didacticiel de démarrage rapide Azure Information Protection Étape 4 | Azure Rights Management"
description: "Étape 4 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en seulement quatre étapes et moins de 15 minutes."
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: d17bacf8e148622db0e2393f40d3fd37c8f086eb
ms.openlocfilehash: a36433167462275e91059f9eb3a2141ffa2797d5


---

# Étape 4 : classification, étiquetage et protection en action 

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Maintenant que vous avez un document Word ouvert avec le client Azure Information Protection installé, vous allez voir combien il est facile d’étiqueter et de protéger votre document à l’aide de la stratégie que nous avons configurée.

La classification et la protection ont lieu quand vous enregistrez le document, mais avant cela, nous allons utiliser notre document non enregistré pour voir combien il est facile d’appliquer et de modifier les étiquettes.

### Pour modifier manuellement notre étiquette par défaut

- Dans la barre Information Protection, sélectionnez l’étiquette **Personal** (Personnel). Vous êtes alors invité à indiquer pourquoi vous abaissez le niveau de classification. Sélectionnez **This file no longer requires that classification** (Ce fichier n’a plus besoin de cette classification), puis cliquez sur **Confirm**.  

    **Sensitivity** (Niveau de confidentialité) prend la valeur **Personal** (Personnel).

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de confirmation de l’abaissement](../media/confirm-lowering.png)

### Pour supprimer complètement la classification

- Dans la barre Information Protection, cliquez sur l’icône **Edit label** (Modifier l’étiquette) à côté de **Personal** (Personnel). Les étiquettes disponibles apparaissent. Au lieu de choisir l’une des étiquettes, cliquez sur l’icône **Remove label** (Supprimer l’étiquette). Cliquez sur **OK** pour confirmer, puis indiquez la justification de cette action.  

    La valeur **Sensitivity** (Niveau de confidentialité) indique **Not set** (Non défini), ce qui correspond à ce que les utilisateurs voient initialement si vous ne définissez pas d’étiquette par défaut.

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : supprimer la classification](../media/sensitivity-not-set.png)


### Pour afficher une invite de recommandation pour l’étiquetage et la protection automatique

1. Dans le document Word, tapez un numéro de carte de crédit valide, par exemple **4242-4242-4242-4242**. 

2. Enregistrez le document (utilisez n’importe quel nom de fichier et n’importe quel emplacement). 

3. L’invite suivante s’affiche : **It is recommended to label this file as Confidential** (Nous vous recommandons d’étiqueter ce fichier comme Confidentiel). Cliquez sur **Change now** (Modifier maintenant).

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 4 : invite de recommandation](../media/change-now.png)

    Le filigrane de votre organisation apparaît tout de suite sur la page, en plus du pied de page **Sensitivity: Confidential**. 

    Si vous avez choisi l’option pour appliquer un modèle RMS, le document est également protégé avec le modèle Azure Rights Management que vous avez spécifié, ce que vous pouvez vérifier en cliquant sur l’onglet **Fichier** et en affichant les informations **Protéger le document**. Si vous avez utilisé le modèle Confidential par défaut, un message précise que l’accès au document est limité aux utilisateurs internes (les utilisateurs extérieurs à votre organisation ne pourront pas l’ouvrir) et que son contenu ne peut pas être copié ou imprimé. En tant que propriétaire du document, vous pouvez le copier et l’imprimer, mais si vous l’envoyez à un autre utilisateur de votre organisation, il ne pourra pas effectuer ces actions.

> [!NOTE]
>Si vous rencontrez des problèmes lors de ces étapes, sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. 
>
>Dans la boîte de dialogue **Microsoft Azure Information Protection**, cliquez sur **Envoyer des commentaires**. Un e-mail est envoyé à l’équipe Information Protection et les fichiers journaux de votre ordinateur sont joints automatiquement pour aider à diagnostiquer tout problème.

##  Étapes suivantes

Maintenant que vous avez vu comment personnaliser la stratégie Azure Information Protection par défaut et comment fonctionne l’étiquetage d’un document Word, essayez d’appliquer certains autres paramètres pour voir comment ils fonctionnent dans les autres applications Office qui prennent en charge Azure Information Protection : Excel, PowerPoint et Outlook. Si ces applications étaient ouvertes quand vous avez installé le client Azure Information Protection, fermez et rouvrez-les avant d’essayer de les utiliser avec Azure Information Protection.

Par exemple, vous pouvez remplacer le titre par défaut **Sensitivity** (Niveau de confidentialité) dans la barre Information Protection par le titre de votre choix. Vous pouvez modifier les info-bulles, les couleurs des étiquettes, l’ordre des étiquettes et leurs noms. Vous pouvez créer des étiquettes et définir vos propres règles automatiques. Vous pouvez affiner vos filigranes en configurant la taille et la couleur, et en passant de diagonal à horizontal.

Notez que si vous utilisez des filigranes avec Excel, ils sont visibles uniquement en mode Mise en page et Aperçu avant impression, ainsi que lors de l’impression.

Chaque fois que vous modifiez des paramètres dans le portail Azure pour la stratégie Information Protection, n’oubliez pas d’**Enregistrer** la stratégie, puis de la **Publier**. Étant donné que vous pouvez apporter des modifications sur plusieurs panneaux, il vaut mieux vérifier qu’aucun panneau n’affiche un bouton **Enregistrer** activé, ce qui indiquerait que vous avez des modifications non enregistrées. Si votre application Office était ouverte quand vous avez publié de nouvelles modifications, fermez-la et rouvrez-la pour télécharger la dernière stratégie.

Quand vous avez terminé vos propres tests, il peut être utile de consulter le [Forum aux questions d’Azure Information Protection](faq.md).




<!--HONumber=Aug16_HO2-->


