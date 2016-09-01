---
title: "Didacticiel de démarrage rapide Azure Information Protection Étape 2 | Azure Rights Management"
description: "Étape 2 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en seulement quatre étapes et moins de 15 minutes."
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 09cb56aaa0d7d97073623c518aa331d591a376e3
ms.openlocfilehash: 65d758635b77ee7d6c423a1400a7621e8e05b14d


---

# Étape 2 : Configurer et publier la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Bien qu’Azure Information Protection soit fourni avec une stratégie par défaut que vous pouvez utiliser sans configuration, nous allons examiner cette stratégie et y apporter des modifications.

1. Connectez-vous au [portail Azure](https://portal.azure.com). Si vous souhaitez tester la protection ainsi que la classification et l’étiquetage, connectez-vous en tant qu’administrateur général pour pouvoir récupérer les modèles Azure Rights Management.
 
2. Dans le menu hub : cliquez sur **Nouveau** > **Sécurité + Identité** > **Azure Information Protection (préversion)** > **Créer**.

    Cette opération crée le panneau **Azure Information Protection**. Vous pourrez ainsi sélectionner le service dans la liste **Parcourir** du hub la prochaine fois que vous vous connecterez au portail. 

    > [!TIP] 
    > Sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous pourrez ainsi ignorer l’étape Parcourir la prochaine fois que vous vous connecterez au portail.

3.  Le panneau principal **Azure Information Protection** indique la stratégie Information Protection par défaut qui est créée automatiquement :
    
    - Étiquettes de classification : **Personal**, **Public**, **Internal**, **Confidential** et **Secret**. Lisez l’info-bulle de chacune d’elles pour comprendre la façon dont les étiquettes sont censées être utilisées. Notez que **Secret** a deux sous-étiquettes (**All Company** et **My Group**), pour illustrer comment une classification peut avoir des sous-catégories.

    - Avec les paramètres par défaut, les étiquettes **Internal**, **Confidential** et **Secret** ont des marquages visuels configurés (par exemple : pied de page, en-tête, filigrane), et la protection n’est définie pour aucune des étiquettes. Les trois paramètres globaux ne sont pas non plus définis. Ainsi, aucun document ou e-mail n’est obligé d’avoir une étiquette, il n’y a aucune étiquette par défaut et les utilisateurs n’ont pas à fournir de justification quand ils abaissent le niveau de confidentialité.

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy.png)

Pour notre didacticiel, nous allons modifier deux de ces paramètres globaux pour que vous puissiez voir leur fonctionnement :

-  **Select the default label** (Sélectionner l’étiquette par défaut) : affectez la valeur **Internal**.

- **Users must provide justification when lowering the sensitivity level (Les utilisateurs doivent fournir une justification quand ils abaissent le niveau de confidentialité)** : affectez la valeur **On**.

Nous allons maintenant modifier les paramètres de l’une des étiquettes, **Confidential** :

1. Cliquez sur l’étiquette **Confidential**.

2. Dans le panneau **Label: Confidential** sont répertoriés les paramètres qui sont disponibles pour chaque étiquette. Apportez les modifications suivantes :

    a. Si vous avez activé Azure Rights Management : dans la section **Définir le modèle RMS pour la protection des documents et e-mails contenant cette étiquette**, si vous voyez **Sélectionner le modèle RMS à partir de**, conservez la valeur par défaut **Azure RMS**. Cliquez ensuite pour **Sélectionner un modèle RMS** sur la zone de liste déroulante et sélectionnez le modèle par défaut **\<nom_de_votre_organisation> - Confidentiel**. Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous verrez et sélectionnerez **VanArsdel, Ltd - Confidential**. Si vous avez désactivé ce modèle Azure Rights Management par défaut, sélectionnez un autre modèle. Toutefois, si vous sélectionnez un modèle de service, vérifiez que votre compte est compris dans l’étendue.
    
    Si vous n’avez pas activé Azure Rights Management, vous ne pouvez pas utiliser cette option.
    
    b. **Documents with this label have a watermark** (Les documents avec cette étiquette ont un filigrane) : cliquez sur **On** et, dans la zone **Text**, tapez le nom de votre organisation. Dans notre exemple, **VanArsdel, Ltd**. 
    
    c. Cliquez sur **Add a new condition** (Ajouter une nouvelle condition) puis, dans le panneau **Condition**, sélectionnez les éléments suivants :
    
    - **Choose the type of condition** (Choisir le type de condition) : **Built-in** (intégré)
    
    - **Select built-in** (Sélectionner intégré) : **Credit Card Number** (Numéro de carte de crédit)
    
    - **Minimum number of occurrences** (Nombre minimal d’occurrences : **1**
    
    - **Compter les occurrences avec des valeurs uniques uniquement** : **Activé**
    
    - Cliquez sur **Save** pour revenir au panneau **Label: Confidential**.

3. Dans le panneau **Label: Confidential**, vous verrez que **Credit Card Number** est affiché comme **CONDITION NAME**, avec **1** **OCCURRENCES**.

4. Conservez la valeur **Select how this label is applied** (Sélectionner comment cette étiquette est appliquée) : **Recommended**.

5. Dans la zone **Enter notes for internal housekeeping** (Entrer des remarques de maintenance interne), tapez **À des fins de test uniquement**.

6. Cliquez sur **Save** dans ce panneau **Label: Confidential** et, dans le panneau **Azure Information Protection** principal, cliquez à nouveau sur **Save**.

7. Maintenant que nous avons effectué et enregistré nos modifications, nous souhaitons qu’elles soient accessibles aux utilisateurs. Cliquez sur **Publish**, puis sur **Yes** pour confirmer.

![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut configurée](../media/info-protect-policy-configured.png)

Vous pouvez fermer le portail Azure, ou le laisser ouvert pour essayer des options de configuration supplémentaires après avoir terminé ce didacticiel.

Maintenant que vous avez examiné la stratégie par défaut et apporté des modifications, l’étape suivante consiste à installer le client Azure Information Protection.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos des options de configuration de la stratégie|[Configuration de la stratégie Azure Information Protection](configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Étape 1](infoprotect-tutorial-step1.md)
[Étape 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Aug16_HO2-->


