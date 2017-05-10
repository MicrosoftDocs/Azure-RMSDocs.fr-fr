---
title: "Nouvelle étiquette Azure Information Protection"
description: "Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes que les utilisateurs voient dans la barre Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 91feb6dfd9421d7c5cccf53b45f8a0f35e74007d
ms.sourcegitcommit: e3974cc1490581414084669632cad54b12b05d5a
ms.translationtype: HT
ms.contentlocale: fr-FR
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Comment créer une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes que les utilisateurs voient dans la barre Information Protection.

Vous pouvez ajouter une étiquette ou ajouter une sous-étiquette à une étiquette existante lorsque vous avez besoin d’un niveau supplémentaire de classification. Par exemple, la dernière de la [stratégie par défaut](configure-policy-default.md) contient des sous-étiquettes.

Utilisez les instructions suivantes pour ajouter une étiquette à la stratégie Azure Information Protection.

1. Si vous ne l’avez pas déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général, puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si la nouvelle étiquette à ajouter s’applique à tous les utilisateurs, procédez de l’une des manières suivantes à partir du panneau **Stratégie : Globale**. 

    - Pour créer une étiquette, cliquez sur **Ajouter une nouvelle étiquette**.

    - Pour créer une sous-étiquette, cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette à laquelle vous souhaitez créer une sous-étiquette, puis cliquez sur **Ajouter une sous-étiquette**.
    
     Si la nouvelle étiquette à ajouter se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour qu’elle s’applique uniquement aux utilisateurs sélectionnés, commencez par sélectionner cette stratégie à partir du panneau **Azure Information Protection** initial.

3. Dans le panneau **Étiquette** ou **Sous-étiquette**, sélectionnez les options que vous souhaitez pour cette nouvelle étiquette, puis cliquez sur **Enregistrer**.
    
    Notez que la couleur noire est automatiquement affectée aux nouvelles étiquettes. Choisissez une couleur distinctive dans la liste des couleurs ou entrez un code (triplet hexadécimal) représentant les composants RVB (rouge, vert, bleu) de la couleur. Par exemple, **#DAA520**. Si vous souhaitez obtenir des informations de référence sur ces codes, la page [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85).aspx) dans la documentation MSDN constitue un bon point de départ. Ces codes sont utilisés dans de nombreux programmes de retouche d’images, par exemple Microsoft Paint. Quand vous choisissez une couleur personnalisée à partir d’une palette, les valeurs RVB s’affichent automatiquement.

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

