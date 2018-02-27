---
title: "Modifier une étiquette Azure Information Protection"
description: "Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection en les configurant dans la stratégie Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: da89ea5986ac78cdf79e97336d74c54e9db2a825
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/23/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Comment modifier ou personnaliser une étiquette existante pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection en les configurant dans la stratégie Azure Information Protection.

Par exemple, vous pouvez changer le nom d’une étiquette ou sous-étiquette, l’info-bulle, la couleur et l’ordre. Vous pouvez choisir si l’étiquette applique des marquages visuels comme un pied de page ou un filigrane. Vous pouvez aussi choisir si l’étiquette applique une protection, ainsi qu’une classification recommandée ou automatique.

Pour modifier une étiquette, utilisez les instructions suivantes :

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Pour changer une étiquette de la stratégie globale afin qu’elle s’applique à tous les utilisateurs, sélectionnez l’étiquette à changer dans le panneau **Azure Information Protection : Stratégie globale** ainsi que tous les panneaux suivants si nécessaire. Pour changer une étiquette d’une [stratégie délimitée](configure-policy-scope.md) pour qu’elle s’applique uniquement aux utilisateurs sélectionnés, sélectionnez d’abord **Stratégies délimitées** dans la sélection de menu **STRATÉGIES**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

    Si vous voulez réorganiser une étiquette, la procédure n’est pas la même. Dans le panneau de la stratégie globale ou de votre stratégie délimitée sélectionnée : cliquez avec le bouton droit sur l’étiquette ou sélectionnez le menu contextuel de l’étiquette. Ensuite, sélectionnez les options **Déplacer vers le haut** ou **Déplacer vers le bas**.

3. Chaque fois que vous apportez des modifications dans un panneau, cliquez sur **Enregistrer** dans ce panneau si vous souhaitez conserver vos modifications.

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

5. Si vous avez changé le nom d’étiquette ou la description et que vous les avez configurés pour des langues supplémentaires : réexportez votre stratégie Azure Information Protection, fournissez de nouvelles traductions et importer les modifications. Pour plus d’informations, consultez [Guide pratique pour configurer les étiquettes pour des langues différentes](configure-policy-languages.md).

> [!TIP]
>Si vous souhaitez réinitialiser l’une des étiquettes par défaut sur ses valeurs par défaut, utilisez les informations de la [stratégie Information Protection par défaut](configure-policy-default.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration des options disponibles pour une étiquette et d’autres paramètres de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


