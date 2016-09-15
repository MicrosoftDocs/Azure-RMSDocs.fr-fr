---
title: "Comment supprimer ou réorganiser une étiquette pour Azure Information Protection | Azure Information Protection"
description: "Vous pouvez supprimer ou réorganiser les étiquettes que les utilisateurs voient dans la barre Information Protection en configurant la stratégie Azure Information Protection en conséquence."
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: 14863f7fcd4df2e8baaddc7837649fa3efe59019


---

# Comment supprimer ou réorganiser une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Vous pouvez supprimer ou réorganiser les étiquettes que les utilisateurs voient dans la barre Information Protection en configurant la stratégie Azure Information Protection en conséquence.

![Suppression ou réorganisation d’étiquettes dans la stratégie Azure Information Protection](../media/info-protect-contextmenu.png)

Au lieu de supprimer une étiquette, vous pouvez simplement la désactiver si vous souhaitez conserver sa configuration mais l’empêcher de s’afficher dans la barre Information Protection.

Triez les étiquettes de manière à ce que les utilisateurs les voient dans un ordre de progression logique dans la barre Information Protection. Par exemple, triez les étiquettes dans leur ordre croissant de confidentialité afin que les utilisateurs voient l’étiquette la moins sensible en premier et l’étiquette la plus sensible en dernier. La [stratégie par défaut](configure-policy-default.md) utilise cette configuration.

> [!IMPORTANT]
>Si vous configurez des [conditions](configure-policy-classification.md) qui peuvent s’appliquer à plusieurs étiquettes, vous devez trier les étiquettes de la moins sensible à la plus sensible. Ce tri permet de s’assurer que l’étiquette la plus sensible est appliquée lorsque les conditions sont évaluées.


Suivez la procédure indiquée ci-dessous pour effectuer ces modifications.

1. Si vous ne l’avez pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com), puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, effectuez l’une des actions suivantes (supprimer, désactiver, ou réorganiser une étiquette) :

    - Pour supprimer une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez supprimer, cliquez sur **Supprimer cette étiquette**, puis cliquez sur **Oui** pour confirmer. Cliquez ensuite sur **Enregistrer**. 

    - Pour désactiver une étiquette : sélectionnez l’étiquette que vous souhaitez désactiver. Dans le Panneau **Étiquette**, pour l’option **Activé**, cliquez sur **Désactivé**, puis sur **Enregistrer**.

    - Pour réorganiser une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez réorganiser, cliquez sur **Déplacer vers le haut** ou **Déplacer vers le bas** jusqu'à ce que l’étiquette soit à l’endroit souhaité. Cliquez ensuite sur **Enregistrer**. 

3. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  





<!--HONumber=Sep16_HO1-->


