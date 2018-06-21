---
title: Modifier une étiquette Azure Information Protection
description: Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection en les configurant dans la stratégie Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: a8c745ac51c34139792367d55c5a83592c191571
ms.sourcegitcommit: 87d73477b7ae9134b5956d648c390d2027a82010
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32326257"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Comment modifier ou personnaliser une étiquette existante pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection ou à partir du bouton **Protéger** du ruban Office en les configurant dans le portail Azure.

Par exemple, vous pouvez changer le nom d’une étiquette ou sous-étiquette, l’info-bulle, la couleur et l’ordre. Vous pouvez choisir si l’étiquette applique des marquages visuels comme un pied de page ou un filigrane. Vous pouvez aussi choisir si l’étiquette applique une protection, ainsi qu’une classification recommandée ou automatique.

Pour modifier une étiquette, utilisez les instructions suivantes :

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **CLASSIFICATIONS** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette que vous souhaitez changer.

    Vous devez procéder différemment si vous souhaitez réorganiser une étiquette : au lieu de sélectionner l’étiquette, cliquez dessus avec le bouton droit ou sélectionnez le menu contextuel associé à l’étiquette. Ensuite, sélectionnez les options **Déplacer vers le haut** ou **Déplacer vers le bas**.

3. Chaque fois que vous apportez des modifications dans un nouveau panneau, cliquez sur **Enregistrer** dans ce panneau si vous souhaitez conserver vos modifications.
    
    Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

4. Si vous avez changé le nom d’étiquette ou la description et que vous les avez configurés pour des langues supplémentaires : réexportez votre stratégie Azure Information Protection, fournissez de nouvelles traductions et importer les modifications. Pour plus d’informations, consultez [Guide pratique pour configurer les étiquettes pour des langues différentes](configure-policy-languages.md).

> [!TIP]
>Si vous souhaitez réinitialiser l’une des étiquettes par défaut sur ses valeurs par défaut, utilisez les informations de la [stratégie Information Protection par défaut](configure-policy-default.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration des options disponibles pour une étiquette et d’autres paramètres de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


