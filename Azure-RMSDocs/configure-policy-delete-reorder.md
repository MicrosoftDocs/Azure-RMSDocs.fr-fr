---
title: Supprimer ou réorganiser une étiquette Azure Information Protection – AIP
description: Vous pouvez supprimer ou réorganiser les étiquettes Azure Information Protection que voient les utilisateurs.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 3640660b65bcd9a0c8e437c1180a07fcd1a32d51
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806666"
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Comment supprimer ou réorganiser une étiquette pour Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) dans la documentation de Microsoft 365. *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Vous pouvez supprimer ou réorganiser les étiquettes Azure Information Protection que les utilisateurs voient dans leurs applications Office en sélectionnant ces actions pour les étiquettes.

![Suppression ou réorganisation d’étiquettes dans la stratégie Azure Information Protection](./media/info-protect-contextmenu.png)

Quand vous supprimez une étiquette qui a été appliquée à des documents et à des e-mails et que ces derniers sont ensuite ouverts par le client Azure Information Protection, les utilisateurs voient **Non défini** en guise d’état pour l’étiquette. Toutefois, les informations de l’étiquette sont conservées dans les métadonnées et peuvent donc être lues par les services qui les recherchent.

En outre, si l’étiquette supprimée appliquait une protection, cette protection n’est pas supprimée. Les paramètres de protection de l’étiquette sont conservés et s’affichent dans la section **Modèles de protection**. Ce modèle peut maintenant être converti en une nouvelle étiquette. Tant que ce modèle est conservé, vous ne pouvez pas créer une étiquette avec le même nom que l’étiquette que vous avez supprimée. Si c’est ce que vous voulez faire, vous disposez des options suivantes :

- Convertir le modèle en étiquette. 
    
    Cette action est recommandée, car si nécessaire, vous pouvez ensuite changer le nom du modèle et modifier les paramètres de protection.

- Utiliser PowerShell pour renommer le modèle ou le supprimer.
    
    Avant d’effectuer ces actions, vérifiez si d’autres administrateurs ou services utilisent le modèle et s’ils l’ont déjà utilisé. Vous pouvez identifier le modèle par son ID de modèle (qui ne change pas) ou son nom (qui peut être changé). En guise de bonne pratique, supprimez un modèle seulement si vous êtes certain que les utilisateurs n’auront pas à ouvrir les documents ou les e-mails qui ont été protégés par le modèle.

Pour plus d’informations sur la gestion des modèles de protection, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).

Avant de supprimer une étiquette, envisagez plutôt de la désactiver ou de la supprimer de la stratégie :
    
- Quand vous désactivez une étiquette qui a été appliquée à des documents et e-mails, elle n’est pas supprimée de ces derniers. L’étiquette demeure dans la stratégie, mais ne s’affiche plus en tant qu’étiquette que les utilisateurs peuvent sélectionner dans la barre Information Protection. La désactivation d’une étiquette vous permet de conserver la configuration d’origine au cas où vous souhaiteriez que des utilisateurs dans la même stratégie sélectionnent l’étiquette ultérieurement, après une simple réactivation de celle-ci.

- En outre, quand vous supprimez une étiquette d’une stratégie, l’étiquette appliquée n’est pas supprimée de ces documents et e-mails. Toutefois, quand vous supprimez l’étiquette de la stratégie, vous pouvez l’ajouter à une autre stratégie. Pour plus d’informations, consultez [Ajouter une étiquette à une stratégie Azure Information Protection ou la supprimer de celle-ci](configure-policy-add-remove-label.md).

Triez les étiquettes de manière à ce que les utilisateurs les voient dans un ordre de progression logique dans la barre Information Protection. Par exemple, triez les étiquettes dans leur ordre croissant de confidentialité afin que les utilisateurs voient l’étiquette la moins sensible en premier et l’étiquette la plus sensible en dernier. La [stratégie par défaut](configure-policy-default.md) utilise cette configuration et reflète la sensibilité croissante dans les noms des étiquettes.

> [!IMPORTANT]
>Si vous configurez des [conditions](configure-policy-classification.md) qui peuvent s’appliquer à plusieurs étiquettes, vous devez trier les étiquettes de la moins sensible à la plus sensible. Ce tri permet de s’assurer que l’étiquette la plus sensible est appliquée lorsque les conditions sont évaluées.


Suivez la procédure indiquée ci-dessous pour effectuer ces modifications.

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **classifications**  >  **étiquettes** : dans le volet **Azure information protection-étiquettes** , effectuez une ou plusieurs des actions suivantes : 

    - Pour supprimer une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez supprimer, cliquez sur **Supprimer cette étiquette**, puis cliquez sur **OK** pour confirmer. 

    - Pour désactiver une étiquette : sélectionnez l’étiquette que vous souhaitez désactiver. Dans le volet **étiquette** , pour **activé**, sélectionnez **désactivé**, puis cliquez sur **Enregistrer**.

    - Pour réorganiser une étiquette : cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette que vous souhaitez réorganiser, puis cliquez sur **monter** ou **descendre jusqu’à ce que** l’étiquette soit dans l’ordre de votre choix.  

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  


