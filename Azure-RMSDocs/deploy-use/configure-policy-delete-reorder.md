---
title: "Comment supprimer ou réorganiser une étiquette | Azure Information Protection"
description: "Vous pouvez supprimer ou réorganiser les étiquettes que les utilisateurs voient dans la barre Information Protection en configurant la stratégie Azure Information Protection en conséquence."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: 4fcfcebc7da5a22a91911d70d4d787dc525d3485
ms.openlocfilehash: 743741fc63adfd959074986aab5c697d817f69c7


---

# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Comment supprimer ou réorganiser une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Vous pouvez supprimer ou réorganiser les étiquettes que les utilisateurs voient dans la barre Information Protection en configurant la stratégie Azure Information Protection en conséquence.

![Suppression ou réorganisation d’étiquettes dans la stratégie Azure Information Protection](../media/info-protect-contextmenu.png)

Au lieu de supprimer une étiquette, vous pouvez simplement la désactiver si vous souhaitez conserver sa configuration mais l’empêcher de s’afficher dans la barre Information Protection.

Triez les étiquettes de manière à ce que les utilisateurs les voient dans un ordre de progression logique dans la barre Information Protection. Par exemple, triez les étiquettes dans leur ordre croissant de confidentialité afin que les utilisateurs voient l’étiquette la moins sensible en premier et l’étiquette la plus sensible en dernier. La [stratégie par défaut](configure-policy-default.md) utilise cette configuration.

> [!IMPORTANT]
>Si vous configurez des [conditions](configure-policy-classification.md) qui peuvent s’appliquer à plusieurs étiquettes, vous devez trier les étiquettes de la moins sensible à la plus sensible. Ce tri permet de s’assurer que l’étiquette la plus sensible est appliquée lorsque les conditions sont évaluées.


Suivez la procédure indiquée ci-dessous pour effectuer ces modifications.

1. Si ce n’est déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général, puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette à supprimer, désactiver ou réorganiser s’applique à tous les utilisateurs, procédez de l’une des manières suivantes depuis le panneau **Stratégie : Globale**. 

    - Pour supprimer une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez supprimer, cliquez sur **Supprimer cette étiquette**, puis cliquez sur **Oui** pour confirmer. Cliquez ensuite sur **Enregistrer**. 

    - Pour désactiver une étiquette : sélectionnez l’étiquette que vous souhaitez désactiver. Dans le Panneau **Étiquette**, pour l’option **Activé**, cliquez sur **Désactivé**, puis sur **Enregistrer**.

    - Pour réorganiser une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez réorganiser, cliquez sur **Déplacer vers le haut** ou **Déplacer vers le bas** jusqu'à ce que l’étiquette soit à l’endroit souhaité. Cliquez ensuite sur **Enregistrer**. 

     Si l’étiquette à supprimer, désactiver ou réorganiser se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour qu’elle s’applique uniquement aux utilisateurs sélectionnés, commencez par sélectionner cette stratégie à partir du panneau **Azure Information Protection** initial.

3. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  





<!--HONumber=Dec16_HO1-->


