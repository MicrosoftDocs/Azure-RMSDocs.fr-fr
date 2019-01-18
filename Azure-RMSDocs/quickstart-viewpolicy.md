---
title: 'Démarrage rapide : Bien démarrer avec Azure Information Protection sur le Portail Azure – AIP'
description: Si Azure Information Protection est nouveau pour votre organisation, commencez par ajouter le service au Portail Azure, vérifier que le service de protection est activé et afficher la stratégie.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/15/2018
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: 91a9a124c53d7c8f1aab31213595a8fc2f3627dd
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54393981"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>Démarrage rapide : Bien démarrer avec Azure Information Protection dans le portail Azure

Dans ce démarrage rapide, vous allez ajouter Azure Information Protection au Portail Azure, vérifier que le service de protection est activé et afficher la stratégie par défaut de votre organisation. 

Ce démarrage rapide prend 5 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

- Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

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

Même si le service de protection est maintenant automatiquement activé pour les nouveaux locataires, il est préférable de vérifier qu’aucune activation manuelle n’est nécessaire. 

1. Dans le panneau **Azure Information Protection**, sélectionnez **Gérer** > **Activation de la protection**.

2. Vérifiez que la protection est activée pour votre locataire : 
    
    - Si la protection est activée, la confirmation suivante s’affiche :
        
        ![État d’Azure Information Protection pour Azure RMS](./media/info-protect-azurerms-activated.png)
        
    - Si la protection n’est pas activée, les informations d’état vous l’indiquent, et l’option d’activation est affichée :
        
        ![État d’Azure Information Protection pour Azure RMS](./media/info-protect-azurerms-deactivated.png)

3. Si la protection n’est pas activée, sélectionnez **Activer**. 

    Quand l’activation est terminée, la barre d’informations affiche **Activation terminée**.

## <a name="view-your-organizations-default-policy---labels-and-policy-settings"></a>Afficher la stratégie par défaut de l’organisation – étiquettes et paramètres de stratégie

La première fois que vous vous connectez au service Azure Information Protection sur le Portail Azure, une stratégie par défaut est créée pour votre locataire. La stratégie par défaut contient des étiquettes et des paramètres que vous pouvez utiliser tels quels ou personnaliser.

1. Sélectionnez **Classifications** > **Stratégies** > **Global** pour afficher la stratégie Azure Information Protection par défaut qui est créée pour votre locataire.
    
2. Prenez quelques minutes pour vous familiariser avec les étiquettes affichées :
    
   - Étiquettes de classification : **Personnel**, **Public**, **Général**, **Confidentiel** et **Hautement confidentiel**. Les deux dernières étiquettes se développent pour afficher des sous-étiquettes, qui sont des exemples de sous-catégories dans une classification :
    
   - Avec la configuration par défaut, des marquages visuels ne sont pas configurés pour certaines étiquettes. Les marquages visuels sont un pied de page, un en-tête et un filigrane. En fonction de votre stratégie par défaut, la protection peut ou non être définie pour certaines étiquettes. Par exemple : 
    
     ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](./media/info-protect-policy-default-labelsv2.png)
    
3. Après les étiquettes, dans la section **Configurer les paramètres à afficher et à appliquer aux utilisateurs finaux d’Information Protection**, vous voyez également certains paramètres de stratégie. Par exemple, aucune étiquette par défaut n’est définie, les documents ou e-mails ne doivent pas obligatoirement avoir une étiquette et les utilisateurs n’ont pas à fournir de justification quand ils changent les étiquettes :
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : stratégie par défaut](./media/info-protect-policy-default-settings-quickstart.png) 

4. Dans la mesure où vous ne voyez que les étiquettes et les paramètres, vous pouvez fermer tous les panneaux que vous avez ouverts.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez vu les étiquettes et les paramètres de stratégie sur le portail Azure, le tutoriel suivant pourra vous être utile : [Modifier la stratégie et créer une étiquette pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

Pour obtenir des instructions détaillées sur la configuration de tous les aspects de la stratégie Azure Information Protection, voir [Configurer la stratégie Azure Information Protection](configure-policy.md).
