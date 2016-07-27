---
title: "Didacticiel de démarrage rapide Azure Information Protection Étape 2 | Azure Rights Management"
description: "Étape 2 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en seulement quatre étapes et moins de 15 minutes."
author: cabailey
manager: mbaldwin
ms.date: 07/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 463c0bc1fa86f73e2623faf5a624afeabcadeedb
ms.openlocfilehash: c6ecf22b72d862c605f8be2ab1f75fd2126f8575


---

# Étape 2 : Configurer et publier la stratégie Azure Information Protection

*S’applique à : Azure Information Protection (préversion)*

Bien qu’Azure Information Protection soit fourni avec une stratégie par défaut que vous pouvez utiliser sans configuration, nous allons examiner cette stratégie et y apporter des modifications.

1. Connectez-vous au portail Azure à l’aide de ce lien spécial pour Azure Information Protection : https://portal.azure.com/?microsoft_azure_informationprotection=true
 
2. Dans le menu hub, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

- Le panneau principal **Azure Information Protection** s’affiche et montre la stratégie Information Protection par défaut créée automatiquement. Cette stratégie par défaut contient les étiquettes de classification suivantes : **Personal**, **Public**, **Internal**, **Confidential** et **Secret**. Lisez l’info-bulle de chacune d’elles pour comprendre la façon dont les étiquettes sont censées être utilisées. Notez que **Secret** a deux sous-étiquettes (**All Company** et **My Group**), pour illustrer comment une classification peut avoir des sous-catégories.

- Avec les paramètres par défaut, **Internal**, **Confidential** et **Secret** ont des marquages visuels configurés (par exemple pied de page, en-tête, filigrane), et la protection n’est définie pour aucune des étiquettes. Les trois paramètres globaux ne sont pas non plus définis. Ainsi, aucun document ou e-mail n’est obligé d’avoir une étiquette, il n’y a aucune étiquette par défaut et les utilisateurs n’ont pas à fournir de justification quand ils abaissent le niveau de confidentialité.

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy.png)

Pour notre didacticiel, nous allons modifier deux de ces paramètres globaux pour que vous puissiez voir leur fonctionnement :

-  **Select the default label** (Sélectionner l’étiquette par défaut) : affectez la valeur **Internal**.

- **Users must provide justification when lowering the sensitivity level (Les utilisateurs doivent fournir une justification quand ils abaissent le niveau de confidentialité)** : affectez la valeur **On**.

Nous allons maintenant modifier les paramètres de l’une des étiquettes, **Confidential** :

1. Cliquez sur l’entrée d’étiquette **Confidential**.

2. Dans le panneau **Label: Confidential** sont répertoriés les paramètres qui sont disponibles pour chaque étiquette. Apportez les modifications suivantes :

    a. Si vous avez activé Azure Rights Management, pour **Select RMS template** (Sélectionner le modèle RMS) : cliquez sur la zone de liste déroulante et sélectionnez le modèle par défaut **\<nom_votre_organisation> - Confidential**. Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous verrez et sélectionnerez **VanArsdel, Ltd - Confidential**. Si vous avez désactivé ce modèle Azure Rights Management par défaut, sélectionnez un autre modèle. Toutefois, si vous sélectionnez un modèle de service, vérifiez que votre compte est compris dans l’étendue.

    Si vous n’avez pas activé Azure Rights Management, vous ne pouvez pas utiliser cette option.

    b. **Documents with this label have a watermark** (Les documents avec cette étiquette ont un filigrane) : cliquez sur **On** et, dans la zone **Text**, tapez le nom de votre organisation. Dans notre exemple, **VanArsdel, Ltd**. 

    c. Cliquez sur **Add a new condition** (Ajouter une nouvelle condition) puis, dans le panneau **Condition**, sélectionnez les éléments suivants :

    - **Choose the type of condition** (Choisir le type de condition) : **Built-in** (intégré)

    - **Select built-in** (Sélectionner intégré) : **Credit Card Number** (Numéro de carte de crédit)

    - **Minimum number of occurrences** (Nombre minimal d’occurrences : **1**

    - Cliquez sur **Save** pour revenir au panneau **Label: Confidential**.

3. Dans le panneau **Label: Confidential**, vous verrez que **Credit Card Number** est affiché comme **CONDITION NAME**, avec **1** **OCCURRENCES**.

4. Conservez la valeur **Select how this label is applied** (Sélectionner comment cette étiquette est appliquée) : **Recommended**.

5. Dans la zone **Enter notes for internal housekeeping** (Entrer des remarques de maintenance interne), tapez **À des fins de test uniquement**.

6. Cliquez sur **Save** dans ce panneau **Label: Confidential** et, dans le panneau **Azure Information Protection** principal, cliquez à nouveau sur **Save**.

7. Maintenant que nous avons effectué et enregistré nos modifications, nous souhaitons qu’elles soient accessibles aux utilisateurs. Cliquez sur **Publish**, puis sur **Yes** pour confirmer.

![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut configurée](../media/info-protect-policy-configured.png)

Vous pouvez fermer le portail Azure, ou le laisser ouvert pour essayer des options de configuration supplémentaires après avoir terminé ce didacticiel.

Maintenant que vous avez examiné la stratégie par défaut et apporté des modifications, l’étape suivante consiste à installer le client Azure Information Protection.


>[!div class="step-by-step"]
[&#171; Étape 1](infoprotect-tutorial-step1.md)
[Étape 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Jul16_HO3-->


