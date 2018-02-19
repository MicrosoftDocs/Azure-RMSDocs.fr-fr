---
title: "Supprimer ou réorganiser une étiquette Azure Information Protection"
description: "Vous pouvez supprimer ou réorganiser les étiquettes que les utilisateurs voient dans la barre Information Protection en configurant la stratégie Azure Information Protection en conséquence."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: b6694c7c205f7ccd899669cc887b79ab39ec8ec4
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Comment supprimer ou réorganiser une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Vous pouvez supprimer ou réorganiser les étiquettes que les utilisateurs voient dans la barre Information Protection en sélectionnant ces actions dans la stratégie Azure Information Protection.

![Suppression ou réorganisation d’étiquettes dans la stratégie Azure Information Protection](../media/info-protect-contextmenu.png)

Quand vous supprimez une étiquette qui a été appliquée à des documents et des e-mails, puis que vous publiez la stratégie Azure Information Protection, l’étiquette est automatiquement supprimée des documents et des e-mails lors de leur prochaine ouverture par le client Azure Information Protection.

Cependant, si l’étiquette appliquait une protection, cette protection n’est pas supprimée. Les paramètres de protection de l’étiquette sont conservés et s’affichent dans les **Modèles de protection**. Ce modèle peut maintenant être converti en une nouvelle étiquette ou lié à une étiquette. Tant que ce modèle est conservé, vous ne pouvez pas créer une étiquette avec le même nom que l’étiquette que vous avez supprimée. Si c’est ce que vous voulez faire, vous disposez des options suivantes :

- Convertir le modèle en étiquette. 
    
    Cette action est recommandée, car si nécessaire, vous pouvez ensuite changer le nom du modèle et modifier les paramètres de protection.

- Utiliser PowerShell pour renommer le modèle ou le supprimer.
    
    Avant d’effectuer ces actions, vérifiez si d’autres administrateurs ou services utilisent le modèle et l’identifient par son nom actuel. Supprimez un modèle seulement si vous n’avez pas besoin d’ouvrir des documents ou des e-mails qui ont été protégés par le modèle.

Pour plus d’informations sur la gestion des modèles de protection, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).

Avant de supprimer une étiquette, pensez à plutôt la désactiver. Quand vous désactivez une étiquette qui a été appliquée à des documents et des e-mails, l’étiquette appliquée n’est pas supprimée de ces documents et e-mails, mais elle ne s’affiche plus comme une étiquette que les utilisateurs peuvent sélectionner dans la barre Information Protection. La désactivation d’une étiquette vous permet également de conserver la configuration d’origine au cas où vous souhaiteriez que des utilisateurs sélectionnent l’étiquette ultérieurement, après une simple réactivation.

Triez les étiquettes de manière à ce que les utilisateurs les voient dans un ordre de progression logique dans la barre Information Protection. Par exemple, triez les étiquettes dans leur ordre croissant de confidentialité afin que les utilisateurs voient l’étiquette la moins sensible en premier et l’étiquette la plus sensible en dernier. La [stratégie par défaut](configure-policy-default.md) utilise cette configuration et reflète la sensibilité croissante dans les noms des étiquettes.

> [!IMPORTANT]
>Si vous configurez des [conditions](configure-policy-classification.md) qui peuvent s’appliquer à plusieurs étiquettes, vous devez trier les étiquettes de la moins sensible à la plus sensible. Ce tri permet de s’assurer que l’étiquette la plus sensible est appliquée lorsque les conditions sont évaluées.


Suivez la procédure indiquée ci-dessous pour effectuer ces modifications.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette à configurer s’applique à tous les utilisateurs, restez dans le panneau **Azure Information Protection - Stratégie globale**.
    
    Si l’étiquette à configurer se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour s’appliquer uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez **Stratégies délimitées**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

3. Dans le panneau **Azure Information Protection - Stratégie globale** ou le panneau **Stratégie :\<nom>**, effectuez une ou plusieurs des actions suivantes : 

    - Pour supprimer une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez supprimer, cliquez sur **Supprimer cette étiquette**, puis cliquez sur **Oui** pour confirmer. Cliquez ensuite sur **Enregistrer**. 

    - Pour désactiver une étiquette : sélectionnez l’étiquette que vous souhaitez désactiver. Dans le Panneau **Étiquette**, pour l’option **Activé**, cliquez sur **Désactivé**, puis sur **Enregistrer**.

    - Pour réorganiser une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette à réorganiser, cliquez sur **Déplacer vers le haut** ou **Déplacer vers le bas** jusqu'à ce que l’étiquette se trouve à l’endroit souhaité. Cliquez ensuite sur **Enregistrer**. 

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

