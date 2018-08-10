---
title: Ajouter une étiquette à une stratégie Azure Information Protection ou la supprimer de celle-ci
description: Ajouter ou supprimer une étiquette Azure Information Protection à la stratégie globale pour tous les utilisateurs, ou à une stratégie délimitée pour une partie des utilisateurs, ou l’en supprimer.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.openlocfilehash: bca42c43f8e25ae4a9bb4b1818244834551f9ba1
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39491052"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Ajouter une étiquette à une stratégie Azure Information Protection ou la supprimer de celle-ci

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Après avoir créé une étiquette Azure Information Protection, vous pouvez l’ajouter à une stratégie afin qu’elle soit disponible pour les utilisateurs. Si l’étiquette est destinée à tous les utilisateurs, ajoutez-la à la stratégie globale. Si l’étiquette est destinée à une partie des utilisateurs, ajoutez-la à une stratégie délimitée. Vous ne pouvez ajouter une étiquette qu’à une seule stratégie. Pour ajouter une sous-étiquette, son étiquette parente doit être dans la même stratégie, ou dans la stratégie globale.

En ce qui concerne les étiquettes qui se trouvent déjà dans une stratégie, vous pouvez les supprimer de celle-ci. Cette action ne supprime pas l’étiquette. Elle demeure utilisable dans une autre stratégie.

Si vous n’avez pas encore créé l’étiquette, consultez [Comment créer une étiquette pour Azure Information Protection](configure-policy-new-label.md).

Pour créer une stratégie délimitée afin que l’étiquette s’applique à une partie des utilisateurs, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Pour ajouter une étiquette à une stratégie ou la supprimer de celle-ci

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **CLASSIFICATIONS** > **Stratégies** : dans le panneau **Azure Information Protection** - **Stratégies**, sélectionnez **Globale** si l’étiquette à ajouter ou supprimer s’applique à tous les utilisateurs.

    Si l’étiquette à ajouter ou supprimer s’applique à une partie des utilisateurs, sélectionnez votre stratégie délimitée à la place.

3. Dans le panneau **Stratégie**, sélectionnez **Ajouter ou supprimer des étiquettes**.

4. Dans le panneau **Stratégie : ajouter ou supprimer des étiquettes**, toutes les étiquettes se trouvant déjà dans une stratégie sont accompagnées d’une case cochée et du nom de la stratégie correspondante dans la colonne **STRATÉGIE**.
     
    Les sous-étiquettes sont mises en retrait. Dans une stratégie délimitée, les étiquettes qui sont héritées de la stratégie globale s’affichent comme étant non disponibles.
    
    Effectuez une ou plusieurs des actions ci-dessous, puis cliquez sur **OK** :
    
    - Pour ajouter une étiquette, sélectionnez-la ; cette opération ajoute une case cochée.
    
    - Pour supprimer une étiquette, décochez la case correspondante.
  
5. Pour enregistrer vos modifications, cliquez sur **Enregistrer**.
   
    Vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

