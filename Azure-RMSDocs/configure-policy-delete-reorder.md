---
title: Supprimer ou réorganiser une étiquette Azure Information Protection
description: Vous pouvez supprimer ou réorganiser les étiquettes Azure Information Protection que voient les utilisateurs.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: ab7c15e84b83bccb1af08c0e26631f1885217b11
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39489982"
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Comment supprimer ou réorganiser une étiquette pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Vous pouvez supprimer ou réorganiser les étiquettes Azure Information Protection que les utilisateurs voient dans leurs applications Office en sélectionnant ces actions pour les étiquettes.

![Suppression ou réorganisation d’étiquettes dans la stratégie Azure Information Protection](./media/info-protect-contextmenu.png)

Quand vous supprimez une étiquette qui a été appliquée à des documents et à des e-mails et que ces derniers sont ensuite ouverts par le client Azure Information Protection, les utilisateurs voient **Non défini** en guise d’état pour l’étiquette. Toutefois, les informations de l’étiquette sont conservées dans les métadonnées et peuvent donc être lues par les services qui les recherchent.

En outre, si l’étiquette supprimée appliquait une protection, cette protection n’est pas supprimée. Les paramètres de protection de l’étiquette sont conservés et s’affichent dans la section **Modèles de protection**. Ce modèle peut maintenant être converti en une nouvelle étiquette ou lié à une étiquette. Tant que ce modèle est conservé, vous ne pouvez pas créer une étiquette avec le même nom que l’étiquette que vous avez supprimée. Si c’est ce que vous voulez faire, vous disposez des options suivantes :

- Convertir le modèle en étiquette. 
    
    Cette action est recommandée, car si nécessaire, vous pouvez ensuite changer le nom du modèle et modifier les paramètres de protection.

- Utiliser PowerShell pour renommer le modèle ou le supprimer.
    
    Avant d’effectuer ces actions, vérifiez si d’autres administrateurs ou services utilisent le modèle et l’identifient par son nom actuel. Supprimez un modèle seulement si vous n’avez pas besoin d’ouvrir des documents ou des e-mails qui ont été protégés par le modèle.

Pour plus d’informations sur la gestion des modèles de protection, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).

Avant de supprimer une étiquette, envisagez plutôt de la désactiver ou de la supprimer de la stratégie :
    
- Quand vous désactivez une étiquette qui a été appliquée à des documents et e-mails, elle n’est pas supprimée de ces derniers. L’étiquette demeure dans la stratégie, mais ne s’affiche plus en tant qu’étiquette que les utilisateurs peuvent sélectionner dans la barre Information Protection. La désactivation d’une étiquette vous permet de conserver la configuration d’origine au cas où vous souhaiteriez que des utilisateurs dans la même stratégie sélectionnent l’étiquette ultérieurement, après une simple réactivation de celle-ci.

- En outre, quand vous supprimez une étiquette d’une stratégie, l’étiquette appliquée n’est pas supprimée de ces documents et e-mails. Toutefois, quand vous supprimez l’étiquette de la stratégie, vous pouvez l’ajouter à une autre stratégie. Pour plus d’informations, consultez [Ajouter une étiquette à une stratégie Azure Information Protection ou la supprimer de celle-ci](configure-policy-add-remove-label.md).

Triez les étiquettes de manière à ce que les utilisateurs les voient dans un ordre de progression logique dans la barre Information Protection. Par exemple, triez les étiquettes dans leur ordre croissant de confidentialité afin que les utilisateurs voient l’étiquette la moins sensible en premier et l’étiquette la plus sensible en dernier. La [stratégie par défaut](configure-policy-default.md) utilise cette configuration et reflète la sensibilité croissante dans les noms des étiquettes.

> [!IMPORTANT]
>Si vous configurez des [conditions](configure-policy-classification.md) qui peuvent s’appliquer à plusieurs étiquettes, vous devez trier les étiquettes de la moins sensible à la plus sensible. Ce tri permet de s’assurer que l’étiquette la plus sensible est appliquée lorsque les conditions sont évaluées.


Suivez la procédure indiquée ci-dessous pour effectuer ces modifications.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **CLASSIFICATIONS** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, effectuez une ou plusieurs des actions suivantes : 

    - Pour supprimer une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez supprimer, cliquez sur **Supprimer cette étiquette**, puis cliquez sur **OK** pour confirmer. 

    - Pour désactiver une étiquette : sélectionnez l’étiquette que vous souhaitez désactiver. Dans le Panneau **Étiquette**, pour l’option **Activé**, sélectionnez **Désactivé**, puis cliquez sur **Enregistrer**.

    - Pour réorganiser une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette à réorganiser, cliquez sur **Déplacer vers le haut** ou **Déplacer vers le bas** jusqu'à ce que l’étiquette se trouve à l’endroit souhaité.  

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

