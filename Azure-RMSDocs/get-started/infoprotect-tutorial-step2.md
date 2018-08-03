---
title: Didacticiel de démarrage rapide, étape 2 - AIP
description: 'Didacticiel de présentation expliquant comment tester rapidement Azure Information Protection, étape 2 : configurer la stratégie.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
ms.openlocfilehash: fca6e6e2ee2c229b718c74ee3c26a2644911a241
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39372306"
---
# <a name="step-2-configure-the-azure-information-protection-policy"></a>Étape 2 : Configurer la stratégie Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Bien qu’Azure Information Protection soit fourni avec une stratégie par défaut que vous pouvez utiliser sans configuration, nous allons examiner cette stratégie et y apporter des modifications.

1. Toujours à partir de l’[étape 1](infoprotect-tutorial-step1.md) dans le portail Azure, sélectionnez **CLASSIFICATIONS** > **Stratégies** > **Globale** pour ouvrir le panneau **Stratégie : Globale**. Ce panneau affiche la stratégie Azure Information Protection par défaut qui est créée pour votre locataire.

2. Prenez quelques minutes pour vous familiariser avec les étiquettes affichées :
    
    - Étiquettes de classification : **Personnel**, **Public**, **Interne**, **Confidentiel** et **Hautement confidentiel**. Les deux dernières étiquettes se développent pour afficher des sous-étiquettes, qui sont des exemples de sous-catégories dans une classification :
    
       > [!NOTE]
       > Votre stratégie par défaut peut différer légèrement de celle de ce didacticiel. Par exemple, vous avez une étiquette nommée **Interne** au lieu de **Général**, et **Secret** au lieu de **Hautement confidentiel**. Vous ne voyez peut-être pas les sous-étiquettes nommées **Destinataires uniquement** ou vous n’avez aucune étiquette. La raison de ces changements est qu’il existe différentes versions de la stratégie par défaut, selon le moment où elle a été créée pour votre locataire. Vous pouvez aussi avoir l’avoir modifiée vous-même avant de commencer ce didacticiel.
       > 
       > Si votre stratégie par défaut est différente, vous pouvez néanmoins utiliser ce didacticiel, mais n’oubliez pas ces différences quand vous utilisez les instructions et les images qui suivent. Si vous voulez modifier votre stratégie par défaut pour qu’elle corresponde à la stratégie par défaut actuelle, consultez [La stratégie Azure Information Protection par défaut](../deploy-use/configure-policy-default.md).
    
    - Avec la configuration par défaut, des marquages visuels ne sont pas configurés pour certaines étiquettes. Les marquages visuels sont un pied de page, un en-tête et un filigrane. En fonction de votre stratégie par défaut, la protection peut ou non être définie pour certaines étiquettes. Par exemple : 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy-default-labelsv2.png)
    
3. Après les étiquettes, dans la section **Configurer les paramètres à afficher et à appliquer aux utilisateurs finaux d’Information Protection**, vous voyez également certains paramètres de stratégie. Par exemple, aucune étiquette par défaut n’est définie, les documents ou e-mails ne doivent pas obligatoirement avoir une étiquette et les utilisateurs n’ont pas à fournir de justification quand ils changent les étiquettes :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-settings-for-a-default-label-and-prompt-for-justification"></a>Modification des paramètres pour une étiquette par défaut et demande de justification

Pour ce tutoriel, nous allons modifier deux de ces paramètres de stratégie pour vous permettre de voir comment ils fonctionnent :

1. Pour **Sélectionner l’étiquette par défaut**, choisissez **Général**. 

    Si vous n’avez pas cette étiquette car vous avez une version plus ancienne de la stratégie, choisissez **Interne** comme étiquette équivalente.

2. Pour **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**, définissez cette option sur **Activé**.

3. De plus, recherchez le paramètre **Mettre l’option des autorisations personnalisées à la disposition des utilisateurs**. Si ce paramètre est défini sur **Off** (Désactivé), définissez-le sur **On** (Activé).
    
    Vous n’aurez peut-être pas à changer ce paramètre, car la valeur par défaut dépend du moment où vous avez obtenu votre abonnement. Nous allons utiliser des autorisations personnalisées plus loin dans le didacticiel pour partager un document protégé avec un utilisateur que vous spécifiez quand vous cliquez avec le bouton droit sur le fichier dans l’Explorateur de fichiers.

4. Sélectionnez **Enregistrer** sur ce panneau **Stratégie : Globale** et, si vous êtes invité à confirmer votre action, sélectionnez **OK**. Fermez ce panneau.

## <a name="creating-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>Création d’une étiquette pour la protection, de marquages visuels et d’une condition pour une demande de classification

Nous allons maintenant créer une sous-étiquette pour **Confidentiel**.

1. À partir de l’option de menu **CLASSIFICATIONS** > **Étiquettes** : cliquez avec le bouton droit sur l’étiquette **Confidentiel** et sélectionnez **Ajouter une sous-étiquette**.
    
    Si vous n’avez pas d’étiquette nommée **Confidentiel**, vous pouvez sélectionner une autre étiquette ou créer une étiquette, puis suivre le didacticiel avec des différences mineures.

2. Dans le panneau **Sous-étiquette**, spécifiez le nom d’étiquette **Finance** et ajoutez la description suivante : **Données confidentielles qui contiennent des informations financières réservées aux employés uniquement**.
    
    Ce texte explique comment l’étiquette sélectionnée va être utilisée et s’affiche sous forme d’info-bulle pour aider les utilisateurs dans leur choix.

3. Pour **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Protéger**, puis **Protection** :
    
    ![Protection configurée pour une étiquette Azure Information Protection](../media/info-protect-protection-bar-configured.png) 
    
4. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé du cloud)** est sélectionnée. Cette option utilise le service Azure Rights Management pour protéger les documents et les e-mails. Vérifiez aussi que l’option **Définir les autorisations** est sélectionnée. Ensuite, sélectionnez **Ajouter des autorisations**.

5. Dans le panneau **Ajouter des autorisations**, sélectionnez **Ajouter \<nom de l’organisation> - Tous les membres**. Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous voyez et sélectionnez l’option suivante :
    
    ![Accorder des autorisations de protection à tous les membres pour une étiquette Azure Information Protection](../media/info-protect-protection-all-members.png) 
    
    Cette option sélectionne automatiquement tous les utilisateurs de votre organisation qui peuvent recevoir des autorisations. Toutefois, d’autres options vous permettent de parcourir et de rechercher des groupes ou utilisateurs dans votre locataire. Sinon, quand vous sélectionnez l’option **Entrer les détails**, vous pouvez spécifier des adresses e-mail individuelles ou tous les utilisateurs d’une autre organisation.

6. Pour les autorisations, sélectionnez **Réviseur** dans les options prédéfinies. Vous voyez comment ce niveau d’autorisation accorde automatiquement certaines autorisations répertoriées, mais pas toutes les autorisations :
    
    ![Accorder des autorisations de protection de coauteur pour une étiquette Azure Information Protection](../media/info-protect-protection-reviewer.png)
    
    Vous pouvez sélectionner différents niveaux d’autorisation ou spécifier des droits d’utilisation individuels à l’aide de l’option **Personnalisé**. Dans ce didacticiel, nous utilisons l’option **Réviseur**. Vous pourrez tester différentes autorisations par la suite et découvrir comment limiter les actions des utilisateurs spécifiés sur le document protégé ou l’e-mail.

7. Cliquez sur **OK** pour fermer le panneau **Ajouter des autorisations**. Le panneau **Protection** est mis à jour pour refléter votre configuration. Par exemple :
    
     ![Panneau Protection affichant la configuration des autorisations pour une étiquette Azure Information Protection](../media/info-protect-protection-configured.png)
    
    Si vous sélectionnez **Ajouter des autorisations**, le panneau **Ajouter des autorisations** s’ouvre à nouveau pour vous permettre d’ajouter des utilisateurs et de leur accorder des autorisations différentes. Par exemple, accordez uniquement un accès en consultation à un groupe spécifique. Dans ce didacticiel, nous utilisons un seul jeu d’autorisations pour tous les utilisateurs.

8. Passez en revue et conservez les valeurs par défaut pour l’expiration du contenu et l’accès hors connexion, puis cliquez sur **OK** pour enregistrer et fermer le panneau **Protection**.

8. Revenez au panneau **Sous-étiquette** et recherchez la section **Définir un marquage visuel** :
    
    Pour le paramètre **Les documents avec cette étiquette ont un pied de page**, cliquez sur **Activé**, puis, dans la zone **Texte**, tapez **Classé confidentiel**. 
    
    Pour le paramètre **Les documents avec cette étiquette ont un filigrane**, cliquez sur **Activé** puis, dans la zone **Texte**, tapez le nom de votre organisation. Par exemple, **VanArsdel, Ltd** 
    
    Bien que vous puissiez changer l’apparence des marquages visuels, nous utilisons pour le moment les valeurs par défaut de ces paramètres.
    
9. Recherchez la section **Configurer des conditions pour appliquer automatiquement cette étiquette** :
    
    Cliquez sur **Ajouter une nouvelle condition**, puis, dans le panneau **Condition**, sélectionnez les éléments suivants :
    
    a. **Choisir le type de condition** : conservez la valeur par défaut **Types d’informations**.
    
    b. Dans la zone de recherche **Sélectionner les types d’informations** : tapez **Numéro de carte de crédit**. Ensuite, dans les résultats de recherche, sélectionnez **Numéro de carte de crédit**.
    
    c. **Nombre minimal d’occurrences** : conservez la valeur par défaut **1**.
    
    d. **Comptabiliser seulement les occurrences avec des valeurs uniques** : conservez la valeur par défaut **Désactivé**.
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-configure-condition.png)
    
    Cliquez sur **Enregistrer** pour revenir au panneau **Sous-étiquette**.

10. Dans le panneau **Sous-étiquette**, vous voyez que **Numéro de carte de crédit** est affiché comme **NOM DE LA CONDITION**, avec **1** **OCCURRENCES** :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : Configurer la condition de la carte de crédit](../media/step2-see-condition.png)

11. Pour **Sélectionner comment cette étiquette est appliquée** : conservez la valeur par défaut **Recommandé** et ne modifiez pas le conseil de stratégie par défaut. 

12. Dans la zone **Enter notes for internal housekeeping** (Entrer des remarques de maintenance interne), tapez **À des fins de test uniquement**.

13. Cliquez sur **Enregistrer** dans ce panneau **Sous-étiquette**. Si vous êtes invité à confirmer, cliquez sur **OK**. La nouvelle étiquette est créée et enregistrée, mais elle n’est pas encore ajoutée à une stratégie.

14. À partir de l’option de menu **CLASSIFICATIONS** > **Stratégies** : sélectionnez à nouveau **Globale**, puis sélectionnez le lien **Ajouter ou supprimer des étiquettes** situé en regard des étiquettes.

15. À partir du panneau **Stratégie : ajouter ou supprimer des étiquettes**, sélectionnez l’étiquette que vous venez de créer, la sous-étiquette nommée **Finance** et cliquez sur **OK**.

16. Dans le panneau **Stratégie : Globale**, votre nouvelle sous-étiquette s’affiche désormais dans votre stratégie globale, qui est configurée pour le marquage visuel et la protection. Par exemple :

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut configurée](../media/info-protect-policy-configuredv2.png)
    
    Vous voyez aussi que les paramètres sont configurés avec les modifications que vous avez apportées à l’étiquette par défaut et à la justification :
    
    ![Didacticiel de démarrage rapide Azure Information Protection - Étape 3 : Paramètres configurés](../media/info-protect-settings-configuredv2.png)
    

17. Cliquez sur **Enregistrer** sur ce panneau **Stratégie : Globale**. Si vous êtes invité à confirmer cette action, cliquez sur **OK**.

Vous pouvez fermer le portail Azure, ou le laisser ouvert pour essayer des options de configuration supplémentaires après avoir terminé ce didacticiel.

Maintenant que vous avez examiné la stratégie par défaut et apporté des modifications, l’étape suivante consiste à installer le client Azure Information Protection.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de la stratégie par défaut et des différentes versions|[La stratégie Azure Information Protection par défaut](../deploy-use/configure-policy-default.md)|
|À propos de la configuration de la stratégie|[Configuration de la stratégie Azure Information Protection](../deploy-use/configure-policy.md)|
|Instructions détaillées pour la configuration d’une étiquette pour la protection|[Guide pratique pour configurer une étiquette pour la protection Rights Management](../deploy-use/configure-policy-protection.md)|
|Informations détaillées sur les autorisations|[Configuration des droits d’utilisation pour Azure Rights Management](../deploy-use/configure-usage-rights.md)|



>[!div class="step-by-step"]
[&#171; Étape 1](infoprotect-tutorial-step1.md)
[Étape 3 &#187;](infoprotect-tutorial-step3.md)
