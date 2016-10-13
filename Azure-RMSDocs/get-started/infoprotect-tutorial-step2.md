---
title: "Étape 1 du didacticiel de démarrage rapide | Azure Information Protection"
description: "Étape 2 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en environ 30 minutes."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: b23022c5fbec3d4f6f19ab5017ecf9badf01a9e7
ms.openlocfilehash: c8cad9c4b6efe2630843bcb1618ecd535670e0fe


---

# Étape 2 : Configurer et publier la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection*

Bien qu’Azure Information Protection soit fourni avec une stratégie par défaut que vous pouvez utiliser sans configuration, nous allons examiner cette stratégie et y apporter des modifications.

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général pour votre locataire.

2. Dans le menu Hub, cliquez sur **Nouveau**, puis, dans la liste **MARKETPLACE**, sélectionnez **Sécurité + Identité**. Dans le panneau **Sécurité + Identité**, dans la liste **Applications proposées**, sélectionnez **Azure Information Protection**. Dans le panneau **Azure Information Protection**, cliquez sur **Créer**.

    Cette opération crée le panneau **Azure Information Protection**. Vous pouvez ainsi sélectionner le service dans la liste **Autres services** du hub lors de votre prochaine connexion au portail. 

    > [!TIP] 
    > Sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.

3.  Le panneau principal **Azure Information Protection** indique la stratégie Information Protection par défaut qui est créée automatiquement :
    
    - Étiquettes de classification : **Personal**, **Public**, **Internal**, **Confidential** et **Secret**. Lisez l’info-bulle de chacune d’elles pour comprendre la façon dont les étiquettes sont censées être utilisées. Notez que **Secret** a deux sous-étiquettes (**All Company** et **My Group**), pour illustrer comment une classification peut avoir des sous-catégories.

    - Avec les paramètres par défaut, les étiquettes **Internal**, **Confidential** et **Secret** ont des marquages visuels configurés (par exemple : pied de page, en-tête, filigrane), et la protection n’est définie pour aucune des étiquettes. Les trois paramètres globaux ne sont pas non plus définis. Ainsi, aucun document ou e-mail n’est obligé d’avoir une étiquette, il n’y a aucune étiquette par défaut et les utilisateurs n’ont pas à fournir de justification quand ils abaissent le niveau de classification.

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy.png)

## Modification des paramètres globaux pour un modèle par défaut et une demande de justification

Pour notre didacticiel, nous allons modifier deux de ces paramètres globaux pour que vous puissiez voir leur fonctionnement :

1. Pour **Select the default label** (Sélectionner l’étiquette par défaut), affectez la valeur **Internal**.

2. Pour **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Les utilisateurs doivent fournir une justification pour définir une étiquette de classification d’un niveau inférieur, supprimer une étiquette ou enlever la protection), affectez la valeur **On**.

## Configuration d’une étiquette pour la protection, d’un filigrane et d’une condition pour une demande de classification

Nous allons maintenant modifier les paramètres de l’une des étiquettes, **Confidential** :

1. Cliquez sur l’étiquette **Confidential**. 
    
    Dans le nouveau panneau **Label: Confidential** (Étiquette : Confidentiel) sont répertoriés les paramètres qui sont disponibles pour chaque étiquette. 

2. Dans le panneau **Label: Confidential**, recherchez la section **Set RMS template for protecting documents and emails containing this label** (Définir le modèle RMS pour la protection des documents et e-mails contenant cette étiquette) :
    
    Pour l’option **Select RMS template from** (Sélectionner le modèle RMS à partir de), conservez la valeur par défaut **Azure RMS**. Cliquez ensuite pour **Sélectionner un modèle RMS** sur la zone de liste déroulante et sélectionnez le modèle par défaut **\<nom_de_votre_organisation> - Confidentiel**. 
    
    Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous verrez et sélectionnerez **VanArsdel, Ltd - Confidential** : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Définir la protection Azure RMS](../media/step2-select-rms-template.png)
    
    Si vous avez désactivé ce modèle Azure Rights Management par défaut, sélectionnez un autre modèle. Toutefois, si vous sélectionnez un modèle de service, vérifiez que votre compte est compris dans l’étendue.
    
3. Recherchez la section **Set visual marking** (Activer le marquage visuel) :
    
    Pour le paramètre **Documents with this label have a watermark** (Les documents avec cette étiquette ont un filigrane), cliquez sur **On** puis, dans la zone **Text**, tapez le nom de votre organisation. Dans notre exemple, **VanArsdel, Ltd** : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Définir la protection Azure RMS](../media/step2-configure-watermark.png)
    
    Bien que vous puissiez modifier la taille, la couleur et la disposition des filigranes, nous laisserons ces paramètres à leurs valeurs par défaut pour le moment.
    
4. Recherchez la section **Configure conditions for automatically applying this label** (configurer les conditions de l’application automatique de cette étiquette) :
    
    Cliquez sur **Add a new condition** (Ajouter une nouvelle condition) puis, dans le panneau **Condition**, sélectionnez les éléments suivants :
    
    a. **Choose the type of condition** (Choisir le type de condition) : conservez la valeur par défaut **Built-in** (Intégrée).
    
    b. **Select built-in** (Sélectionner prédéfini) : dans la liste déroulante, sélectionnez **Credit Card Number** (Numéro de carte de crédit).
    
    c. **Minimum number of occurrences** (Nombre minimal d’occurrences) : conservez la valeur par défaut **1**.
    
    d. **Count occurrences with unique values only** (Compter les occurrences avec des valeurs uniques uniquement) : conservez la valeur par défaut **Off** (Désactivé).
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-configure-condition.png)
    
    Cliquez sur **Save** pour revenir au panneau **Label: Confidential**.

5. Dans le panneau **Label: Confidential**, vous verrez que **Credit Card Number** est affiché comme **CONDITION NAME**, avec **1** **OCCURRENCES** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-see-condition.png)

6. Pour **Select how this label is applied** (Sélectionner comment cette étiquette est appliquée) : conservez la valeur par défaut **Recommended** (Recommandé), et ne modifiez pas le conseil de stratégie par défaut :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Classification recommandée](../media/step2-keep-recommended.png)

7. Dans la zone **Enter notes for internal housekeeping** (Entrer des remarques de maintenance interne), tapez **À des fins de test uniquement** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Taper des remarques](../media/step2-type-notes.png)

8. Cliquez sur **Save** (Enregistrer) dans le panneau **Label: Confidential** (Étiquette : Confidentiel). Ensuite, dans le panneau principal **Azure Information Protection**, recliquez sur **Save**.

9. Maintenant que nous avons effectué et enregistré nos modifications, nous souhaitons qu’elles soient accessibles aux utilisateurs. Cliquez sur **Publish**, puis sur **Yes** pour confirmer.

![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut configurée](../media/info-protect-policy-configured.png)

Vous pouvez fermer le portail Azure, ou le laisser ouvert pour essayer des options de configuration supplémentaires après avoir terminé ce didacticiel.

Ayant examiné la stratégie par défaut et apporté des modifications, vous pouvez passer à l’étape suivante, qui consiste à installer le client Azure Information Protection et l’application de partage Rights Management.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos des options de configuration de la stratégie|[Configuration de la stratégie Azure Information Protection](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Étape 1](infoprotect-tutorial-step1.md)
[Étape 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Sep16_HO4-->


