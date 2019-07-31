---
title: 'Démarrage rapide : afficher Azure Information Protection sur le portail Azure - AIP'
description: Si Azure Information Protection est nouveau pour votre organisation, commencez par ajouter le service au Portail Azure, vérifier que le service de protection est activé et afficher les paramètres de stratégie et les étiquettes.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/20/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 5dc98a019ca34e6a303308e4e93d076042893638
ms.sourcegitcommit: 47182b6a65bfae3561cb34be3d6a6852a1edccb9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68446873"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>Démarrage rapide : Bien démarrer avec Azure Information Protection dans le portail Azure

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Dans ce démarrage rapide, vous allez ajouter Azure Information Protection au portail Azure, vérifier que le service de protection est activé, créer des étiquettes par défaut si vous n’avez pas d’étiquettes et afficher les paramètres de stratégie pour Azure Information Protection.

Ce démarrage rapide prend moins de 10 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

- Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Ajouter Azure Information Protection au Portail Azure

Azure Information Protection n’est pas automatiquement disponible sur le Portail Azure. Vous devez l’ajouter.

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec le compte Administrateur général de votre locataire. 
    
    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Dans le menu hub, sélectionnez **Créer une ressource**, puis, à partir de la zone de recherche pour la Place de marché, tapez **Azure Information Protection**. 
    
3. Dans la liste des résultats, sélectionnez **Azure Information Protection**. Ensuite, dans le panneau **Azure Information Protection**, cliquez sur **Créer**.
    
    > [!TIP] 
    > Ou sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.
    
    Cliquez sur **Créer** à nouveau.

## <a name="confirm-the-protection-service-is-activated"></a>Vérifier que le service de protection est activé

Même si le service de protection est maintenant automatiquement activé pour les nouveaux clients, il est préférable de vérifier qu’aucune activation manuelle n’est nécessaire. 

1. Dans le panneau **Azure Information Protection**, sélectionnez **Gérer** > **Activation de la protection**.

2. Vérifiez que la protection est activée pour votre locataire : 
    
    - Si la protection est activée, la confirmation suivante s’affiche :
        
        ![État d’Azure Information Protection pour Azure RMS : activé](./media/info-protect-azurerms-activated.png)
        
    - Si la protection n’est pas activée, les informations d’état vous l’indiquent, et l’option d’activation est affichée :
        
        ![État d’Azure Information Protection pour Azure RMS : non activé](./media/info-protect-azurerms-deactivated.png)

3. Si la protection n’est pas activée, sélectionnez **Activer**. 

    Quand l’activation est terminée, la barre d’informations affiche **Activation terminée**.

## <a name="create-labels---if-necessary"></a>Créer des étiquettes - si nécessaire

Votre entreprise peut déjà disposer d’étiquettes, car elles ont été créées automatiquement pour votre locataire, ou parce que vous avez des étiquettes de sensibilité dans le Centre de sécurité et de conformité Office 365, le centre de sécurité Microsoft ou le centre de conformité Microsoft. Voyons voir :

1. Sélectionnez **Classifications** > **Étiquettes** :
    
    Si vous voyez l’option **Générer des étiquettes par défaut**, vous n’avez pas encore d’étiquettes :
    
     ![Azure Information Protection, aucune étiquette par défaut](./media/info-protect-nodefaultlabels.png)
    
    Si vous ne voyez pas cette option pour générer des étiquettes par défaut, vous disposez déjà d’étiquettes, probablement similaires à celles de l’image suivante, qui sont les étiquettes par défaut pour Azure Information Protection :
    
    ![Azure Information Protection, étiquettes par défaut](./media/info-protect-defaultlabels.png)

2. Si vous avez des étiquettes, accédez à la section suivante pour afficher vos étiquettes. Si vous n’avez pas encore d’étiquettes, sélectionnez l’option **Générer des étiquettes par défaut**.

4. Ensuite, pour publier les étiquettes pour tous les utilisateurs, à partir de **Classifications** > **Stratégies** > **Général** :
    
    a. Sélectionnez **Ajouter ou supprimer des étiquettes**.
    
    b. Dans le panneau **Stratégie : Ajouter ou supprimer des étiquettes**, sélectionnez toutes les étiquettes, puis sélectionnez **OK**.
    
    c. De retour dans le panneau **Stratégie : Général**, sélectionnez **Enregistrer**.

## <a name="view-your-labels"></a>Afficher vos étiquettes

Sélectionnez **Classifications** > **Étiquettes** et consacrez quelques minutes à vous familiariser avec les étiquettes qui sont affichées sur le panneau **Azure Information Protection - Étiquettes** .

Si elles ne ressemblent aux étiquettes dans l’image de la section précédente, vous n’utilisez pas les étiquettes par défaut d’Azure Information Protection, mais des étiquettes qui ont été créées à partir du Centre de sécurité et de conformité Office 365, du centre de sécurité Microsoft 365 ou du centre de conformité Microsoft 365.

> [!TIP]
> Si vous ne souhaitez pas utiliser vos étiquettes personnalisées, mais les étiquettes par défaut d’Azure Information Protection : 
> - Supprimez les étiquettes personnalisées et l’option pour générer des étiquettes par défaut s’affiche dans le panneau **Étiquettes**, comme décrit dans la [section précédente](#create-labels---if-necessary). 

À partir du panneau **Azure Information Protection - Étiquettes** :

- Les étiquettes de classification par défaut sont **Personnel**, **Public**, **Interne**, **Confidentiel** et **Hautement confidentiel**. Les deux dernières étiquettes se développent pour afficher des sous-étiquettes, qui sont des exemples de sous-catégories dans une classification.

- À partir des colonnes **MARKING** et **PROTECTION**, vous pouvez voir que certaines étiquettes contiennent des marquages visuels configurés. Les marquages visuels sont un pied de page, un en-tête et un filigrane. Certaines étiquettes également avoir une protection définie. 

Par exemple : 

![Présentation par guide de démarrage rapide Azure Information Protection des étiquettes par défaut](./media/info-protect-policy-default-labelsv2.png)

Si vous sélectionnez une étiquette, vous voyez des détails pour cette configuration d’étiquette sur un nouveau panneau.

## <a name="view-your-policy-settings"></a>Afficher vos paramètres de stratégie

La première fois que vous vous connectez au service Azure Information Protection à l’aide du portail Azure, les paramètres de stratégie par défaut qui sont utilisés par le client Azure Information Protection sont toujours créés pour vous. Pour ce client, les paramètres de stratégie et les étiquettes que nous avons consultés sont téléchargés sur le client dans la stratégie Azure Information Protection.

Si vous utilisez le client d’étiquetage unifié Azure Information Protection, ce client n’utilise pas ces paramètres de stratégie. Au lieu de cela, ce client télécharge les étiquettes et les paramètres de stratégie à partir du Centre de sécurité et de conformité Office 365, du centre de conformité Microsoft 365 ou du centre de sécurité Microsoft 365.

Pour afficher les paramètres de la stratégie Azure Information Protection par défaut :

1. Sélectionnez **Classifications** > **Stratégies** > **Général** pour afficher les paramètres de la stratégie Azure Information Protection par défaut qui est créée pour votre locataire.
    
2. Après les étiquettes, dans la section **Configurer les paramètres à présenter et à appliquer aux utilisateurs finaux d’Information Protection**, les paramètres de la stratégie s’affichent. Par exemple, aucune étiquette par défaut n’est définie, les documents ou e-mails ne doivent pas obligatoirement avoir une étiquette et les utilisateurs n’ont pas à fournir de justification quand ils changent les étiquettes :
    
    ![Paramètres globaux de la stratégie Azure Information Protection](./media/defaultsettings-aip.png)

3. Dans la mesure où vous ne voyez que les paramètres, vous pouvez fermer tous les panneaux du portail que vous avez ouverts.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez vu les étiquettes par défaut et les paramètres de stratégie sur le portail Azure, le tutoriel suivant pourra vous être utile : [Modifier la stratégie et créer une étiquette pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

Pour obtenir des instructions détaillées sur la configuration de tous les aspects de la stratégie Azure Information Protection, voir [Configurer la stratégie Azure Information Protection](configure-policy.md).
