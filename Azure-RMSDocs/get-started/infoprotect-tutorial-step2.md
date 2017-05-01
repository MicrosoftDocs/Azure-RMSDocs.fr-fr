---
title: "Didacticiel de démarrage rapide, étape 2 - AIP"
description: "Didacticiel de présentation expliquant comment tester rapidement Azure Information Protection, étape 2 : configurer la stratégie."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
ms.openlocfilehash: 9a2392df400356e7937db49cec3e0fe1e3d0f228
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>Étape 2 : Configurer et publier la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection*

Bien qu’Azure Information Protection soit fourni avec une stratégie par défaut que vous pouvez utiliser sans configuration, nous allons examiner cette stratégie et y apporter des modifications.

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général ou administrateur de la sécurité pour votre locataire.

2. Dans le menu Hub, cliquez sur **Nouveau**, puis, dans la liste **MARKETPLACE**, sélectionnez **Sécurité + Identité**. Dans le panneau **Sécurité + Identité**, dans la liste **Applications proposées**, sélectionnez **Azure Information Protection**. Dans le panneau **Azure Information Protection**, cliquez sur **Créer**.

    Ceci active le service pour votre locataire et crée le panneau **Azure Information Protection**. Vous pouvez ainsi sélectionner le service dans la liste **Autres services** du hub lors de votre prochaine connexion au portail. 

    > [!TIP] 
    > Sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.

3.  Explorez le panneau **Stratégie : Globale**, qui s’ouvre automatiquement et affiche la stratégie Information Protection par défaut automatiquement créée pour votre client :
    
    - Étiquettes de classification : **Personnel**, **Public**, **Interne**, **Confidentiel** et **Hautement confidentiel**. Les deux dernières étiquettes se développent pour afficher des sous-étiquettes : **Tous les employés** et **Tout le monde (sans protection)**, qui sont des exemples de sous-catégories dans une classification.
    
       > [!NOTE]
       > Votre stratégie par défaut peut différer légèrement de celle de ce didacticiel. Par exemple, vous avez une étiquette nommée **Interne** au lieu de **Général**, et **Secret** au lieu de **Hautement confidentiel**. Si tel est le cas, vous utilisez probablement une version plus ancienne de la stratégie par défaut. Vous pouvez aussi avoir l’avoir modifiée vous-même avant de commencer ce didacticiel.
       > 
       > Si votre stratégie par défaut est différente, vous pouvez néanmoins utiliser ce didacticiel, mais n’oubliez pas ces différences quand vous utilisez les instructions et les images qui suivent. Si vous voulez modifier votre stratégie par défaut pour qu’elle corresponde à la stratégie par défaut actuelle, consultez [La stratégie Azure Information Protection par défaut](../deploy-use/configure-policy-default.md).

    - Avec la configuration par défaut, certaines étiquettes n’ont pas de marquages visuels configurés (comme un pied de page, un en-tête, un filigrane) et la protection n’est définie pour aucune des étiquettes : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy-default-labelsv2.png)
    
    Certains paramètres de stratégie ne sont pas non plus définis. Ainsi, certains documents ou e-mails ne sont pas obligés d’avoir une étiquette, il n’y a pas d’étiquette par défaut et les utilisateurs n’ont pas à fournir de justification quand ils modifient les étiquettes :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-settings-for-a-default-label-and-prompt-for-justification"></a>Modification des paramètres pour une étiquette par défaut et demande de justification

Pour notre didacticiel, nous allons modifier deux de ces paramètres de stratégie pour vous permettre de voir comment ils fonctionnent :

1. Pour **Sélectionner l’étiquette par défaut**, affectez la valeur **Général**. 

    Si vous n’avez pas cette étiquette car vous avez une version plus ancienne de la stratégie, choisissez **Interne** comme étiquette équivalente.

2. Pour **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**, affectez la valeur **Activé**.

## <a name="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification"></a>Configuration d’une étiquette pour la protection, d’un filigrane et d’une condition pour une demande de classification

Nous allons maintenant changer les paramètres d’une des sous-étiquettes, **Tous les employés**, de l’étiquette principale **Confidentiel**. 

Si votre étiquette **Confidentiel** n’a pas de sous-étiquettes car vous avez une version plus ancienne de la stratégie, vous pouvez utiliser l’étiquette **Confidentiel** à la place. Les étapes de configuration sont identiques, mais le nom du panneau de l’étiquette est **Confidentiel** au lieu de **Tous les employés**.

1. Vérifiez que l’étiquette **Confidentiel** est développée et, à partir de cette étiquette, sélectionnez **Tous les employés**.
    
    Dans le nouveau panneau **Étiquette : Tous les employés**, vous voyez maintenant les paramètres qui sont disponibles pour chaque étiquette. 

2. Lisez le texte de la **Description** pour cette étiquette. Il explique comment l’étiquette sélectionnée est destinée à être utilisée. Affiché dans une info-bulle, il aide les utilisateurs à décider quelle étiquette sélectionner.

3. Recherchez la section **Définir les autorisations pour les documents et les e-mails contenant cette étiquette** et sélectionnez **Protéger** :
    
    ![Configurer la protection d’une étiquette Azure Information Protection](../media/info-protect-protection-barv2.png) 
    
    Cette action ouvre le panneau **Protection**.
    
3. Dans le panneau **Protection**, assurez-vous que l’option **Azure RMS** est sélectionnée, ainsi que l’option **Sélectionner un modèle prédéfini**, puis cliquez sur la zone de liste déroulante et choisissez le modèle par défaut **\<Nom de votre organisation > Confidentiel**.     
    
    Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous verrez et sélectionnerez **VanArsdel, Ltd - Confidential** : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Définir la protection Azure RMS](../media/step2-select-rms-template.png)
    
    Si vous avez désactivé ce modèle Azure Rights Management par défaut, sélectionnez un autre modèle. Toutefois, si vous sélectionnez un modèle de service, vérifiez que votre compte est compris dans l’étendue.
    
4. Cliquez sur **OK** pour enregistrer vos modifications, ce qui ferme le panneau **Protection**. Vous voyez votre configuration reflétée dans le panneau **Étiquette : Tous les employés** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection - Étape 3 : Protection Azure RMS configurée](../media/protection-bar-configured.png)
    
5. Maintenant, dans le panneau **Étiquette : Tous les employés**, recherchez la section **Définir un marquage visuel** :
    
    Pour le paramètre **Les documents avec cette étiquette ont un filigrane**, cliquez sur **Activé** puis, dans la zone **Texte**, tapez le nom de votre organisation. Dans notre exemple, **VanArsdel, Ltd** : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Définir la protection Azure RMS](../media/step2-configure-watermark.png)
    
    Bien que vous puissiez modifier la taille, la couleur et la disposition des filigranes, nous laisserons ces paramètres à leurs valeurs par défaut pour le moment.
    
6. Recherchez la section **Configurer des conditions pour appliquer automatiquement cette étiquette** :
    
    Cliquez sur **Ajouter une nouvelle condition**, puis dans le panneau **Condition**, sélectionnez les éléments suivants :
    
    a. **Choisir le type de condition** : conservez la valeur par défaut **Prédéfinie**.
    
    b. **Sélectionner Prédéfinie** : dans la liste déroulante, sélectionnez **Numéro de carte de crédit**.
    
    c. **Nombre minimal d’occurrences** : conservez la valeur par défaut **1**.
    
    d. **Comptabiliser seulement les occurrences avec des valeurs uniques** : conservez la valeur par défaut **Désactivé**.
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-configure-condition.png)
    
    Cliquez sur **Enregistrer** pour revenir au panneau **Étiquette : Tous les employés**.

7. Dans le panneau **Étiquette : Tous les employés**, vous voyez que **Numéro de carte de crédit** est affiché comme **NOM DE LA CONDITION**, avec **1** **OCCURRENCES** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-see-condition.png)

8. Pour **Sélectionner comment cette étiquette est appliquée** : conservez la valeur par défaut **Recommandée** et ne modifiez pas le conseil de stratégie par défaut :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Classification recommandée](../media/step2-keep-recommendedv2.png)

9. Dans la zone **Saisir des notes pour les tâches de nettoyage internes**, tapez **À des fins de test uniquement** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Taper des remarques](../media/step2-type-notes.png)

10. Cliquez sur **Enregistrer** sur ce panneau **Étiquette : Tous les employés**. Puis, dans le panneau **Stratégie : Globale**, cliquez une nouvelle fois sur **Enregistrer**.
    
    À ce stade, vos étiquettes indiquent maintenant la protection Azure RMS pour l’étiquette que vous venez de configurer :

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut configurée](../media/info-protect-policy-configuredv2.png)
    
    Les paramètres sont configurés avec vos modifications apportées à l’étiquette par défaut et à la justification :
    
    ![Didacticiel de démarrage rapide Azure Information Protection - Étape 3 : Paramètres configurés](../media/info-protect-settings-configuredv2.png)
    
11. Maintenant que nous avons apporté des modifications et les avons enregistrées, nous voulons les mettre à la disposition des utilisateurs. Pour cela, dans le panneau **Azure Information Protection** initial, cliquez sur **Publier**, puis sur **Oui** pour confirmer.

    ![Didacticiel de démarrage rapide Azure Information Protection - Étape 3 : Publier la stratégie configurée](../media/info-protect-publish.png)

Vous pouvez fermer le portail Azure, ou le laisser ouvert pour essayer des options de configuration supplémentaires après avoir terminé ce didacticiel.

Maintenant que vous avez examiné la stratégie par défaut et apporté des modifications, l’étape suivante consiste à installer le client Azure Information Protection.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos des options de configuration de la stratégie|[Configuration de la stratégie Azure Information Protection](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Étape 1](infoprotect-tutorial-step1.md)
[Étape 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]