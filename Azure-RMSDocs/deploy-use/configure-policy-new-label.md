---
title: "Comment créer une étiquette | Azure Information Protection"
description: "Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes que les utilisateurs voient dans la barre Information Protection."
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: ebb11148718f22c79bb49c82b9855f5e6f2a5b18
ms.openlocfilehash: 5cf6237f33d0818c8411cbb5126fc825c3c411d7


---

# Comment créer une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes que les utilisateurs voient dans la barre Information Protection.

Vous pouvez ajouter une étiquette ou ajouter une sous-étiquette à une étiquette existante lorsque vous avez besoin d’un niveau supplémentaire de classification. Par exemple, l’étiquette **Secret**, qui se trouve dans la [stratégie par défaut](configure-policy-default.md), contient des sous-étiquettes.

Utilisez les instructions suivantes pour ajouter une étiquette à la stratégie Azure Information Protection.

1. Si ce n’est déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général, puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, effectuez l’une des opérations suivantes :

    - Pour créer une étiquette, cliquez sur **Ajouter une nouvelle étiquette**.

    - Pour créer une sous-étiquette, cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette à laquelle vous souhaitez créer une sous-étiquette, puis cliquez sur **Ajouter une sous-étiquette**.

3. Dans le panneau **Étiquette** ou **Sous-étiquette**, sélectionnez les options que vous souhaitez pour cette nouvelle étiquette, puis cliquez sur **Enregistrer**.

    > [!NOTE]
    >Pour en savoir plus sur la configuration de la protection, consultez la rubrique [Comment configurer une étiquette pour appliquer la protection](configure-policy-protection.md).

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  





<!--HONumber=Sep16_HO4-->

