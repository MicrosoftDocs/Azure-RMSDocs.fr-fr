---
title: 'Tutoriel : Modifier la stratégie Azure Information Protection et créer une étiquette – AIP'
description: Tutoriel de prise en main d’environ 15 minutes, permettant de modifier la stratégie Azure Information Protection dans votre organisation.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2019
ms.topic: tutorial
ms.service: information-protection
ms.openlocfilehash: 2e08b21deb8d1b7ef99d77f56e1bf149a82df081
ms.sourcegitcommit: 9a9c55c96a7e99bcca742e759a3f08507e3b9801
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55231053"
---
# <a name="tutorial-edit-the-azure-information-protection-policy-and-create-a-new-label"></a>Didacticiel : Modifier la stratégie Azure Information Protection et créer une étiquette

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Dans ce tutoriel, vous allez apprendre à :
> [!div class="checklist"]
> * configurer des paramètres de stratégie,
> * Créer une étiquette 
> * Configurer l’étiquette pour les marquages visuels ainsi que pour le classement et la protection recommandés
> * Voir vos paramètres et étiquettes en action

Grâce à cette configuration, les utilisateurs observent l’application d’une étiquette par défaut lorsqu’ils créent un nouveau document ou e-mail. Toutefois, ils sont invités à appliquer la nouvelle étiquette lorsque des informations relatives à une carte de crédit sont détectées. Lorsque la nouvelle étiquette est appliquée, le contenu est reclassé et protégé, et affiche un pied de page et un filigrane correspondants. 

Ce tutoriel prend environ 15 minutes.

## <a name="prerequisites"></a>Prérequis 

Pour suivre ce tutoriel, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 2.
    
    Si vous n’avez pas d’abonnement incluant Azure Information Protection Plan 2, vous pouvez créer un compte [gratuit](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. Vous avez ajouté le panneau Azure Information Protection au Portail Azure et vérifié que le service de protection est activé.

    Si vous avez besoin d’aide avec ces actions, consultez [Démarrage rapide : Ajouter Azure Information Protection au portail Azure et afficher la stratégie](quickstart-viewpolicy.md)

3. Le client Azure Information Protection est installé sur votre ordinateur. 
    
    Pour installer le client, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et téléchargez **AzInfoProtection.exe** sur la page Azure Information Protection.

4. Un ordinateur exécutant Windows (au minimum Windows 7 avec Service Pack 1). Sur cet ordinateur, vous êtes connecté aux applications Office de l’une des catégories suivantes :
    
    - Applications Office version minimale 1805, build 9330.2078 d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) vous est affectée.
    
    - Office 365 ProPlus.
    
    - Office Professionnel Plus 2019.
    
    - Office Professionnel Plus 2016.
    
    - Office Professionnel Plus 2013 avec Service Pack 1.
    
    - Office Professionnel Plus 2010 avec Service Pack 2.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

C’est parti !

## <a name="edit-the-azure-information-protection-policy"></a>Modifier la stratégie Azure Information Protection

À l’aide du portail Azure, nous allons tout d’abord modifier quelques paramètres de stratégie puis créer une nouvelle étiquette.

### <a name="edit-the-policy-settings"></a>Modifier les paramètres de stratégie

1. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général. Accédez ensuite à **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Sélectionnez **Classifications** > **Stratégies** > **Global** pour ouvrir le panneau **Stratégie : Globale**. 

3. Localisez les paramètres de stratégie après les étiquettes, dans la section **Configurer les paramètres à présenter et à appliquer aux utilisateurs finaux d’Information Protection**. 
    
    Notez la façon dont les paramètres sont actuellement configurés. Il s’agit spécifiquement des paramètres **Sélectionner l’étiquette par défaut** et **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**. Par exemple :
    
    ![Tutoriel Azure Information Protection : paramètres de stratégie à modifier](./media/info-protect-policy-default-settings.png)
    
    Nous utiliserons ces paramètres de stratégie plus loin dans ce tutoriel lorsque vous les verrez en action.

4. Pour **Sélectionner l’étiquette par défaut**, choisissez **Général**. 

    Si vous n’avez pas cette étiquette car vous avez une version plus ancienne de la stratégie, choisissez **Interne** comme étiquette équivalente.

5. Pour **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**, définissez cette option sur **Activé**, le cas échéant.

6. Par ailleurs, assurez-vous que le paramètre **Afficher la barre Information Protection dans les applications Office** est défini sur **Activé**.

7. Sélectionnez **Enregistrer** dans ce panneau **Stratégie : Globale** et, si vous êtes invité à confirmer votre action, sélectionnez **OK**. Fermez ce panneau.

### <a name="create-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>Créer une étiquette pour la protection, de marquages visuels et d’une condition pour une demande de classification

Nous allons maintenant créer une sous-étiquette pour **Confidentiel**.

1. À partir de l’option de menu **Classifications** > **Étiquettes** : Cliquez avec le bouton droit sur l’étiquette **Confidentiel** et sélectionnez **Ajouter une sous-étiquette**.
    
    Si vous n’avez pas d’étiquette nommée **Confidentiel**, vous pouvez sélectionner une autre étiquette ou créer une étiquette, puis suivre le didacticiel avec des différences mineures.

2. Dans le panneau **Sous-étiquette**, spécifiez le nom d’étiquette **Finance** et ajoutez la description suivante : **Données confidentielles qui contiennent des informations financières réservées exclusivement aux employés**.
    
    Ce texte explique comment l’étiquette sélectionnée va être utilisée et s’affiche sous forme d’info-bulle pour aider les utilisateurs dans leur choix.

3. Pour **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Protéger**, puis **Protection** :
    
    ![Configuration d’une étiquette Azure Information Protection à des fins de protection](./media/info-protect-protection-bar-configured.png) 
    
4. Dans le panneau **Protection**, vérifiez que l’option **Azure (clé du cloud)** est sélectionnée. Cette option utilise le service Azure Rights Management pour protéger les documents et les e-mails. Vérifiez aussi que l’option **Définir les autorisations** est sélectionnée. Ensuite, sélectionnez **Ajouter des autorisations**.

5. Dans le panneau **Ajouter des autorisations**, sélectionnez **Ajouter \<nom de l’organisation> - Tous les membres**. Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous voyez et sélectionnez l’option suivante :
    
    ![Accorder des autorisations de protection à tous les membres pour une étiquette Azure Information Protection](./media/info-protect-protection-all-members.png) 
    
    Cette option sélectionne automatiquement tous les utilisateurs de votre organisation qui peuvent recevoir des autorisations. Toutefois, d’autres options vous permettent de parcourir et de rechercher des groupes ou utilisateurs dans votre locataire. Sinon, quand vous sélectionnez l’option **Entrer les détails**, vous pouvez spécifier des adresses e-mail individuelles ou tous les utilisateurs d’une autre organisation.

6. Pour les autorisations, sélectionnez **Réviseur** dans les options prédéfinies. Vous voyez comment ce niveau d’autorisation accorde automatiquement certaines autorisations répertoriées, mais pas toutes les autorisations :
    
    ![Accorder des autorisations de protection de coauteur pour une étiquette Azure Information Protection](./media/info-protect-protection-reviewer.png)
    
    Vous pouvez sélectionner différents niveaux d’autorisation ou spécifier des droits d’utilisation individuels à l’aide de l’option **Personnalisé**. Dans ce didacticiel, nous utilisons l’option **Réviseur**. Vous pourrez tester différentes autorisations par la suite et découvrir comment limiter les actions des utilisateurs spécifiés sur le document protégé ou l’e-mail.

7. Cliquez sur **OK** pour fermer le panneau **Ajouter des autorisations**. Le panneau **Protection** est mis à jour pour refléter votre configuration. Par exemple :
    
     ![Panneau Protection affichant la configuration des autorisations pour une étiquette Azure Information Protection](./media/info-protect-protection-configured.png)
    
    Si vous sélectionnez **Ajouter des autorisations**, le panneau **Ajouter des autorisations** s’ouvre à nouveau pour vous permettre d’ajouter des utilisateurs et de leur accorder des autorisations différentes. Par exemple, accordez uniquement un accès en consultation à un groupe spécifique. Dans ce didacticiel, nous utilisons un seul jeu d’autorisations pour tous les utilisateurs.

8. Passez en revue et conservez les valeurs par défaut pour l’expiration du contenu et l’accès hors connexion, puis cliquez sur **OK** pour enregistrer et fermer le panneau **Protection**.

8. Revenez au panneau **Sous-étiquette** et recherchez la section **Définir un marquage visuel** :
    
    Pour le paramètre **Les documents avec cette étiquette ont un pied de page**, cliquez sur **Activé**, puis, dans la zone **Texte**, tapez **Classé confidentiel**. 
    
    Pour le paramètre **Les documents avec cette étiquette ont un filigrane**, cliquez sur **Activé** puis, dans la zone **Texte**, tapez le nom de votre organisation. Par exemple, **VanArsdel, Ltd** 
    
    Bien que vous puissiez changer l’apparence des marquages visuels, nous utilisons pour le moment les valeurs par défaut de ces paramètres.
    
9. Recherchez la section **Configurer des conditions pour appliquer automatiquement cette étiquette** :
    
    Cliquez sur **Ajouter une nouvelle condition**, puis, dans le panneau **Condition**, sélectionnez les éléments suivants :
    
    a. **Choisir le type de condition**  : conservez la valeur par défaut **Types d’informations**.
    
    b. **Sélectionner un secteur d’activité** : conservez la valeur par défaut **Tout**.
    
    c. Dans la zone de recherche **Sélectionner les types d’informations** : tapez **Numéro de carte de crédit**. Ensuite, dans les résultats de recherche, sélectionnez **Numéro de carte de crédit**.
    
    d. **Nombre minimal d’occurrences** : conservez la valeur par défaut **1**.
    
    e. **Comptabiliser seulement les occurrences avec des valeurs uniques** : conservez la valeur par défaut **Désactivé**.
    
    ![Tutoriel Azure Information Protection - configurer la condition de la carte de crédit](./media/step2-configure-condition.png)
    
    Cliquez sur **Enregistrer** pour revenir au panneau **Sous-étiquette**.

10. Dans le panneau **Sous-étiquette**, vous voyez que **Numéro de carte de crédit** est affiché comme **NOM DE LA CONDITION**, avec **1** **OCCURRENCES** :
    
    ![Tutoriel Azure Information Protection - configurer la condition de la carte de crédit](./media/step2-see-condition.png)

11. **Sélectionner comment cette étiquette est appliquée** : conservez la valeur par défaut **Recommandé** et ne changez pas le conseil de stratégie par défaut. 

12. Dans la zone **Ajouter des notes pour l’administrateur** , tapez **À des fins de test uniquement**.

13. Cliquez sur **Enregistrer** dans ce panneau **Sous-étiquette**. Si vous êtes invité à confirmer, cliquez sur **OK**. La nouvelle étiquette est créée et enregistrée, mais elle n’est pas encore ajoutée à une stratégie.

14. À partir de l’option de menu **Classifications** > **Stratégies** : sélectionnez à nouveau **Globale**, puis sélectionnez le lien **Ajouter ou supprimer des étiquettes** situé en regard des étiquettes.

15. Dans le panneau **Stratégie : ajouter ou supprimer des étiquettes**, sélectionnez l’étiquette que vous venez de créer, la sous-étiquette nommée **Finance** et cliquez sur **OK**.

16. Dans le panneau **Stratégie : Globale**, votre nouvelle sous-étiquette s’affiche désormais dans votre stratégie globale, qui est configurée pour le marquage visuel et la protection. Par exemple :

    ![Tutoriel Azure Information Protection : nouvelle sous-étiquette](./media/info-protect-policy-configuredv2.png)
    
    Vous voyez aussi que les paramètres sont configurés pour l’étiquette par défaut et la justification :
    
    ![Tutoriel Azure Information Protection : paramètres configurés](./media/info-protect-settings-configuredv2.png)
    

17. Cliquez sur **Enregistrer** dans ce panneau **Stratégie : Globale**. Si vous êtes invité à confirmer cette action, cliquez sur **OK**.

Vous pouvez fermer le portail Azure, ou le laisser ouvert pour essayer des options de configuration supplémentaires après avoir terminé ce didacticiel.

Vous êtes prêt à tester les résultats de vos modifications.

## <a name="see-classification-labeling-and-protection-in-action"></a>Voir la classification, l’étiquetage et la protection en action 

Les modifications de stratégie que vous avez effectuées et la nouvelle étiquette que vous avez créée s’appliquent à Word, Excel, PowerPoint et Outlook. Mais pour ce tutoriel, nous allons utiliser Word pour les voir en action. 

Ouvrez un nouveau document dans Word. Comme Azure Information Protection est installé, les éléments suivants apparaissent :

![Tutoriel Azure Information Protection : client installé](./media/word2016-calloutsv2.png)

- Sous l’onglet **Accueil**, un groupe **Protection** avec un bouton nommé **Protéger**.
    
    Cliquez sur **Protéger** > **Aide et commentaires** puis, dans la boîte de dialogue **Microsoft Azure Information Protection**, vérifiez l’état de votre client. La mention **Connecté en tant que** et votre nom d’utilisateur s’affichent. En outre, vous devriez également voir une heure et une date récente pour la dernière connexion et le téléchargement de la stratégie Information Protection. Vérifiez que le nom d’utilisateur affiché correspond à celui de votre locataire.

- Une nouvelle barre sous le ruban, la barre Information Protection. Elle affiche le titre **Sensibilité** et les étiquettes que nous avons vues dans le portail Azure.

### <a name="to-manually-change-our-default-label"></a>Pour modifier manuellement notre étiquette par défaut

1. Sur la barre Information Protection, sélectionnez la dernière étiquette pour voir comment s’affichent les sous-étiquettes :
    
    ![Tutoriel Azure Information Protection : voir les sous-étiquettes](./media/info-protect-sub-labelsv2.png)

2. Sélectionnez une de ces sous-étiquettes. Les autres étiquettes n’apparaissent plus sur la barre maintenant que vous avez sélectionné une étiquette pour ce document. La valeur **Sensibilité** change pour montrer le nom de l’étiquette et de la sous-étiquette avec une modification correspondante de la couleur de l’étiquette. Par exemple :
    
    ![Tutoriel Azure Information Protection : sous-étiquette sélectionnée](./media/info-protect-sub-label-selectedv2.png)

3. Dans la barre Information Protection, cliquez sur l’icône **Modifier l’étiquette** en regard de la valeur de l’étiquette actuellement sélectionnée :
    
    ![Tutoriel Azure Information Protection : modifier l’icône d’une étiquette](./media/info-protect-edit-label-selectedv2.png)
    
    Cette action affiche à nouveau les étiquettes disponibles.

4. Sélectionnez maintenant la première étiquette, **Personnel**. Comme vous avez sélectionné une étiquette dont la classification est inférieure à la précédente pour ce document, vous devez justifier votre choix :
    
    ![Tutoriel Azure Information Protection : invite de confirmation de l’abaissement](./media/info-protect-lower-justification.png)
    
    Sélectionnez **L’étiquette précédente ne s’applique plus** et cliquez sur **Confirmer**. La valeur **Sensibilité** devient **Personnel** et les autres étiquettes sont masquées à nouveau.

### <a name="to-remove-the-classification-completely"></a>Pour supprimer complètement la classification

1. Dans la barre Information Protection, cliquez à nouveau sur l’icône **Modifier l’étiquette**. Toutefois, au lieu de choisir l’une des étiquettes, cliquez sur l’icône **Supprimer l’étiquette** :
    
    ![Tutoriel Azure Information Protection : icône de suppression](./media/delete-icon-from-personalv2.png)
    
2. Cette fois, à l’invite, entrez « Ce document n’a pas besoin d’être classé » et cliquez sur **Confirmer**.  
    
    La valeur **Sensibilité** indique **Non défini**, ce qui correspond à ce que voient les utilisateurs pour les nouveaux documents au départ si vous ne définissez pas d’étiquette par défaut comme paramètre de stratégie.

### <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Pour afficher une invite de recommandation pour l’étiquetage et la protection automatique

1. Dans le document Word, tapez un numéro de carte de crédit valide, par exemple **4242-4242-4242-4242**. 

2. Enregistrez le document localement avec un nom de fichier. 

3. Vous voyez maintenant une invite à appliquer l’étiquette que vous avez configurée pour la protection quand des numéros de carte de crédit sont détectés. Si nous n’avez pas accepté la recommandation, notre paramètre de stratégie nous permet de la rejeter en sélectionnant **Abandonner**. En donnant une recommandation mais en permettant à un utilisateur de l’ignorer, vous réduisez les faux positifs quand vous utilisez la classification automatique. Pour ce didacticiel, cliquez sur **Modifier maintenant**.

    ![Tutoriel Azure Information Protection : invite de recommandation](./media/change-nowv2.png)

    Outre le fait que le document montre maintenant que notre étiquette configurée est appliquée (par exemple **Confidentiel\Finance**), vous voyez immédiatement en filigrane le nom de votre entreprise à travers la page, et le pied de page **Classé confidentiel** est également appliqué. 

    Le document est aussi protégé par les autorisations que vous avez spécifiées pour cette étiquette. Vous pouvez vérifier que le document est protégé en cliquant sur l’onglet **Fichier** et en examinant les informations sous **Protéger le document**. Vous voyez que le document est protégé par **Confidentiel\Finance** et avez accès à la description de l’étiquette. 
    
    En raison de la configuration de protection de l’étiquette, seuls les employés peuvent ouvrir le document et certaines actions uniquement leur sont accessibles. Par exemple, parce qu’ils n’ont pas les autorisations pour imprimer, copier et extraire du contenu, ils ne peuvent pas imprimer le document ni copier son contenu. Ces restrictions permettent d’éviter la perte de données. En tant que propriétaire du document, vous pouvez l’imprimer et le copier. Toutefois, si vous l’envoyez par e-mail à un autre utilisateur de votre organisation, ce dernier ne pourra pas effectuer ces actions.

4. Vous pouvez maintenant fermer ce document.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Si vous ne souhaitez pas conserver les modifications que vous avez effectuées dans ce tutoriel, procédez ainsi :

1. Sélectionnez **Classifications** > **Stratégies** > **Global** pour ouvrir le panneau **Stratégie : Globale**.

2. Rétablissez les valeurs d’origine (dont vous avez pris note) des paramètres de stratégie, puis sélectionnez **Enregistrer**. 

3. Dans l’option de menu **Classifications** > **Étiquette** : dans le panneau **Azure Information Protection – Étiquette**, sélectionnez le menu contextuel (**…**) de l’étiquette **Finance** que vous avez créée.

4. Sélectionnez **Supprimer cette étiquette**, puis **OK** si une confirmation vous est demandée.

Redémarrez Word pour télécharger ces modifications.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la modification de la stratégie Azure Information Protection, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Pour plus d’informations sur l’emplacement où est consignée l’activité d’étiquetage, consultez [Journalisation de l’utilisation du client Azure Information Protection](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client).

