---
title: Ajouter une étiquette à une stratégie Azure Information Protection ou l’en supprimer – AIP
description: Ajouter ou supprimer une étiquette Azure Information Protection à la stratégie globale pour tous les utilisateurs, ou à une stratégie délimitée pour une partie des utilisateurs, ou l’en supprimer.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 2100304e6277e1cb3aefd46257df4aaca64156dc
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935093"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Ajouter une étiquette à une stratégie Azure Information Protection ou la supprimer de celle-ci

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Azure information protection client pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Après avoir créé une étiquette Azure Information Protection, vous pouvez l’ajouter à une stratégie afin qu’elle soit disponible pour les utilisateurs. Si l’étiquette est destinée à tous les utilisateurs, ajoutez-la à la stratégie globale. Si l’étiquette est destinée à une partie des utilisateurs, ajoutez-la à une stratégie délimitée. Vous ne pouvez ajouter une étiquette qu’à une seule stratégie. 

Pour ajouter une sous-étiquette, son étiquette parente doit être dans la même stratégie, ou dans la stratégie globale. Quand vous ajoutez une sous-étiquette, les paramètres de l’étiquette principale ne sont pas hérités. Pour les utilisateurs auxquels la sous-étiquette est affectée dans leur stratégie, l’étiquette principale est uniquement prise en charge comme conteneur d’affichage pour le nom et la couleur. Dans ce scénario, les autres paramètres de configuration dans l’étiquette principale ne sont pas pris en charge pour les marquages visuels, la protection et les conditions. Bien que vous puissiez toujours les configurer, ces paramètres dans l’étiquette principale ne sont pris en charge que pour les utilisateurs qui ont l’étiquette principale dans leur stratégie sans la sous-étiquette.

En ce qui concerne les étiquettes qui se trouvent déjà dans une stratégie, vous pouvez les supprimer de celle-ci. Cette action ne supprime pas l’étiquette. Elle demeure utilisable dans une autre stratégie.

Si vous n’avez pas encore créé l’étiquette, consultez [Comment créer une étiquette pour Azure Information Protection](configure-policy-new-label.md).

Pour créer une stratégie délimitée afin que l’étiquette s’applique à une partie des utilisateurs, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Pour ajouter une étiquette à une stratégie ou la supprimer de celle-ci

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**.
    
    Par exemple, dans la zone de recherche pour ressources, services et docs : commencez à taper les **informations** et sélectionnez **Azure information protection**.

2. À partir de l’option de menu **classifications** > **stratégies** : dans le volet **Azure information protection** - **stratégies** , sélectionnez **Global** si l’étiquette à ajouter ou supprimer s’applique à tous les utilisateurs.

    Si l’étiquette à ajouter ou supprimer s’applique à une partie des utilisateurs, sélectionnez votre stratégie délimitée à la place.

3. Dans le volet **stratégie** , sélectionnez **Ajouter ou supprimer des étiquettes**.

4. Dans le volet **stratégie : ajouter ou supprimer des étiquettes** , vous voyez toutes vos étiquettes avec une case à cocher activée si elles se trouvent déjà dans une stratégie, et le nom de stratégie correspondant dans la colonne **stratégie** .
     
    Les sous-étiquettes sont mises en retrait. Dans une stratégie délimitée, les étiquettes qui sont héritées de la stratégie globale s’affichent comme étant non disponibles.
    
    Effectuez une ou plusieurs des actions ci-dessous, puis cliquez sur **OK** :
    
    - Pour ajouter une étiquette, sélectionnez-la ; cette opération ajoute une case cochée.
    
    - Pour supprimer une étiquette, décochez la case correspondante.
  
5. Pour enregistrer vos modifications, cliquez sur **Enregistrer**.
   
    Vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).
