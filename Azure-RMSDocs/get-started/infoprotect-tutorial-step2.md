---
title: "Étape 2 du didacticiel de démarrage rapide | Azure Information Protection"
description: "Étape 2 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en environ 20 minutes."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 8ad1ff05f642571bfe7f4170cb88e29d05515e59
ms.openlocfilehash: f3ec39af7bdbc63169c09eefa54c29cfc4cee40b


---

# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>Étape 2 : Configurer et publier la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection*

Bien qu’Azure Information Protection soit fourni avec une stratégie par défaut que vous pouvez utiliser sans configuration, nous allons examiner cette stratégie et y apporter des modifications.

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général pour votre locataire.

2. Dans le menu Hub, cliquez sur **Nouveau**, puis, dans la liste **MARKETPLACE**, sélectionnez **Sécurité + Identité**. Dans le panneau **Sécurité + Identité**, dans la liste **Applications proposées**, sélectionnez **Azure Information Protection**. Dans le panneau **Azure Information Protection**, cliquez sur **Créer**.

    Cette opération crée le panneau **Azure Information Protection**. Vous pouvez ainsi sélectionner le service dans la liste **Autres services** du hub lors de votre prochaine connexion au portail. 

    > [!TIP] 
    > Sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.

3.  Sur le panneau Azure Information Protection, cliquez sur **Global** et explorez le panneau **Stratégie : Global**, qui indique la stratégie Information Protection par défaut qui est créée automatiquement :
    
    - Étiquettes de classification : **Personal**, **Public**, **Internal**, **Confidential** et **Secret**. Lisez l’info-bulle de chacune d’elles pour comprendre la façon dont les étiquettes sont censées être utilisées. Notez que **Secret** a deux sous-étiquettes (**All Company** et **My Group**), pour illustrer comment une classification peut avoir des sous-catégories.

    - Avec les paramètres par défaut, les étiquettes **Internal**, **Confidential** et **Secret** ont des marquages visuels configurés (par exemple : pied de page, en-tête, filigrane), et la protection n’est définie pour aucune des étiquettes : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy-default-labels.png)
    
    Certains paramètres de stratégie globaux ne sont pas non plus définis. Ainsi, aucun document ou e-mail n’est obligé d’avoir une étiquette, il n’y a aucune étiquette par défaut, les utilisateurs n’ont pas à fournir de justification quand ils modifient les étiquettes et le client n’est pas configuré pour un lien d’aide personnalisé :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-global-settings-for-a-default-template-and-prompt-for-justification"></a>Modification des paramètres globaux pour un modèle par défaut et une demande de justification

Pour notre didacticiel, nous allons modifier deux de ces paramètres de stratégie globaux pour que vous puissiez voir leur fonctionnement :

1. Pour **Sélectionnez l’étiquette par défaut**, affectez la valeur **Interne**.

2. Pour **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**, affectez la valeur **Activé**.

## <a name="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification"></a>Configuration d’une étiquette pour la protection, d’un filigrane et d’une condition pour une demande de classification

Nous allons maintenant modifier les paramètres de l’une des étiquettes, **Confidentiel** :

1. Cliquez sur l’étiquette **Confidentiel**. 
    
    Dans le nouveau panneau **Étiquette : Confidentiel**, sont répertoriés les paramètres qui sont disponibles pour chaque étiquette. 

2. Dans le panneau **Étiquette : Confidentiel**, recherchez la section **Définir le modèle RMS pour la protection des documents et e-mails contenant cette étiquette** :
    
    Pour l’option **Sélectionner le modèle RMS à partir de**, conservez la valeur par défaut **Azure RMS**. Cliquez ensuite pour **Sélectionner un modèle RMS** sur la zone de liste déroulante et sélectionnez le modèle par défaut **\<nom_de_votre_organisation> - Confidentiel**. 
    
    Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous verrez et sélectionnerez **VanArsdel, Ltd - Confidential** : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Définir la protection Azure RMS](../media/step2-select-rms-template.png)
    
    Si vous avez désactivé ce modèle Azure Rights Management par défaut, sélectionnez un autre modèle. Toutefois, si vous sélectionnez un modèle de service, vérifiez que votre compte est compris dans l’étendue.
    
3. Recherchez la section **Définir un marquage visuel** :
    
    Pour le paramètre **Les documents avec cette étiquette ont un filigrane**, cliquez sur **Activé** puis, dans la zone **Texte**, tapez le nom de votre organisation. Dans notre exemple, **VanArsdel, Ltd** : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Définir la protection Azure RMS](../media/step2-configure-watermark.png)
    
    Bien que vous puissiez modifier la taille, la couleur et la disposition des filigranes, nous laisserons ces paramètres à leurs valeurs par défaut pour le moment.
    
4. Recherchez la section **Configurer des conditions pour appliquer automatiquement cette étiquette** :
    
    Cliquez sur **Ajouter une nouvelle condition**, puis dans le panneau **Condition**, sélectionnez les éléments suivants :
    
    a. **Choisir le type de condition** : conservez la valeur par défaut **Prédéfinie**.
    
    b. **Sélectionner Prédéfinie** : dans la liste déroulante, sélectionnez **Numéro de carte de crédit**.
    
    c. **Nombre minimal d’occurrences** : conservez la valeur par défaut **1**.
    
    d. **Comptabiliser seulement les occurrences avec des valeurs uniques** : conservez la valeur par défaut **Désactivé**.
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-configure-condition.png)
    
    Cliquez sur **Enregistrer** pour revenir au panneau **Étiquette : Confidentiel**.

5. Dans le panneau **Étiquette : Confidentiel**, vous verrez que **Numéro de carte de crédit** est affiché comme **NOM DE LA CONDITION**, avec **1** **OCCURRENCES** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-see-condition.png)

6. Pour **Sélectionner comment cette étiquette est appliquée** : conservez la valeur par défaut **Recommandée** et ne modifiez pas le conseil de stratégie par défaut :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Classification recommandée](../media/step2-keep-recommended.png)

7. Dans la zone **Saisir des notes pour les tâches de nettoyage internes**, tapez **À des fins de test uniquement** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Taper des remarques](../media/step2-type-notes.png)

8. Cliquez sur **Enregistrer** dans le panneau **Étiquette : Confidentiel**. Puis, dans le panneau **Stratégie : Globale**, cliquez une nouvelle fois sur **Enregistrer**.

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut configurée](../media/info-protect-policy-configured.png)

9. Maintenant que nous avons apporté des modifications et les avons enregistrées, nous voulons les mettre à la disposition des utilisateurs. Pour cela, dans le panneau **Azure Information Protection** initial, cliquez sur **Publier**, puis sur **Oui** pour confirmer.

Vous pouvez fermer le portail Azure, ou le laisser ouvert pour essayer des options de configuration supplémentaires après avoir terminé ce didacticiel.

Maintenant que vous avez examiné la stratégie par défaut et apporté des modifications, l’étape suivante consiste à installer le client Azure Information Protection.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos des options de configuration de la stratégie|[Configuration de la stratégie Azure Information Protection](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Étape 1](infoprotect-tutorial-step1.md)
[Étape 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


