---
title: "Configuration de stratégies délimitées| Azure Information Protection"
description: "Pour configurer d’autres paramètres et étiquettes pour des utilisateurs spécifiques, vous devez configurer une stratégie délimitée pour Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d1a5e3b85d5450bcb2064a6c3b95e6ad802eea3
ms.openlocfilehash: 99d7a2a9580466492edc313329cada315a9966d6


---

# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées

>*S’applique à : Azure Information Protection*

**[ Cette fonctionnalité est disponible dans une préversion et est susceptible d’être modifiée. ]**

Quand la stratégie Azure Information Protection se télécharge sur des ordinateurs sur lesquels est installé le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), tous les utilisateurs obtiennent les paramètres et étiquettes de la stratégie par défaut ou les modifications que vous avez configurées pour la stratégie globale. Si vous voulez les compléter en donnant d’autres paramètres et étiquettes à des utilisateurs spécifiques, vous devez créer une **stratégie délimitée** (actuellement en préversion) configurée pour ces utilisateurs.

Tous les utilisateurs reçoivent la stratégie globale, qui contient la barre de titre et l’info-bulle, les paramètres globaux et les étiquettes globales Information Protection. Si vous avez configuré des stratégies délimitées pour des utilisateurs spécifiques, ces utilisateurs reçoivent alors ces paramètres et étiquettes supplémentaires. 

Les stratégies délimitées, comme les étiquettes, sont classées dans le portail Azure. Si un utilisateur est configuré pour plusieurs étendues, une stratégie effective est calculée pour cet utilisateur avant d’être téléchargée. Selon l’ordre des stratégies, le dernier paramètre de stratégie est appliqué. Les étiquettes que l’utilisateur voit proviennent de la stratégie globale et des étiquettes supplémentaires des stratégies délimitées auxquelles appartient l’utilisateur. 

Étant donné qu’une stratégie délimitée hérite toujours des étiquettes et paramètres de la stratégie globale, les étiquettes de la stratégie globale s’affichent quand vous créez ou modifiez une stratégie délimitée. Toutefois, vous ne pouvez pas modifier les étiquettes de la stratégie globale quand vous modifiez une stratégie délimitée. En revanche, vous pouvez ajouter des sous-étiquettes à ces étiquettes héritées.

Par exemple, si vous disposez d’une étiquette nommée Confidentiel dans la stratégie globale, tous les utilisateurs la voient. Vous ne pouvez pas la supprimer ni la réorganiser avec une stratégie délimitée. Mais vous pouvez éventuellement créer une stratégie délimitée pour le service Marketing qui permet d’ajouter une nouvelle sous-étiquette à Confidentiel, afin que ces utilisateurs voient Confidentiel\Promotions. Ensuite, vous créez une autre stratégie délimitée pour le service Ventes qui permet d’ajouter une nouvelle sous-étiquette à Confidentiel, afin que ces utilisateurs voient Confidentiel\Partenaires. Chaque sous-étiquette peut alors être configurée pour des paramètres différents et la sous-étiquette est uniquement visible pour les utilisateurs relevant des services respectifs.


Pour configurer une stratégie délimitée pour Azure Information Protection :

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général.

2. Accédez au panneau **Azure Information Protection**: par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information Protection** dans la zone Filtrer. Dans les résultats, sélectionnez **Azure Information Protection**. 

    Dans le panneau **Azure Information Protection** initial, sélectionnez **Ajouter une nouvelle stratégie (PRÉVERSION)**. S’affiche alors le deuxième panneau qui sert à présenter l’actualisation de la stratégie globale, puis à configurer votre nouvelle stratégie délimitée.

3. Spécifiez le nom et la description de la stratégie que seuls les administrateurs voient dans le portail Azure. Ce nom doit être unique pour votre locataire. Ensuite, cliquez sur **Spécifier les utilisateurs/groupes qui obtiennent cette stratégie** et dans les panneaux suivants, vous pouvez rechercher et sélectionner les utilisateurs et groupes pour cette stratégie. Les étiquettes et paramètres que vous configurez dans cette stratégie délimitée sont appliqués à ces utilisateurs uniquement. 

4. Maintenant, créez des étiquettes ou configurez les paramètres de la stratégie délimitée. La stratégie globale est toujours appliquée en premier, afin de compléter la stratégie globale avec les nouvelles étiquettes et de remplacer les paramètres globaux. Par exemple, la stratégie globale peut ne pas avoir d’étiquette par défaut spécifiée et vous configurez une étiquette par défaut différente dans les différentes stratégies délimitées à des services spécifiques.

    Si vous avez besoin d’aide pour configurer des étiquettes ou paramètres, utilisez les liens fournis dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

5. Comme quand vous modifiez la stratégie globale, quand vous apportez des modifications dans un panneau Azure Information Protection, cliquez sur **Enregistrer** pour enregistrer les modifications, ou cliquez sur **Ignorer** pour rétablir les derniers paramètres enregistrés. 

6. Quand vous avez fini d’apporter les modifications souhaitées pour cette stratégie délimitée, dans le panneau **Azure Information Protection** initial, vérifiez que cette stratégie délimitée respecte l’ordre dans lequel vous voulez l’appliquer. Cette vérification s’avère importante quand vous avez sélectionné le même utilisateur pour plusieurs stratégies délimitées. Ensuite, cliquez sur **Publier**. 

Le client Azure Information Protection vérifie toutes les modifications à chaque démarrage d’une application Office prise en charge. Il télécharge les modifications dans la stratégie globale ou les stratégies délimitées qui s’appliquent à cet utilisateur.

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, essayez le [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).




<!--HONumber=Dec16_HO1-->


