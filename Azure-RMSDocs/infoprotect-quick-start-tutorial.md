---
title: 'Tutoriel : modifier la stratégie Azure Information Protection – AIP'
description: Tutoriel de prise en main d’environ 15 minutes, permettant de modifier la stratégie Azure Information Protection dans votre organisation.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 37638bfbc47a4a4d075114540ec65ea5d6372a30
ms.sourcegitcommit: 13dac930fabafeb05d71d7ae8acf5c0a78c12397
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96849825"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-and-create-a-new-label"></a>Tutoriel : Configurer les paramètres de la stratégie Azure Information Protection et créer une étiquette

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>
> **Pour déployer le client classique AIP,** ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.

> [!TIP]
> Si vous utilisez un autre client d’étiquetage que le client classique, consultez la [documentation sur la conformité Microsoft 365](/microsoft-365/compliance/sensitivity-labels) pour des instructions équivalentes à ce tutoriel.
> 

Dans ce tutoriel, vous apprenez à effectuer les opérations suivantes :
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
    
    Si vous n’avez pas d’abonnement incluant Azure Information Protection Plan 2, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. Le volet Azure Information Protection est ajouté au portail Azure, le service de protection est activé et vous avez une ou plusieurs étiquettes publiées dans la stratégie générale Azure Information Protection.
    
    Ces étapes sont décrites dans [Démarrage rapide : Ajouter Azure Information Protection au portail Azure et afficher la stratégie](quickstart-viewpolicy.md).

3. Le client Azure Information Protection (classique) installé sur votre ordinateur Windows (Windows 7 minimum avec Service Pack 1). 

4. Vous êtes connecté aux applications Office à partir de l’une des catégories suivantes :
    
    - Applications Office, pour les versions listées dans le [tableau des versions prises en charge pour Microsoft 365 Apps par le canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), depuis Microsoft 365 Apps for Business ou Microsoft 365 Business Premium, lorsqu’une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur
    
    - Microsoft 365 Apps for enterprise
    
    - Office Professionnel Plus 2019.
    
    - Office Professionnel Plus 2016.
    
    - Office Professionnel Plus 2013 avec Service Pack 1.
    
    - Office Professionnel Plus 2010 avec Service Pack 2.

> [!TIP]
> Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).
> 
C’est parti ! Poursuivez avec [Modifier la stratégie Azure Information Protection](#edit-the-azure-information-protection-policy).

## <a name="edit-the-azure-information-protection-policy"></a>Modifier la stratégie Azure Information Protection

À l’aide du portail Azure, nous allons tout d’abord modifier quelques paramètres de stratégie puis créer une nouvelle étiquette.

### <a name="edit-the-policy-settings"></a>Modifier les paramètres de stratégie

1. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général. Accédez ensuite à **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.
    
    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Sélectionnez **Classifications** > **Stratégies** > **Global** pour ouvrir le panneau **Stratégie : Globale**. 

3. Localisez les paramètres de stratégie après les étiquettes, dans la section **Configurer les paramètres à présenter et à appliquer aux utilisateurs finaux d’Information Protection**. 
    
    Notez la façon dont les paramètres sont actuellement configurés. Il s’agit spécifiquement des paramètres **Sélectionner l’étiquette par défaut** et **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**. Par exemple :
    
    ![Tutoriel Azure Information Protection : paramètres de stratégie à modifier](./media/info-protect-policy-default-settings.png)
    
    Nous utiliserons ces paramètres de stratégie plus loin dans ce tutoriel lorsque vous les verrez en action.

4. Pour **Sélectionner l’étiquette par défaut**, sélectionnez l’une des étiquettes, par exemple **Général**. 
    
    L’étiquette **General** est l’une des étiquettes par défaut qu’Azure Information Protection peut créer pour vous. Cette étape est traitée dans la section [Créer et publier des étiquettes](quickstart-viewpolicy.md#create-and-publish-labels) du Guide de démarrage rapide pour ajouter Azure Information Protection au portail Azure.

5. Pour **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection**, définissez cette option sur **Activé**, le cas échéant.

6. Par ailleurs, assurez-vous que le paramètre **Afficher la barre Information Protection dans les applications Office** est défini sur **Activé**.

7. Sélectionnez **Enregistrer** dans ce panneau **Stratégie : Globale** et, si vous êtes invité à confirmer votre action, sélectionnez **OK**. Fermez ce volet.

### <a name="create-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>Créer une étiquette pour la protection, de marquages visuels et d’une condition pour une demande de classification

Nous allons maintenant créer une sous-étiquette pour **Confidentiel**.

1. À partir de l’option de menu **Classifications** > **Étiquettes** : Cliquez avec le bouton droit sur l’étiquette **Confidentiel** et sélectionnez **Ajouter une sous-étiquette**.
    
    Si vous n’avez pas d’étiquette nommée **Confidentiel**, vous pouvez sélectionner une autre étiquette ou créer une étiquette, puis suivre le didacticiel avec des différences mineures.

2. Dans le volet **Sous-étiquette**, spécifiez le nom d’étiquette **Finance** et ajoutez la description suivante : **Données confidentielles qui contiennent des informations financières réservées exclusivement aux employés**.
    
    Ce texte explique comment l’étiquette sélectionnée va être utilisée et s’affiche sous forme d’info-bulle pour aider les utilisateurs dans leur choix.

3. Pour **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Protéger**, ce qui ouvre automatiquement le volet **Protection** avec l’option **Protection** sélectionnée :
    
    ![Configuration d’une étiquette Azure Information Protection à des fins de protection](./media/info-protect-protection-bar-configured.png) 
    
4. Dans le volet **Protection**, vérifiez que l’option **Azure (clé cloud)** est sélectionnée. Cette option utilise le service Azure Rights Management pour protéger les documents et les e-mails. Vérifiez aussi que l’option **Définir les autorisations** est sélectionnée. Ensuite, sélectionnez **Ajouter des autorisations**.

5. Dans le volet **Ajouter des autorisations**, sélectionnez **Ajouter\<organization name> - Tous les membres**. Par exemple, si le nom de votre organisation est VanArsdel, Ltd, vous voyez et sélectionnez l’option suivante :
    
    ![Accorder des autorisations de protection à tous les membres pour une étiquette Azure Information Protection](./media/info-protect-protection-all-members.png) 
    
    Cette option sélectionne automatiquement tous les utilisateurs de votre organisation qui peuvent recevoir des autorisations. Toutefois, d’autres options vous permettent de parcourir et de rechercher des groupes ou utilisateurs dans votre locataire. Sinon, quand vous sélectionnez l’option **Entrer les détails**, vous pouvez spécifier des adresses e-mail individuelles ou tous les utilisateurs d’une autre organisation.

6. Pour les autorisations, sélectionnez **Réviseur** dans les options prédéfinies. Vous voyez comment ce niveau d’autorisation accorde automatiquement certaines autorisations répertoriées, mais pas toutes les autorisations :
    
    ![Accorder des autorisations de protection de coauteur pour une étiquette Azure Information Protection](./media/info-protect-protection-reviewer.png)
    
    Vous pouvez sélectionner différents niveaux d’autorisation ou spécifier des droits d’utilisation individuels à l’aide de l’option **Personnalisé**. Dans ce didacticiel, nous utilisons l’option **Réviseur**. Vous pourrez tester différentes autorisations par la suite et découvrir comment limiter les actions des utilisateurs spécifiés sur le document protégé ou l’e-mail.

7. Cliquez sur **OK** pour fermer le volet **Ajouter des autorisations**. Le volet **Protection** est mis à jour pour refléter votre configuration. Par exemple :
    
     ![Volet Protection affichant la configuration des autorisations pour une étiquette Azure Information Protection](./media/info-protect-protection-configured.png)
    
    Si vous sélectionnez **Ajouter des autorisations**, le volet **Ajouter des autorisations** s’ouvre à nouveau pour vous permettre d’ajouter des utilisateurs et de leur accorder des autorisations différentes. Par exemple, accordez uniquement un accès en consultation à un groupe spécifique. Dans ce didacticiel, nous utilisons un seul jeu d’autorisations pour tous les utilisateurs.

8. Passez en revue et conservez les valeurs par défaut pour l’expiration du contenu et l’accès hors connexion, puis cliquez sur **OK** pour enregistrer et fermer le volet **Protection**.

8. Revenez au volet **Sous-étiquette** et recherchez la section **Définir un marquage visuel** :
    
    Pour le paramètre **Les documents avec cette étiquette ont un pied de page**, cliquez sur **Activé**, puis, dans la zone **Texte**, tapez **Classé confidentiel**. 
    
    Pour le paramètre **Les documents avec cette étiquette ont un filigrane**, cliquez sur **Activé** puis, dans la zone **Texte**, tapez le nom de votre organisation. Par exemple, **VanArsdel, Ltd** 
    
    Bien que vous puissiez changer l’apparence des marquages visuels, nous utilisons pour le moment les valeurs par défaut de ces paramètres.
    
9. Recherchez la section **Configurer des conditions pour appliquer automatiquement cette étiquette** :
    
    Cliquez sur **Ajouter une nouvelle condition**, puis, dans le volet **Condition**, sélectionnez les éléments suivants :
    
    a. **Choisir le type de condition**  : conservez la valeur par défaut **Types d’informations**.
    
    b. **Sélectionner un secteur d’activité** : conservez la valeur par défaut **Tout**.
    
    c. Dans la zone de recherche **Sélectionner les types d’informations** : tapez **Numéro de carte de crédit**. Ensuite, dans les résultats de recherche, sélectionnez **Numéro de carte de crédit**.
    
    d. **Nombre minimal d’occurrences** : conservez la valeur par défaut **1**.
    
    e. **Comptabiliser seulement les occurrences avec des valeurs uniques** : conservez la valeur par défaut **Désactivé**.
    
    ![Tutoriel Azure Information Protection - configurer la condition de la carte de crédit](./media/step2-configure-condition.png)
    
    Cliquez sur **Enregistrer** pour revenir au volet **Sous-étiquette**.

10. Dans le volet **Sous-étiquette**, vous voyez que **Numéro de carte de crédit** est affiché comme **NOM DE LA CONDITION**, avec **1** **OCCURRENCES** :
    
    ![Tutoriel Azure Information Protection : résumé de la condition de la carte de crédit](./media/step2-see-condition.png)

11. **Sélectionner comment cette étiquette est appliquée** : conservez la valeur par défaut **Recommandé** et ne changez pas le conseil de stratégie par défaut. 

12. Dans la zone **Ajouter des notes pour l’administrateur** , tapez **À des fins de test uniquement**.

13. Cliquez sur **Enregistrer** dans ce volet **Sous-étiquette**. Si vous êtes invité à confirmer, cliquez sur **OK**. La nouvelle étiquette est créée et enregistrée, mais elle n’est pas encore ajoutée à une stratégie.

14. À partir de l’option de menu **Classifications** > **Stratégies** : sélectionnez à nouveau **Globale**, puis sélectionnez le lien **Ajouter ou supprimer des étiquettes** situé en regard des étiquettes.

15. Dans le panneau **Stratégie : ajouter ou supprimer des étiquettes**, sélectionnez l’étiquette que vous venez de créer, la sous-étiquette nommée **Finance** et cliquez sur **OK**.

16. Dans le panneau **Stratégie : Globale**, votre nouvelle sous-étiquette s’affiche à présent dans votre stratégie globale, qui est configurée pour le marquage visuel et la protection. Par exemple :

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

3. Dans l’option de menu **Classifications** > **Étiquette** : dans le volet **Azure Information Protection – Étiquette**, sélectionnez le menu contextuel ( **…** ) de l’étiquette **Finance** que vous avez créée.

4. Sélectionnez **Supprimer cette étiquette**, puis **OK** si une confirmation vous est demandée.

Redémarrez Word pour télécharger ces modifications.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la modification de la stratégie Azure Information Protection, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Pour plus d’informations sur l’emplacement où est consignée l’activité d’étiquetage, consultez [Journalisation de l’utilisation du client Azure Information Protection](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client).

