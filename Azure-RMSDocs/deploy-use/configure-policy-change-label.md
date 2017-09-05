---
title: "Modifier une étiquette Azure Information Protection"
description: "Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection en les configurant dans la stratégie Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: 343b38caa14d3f67a932eedae37ed10c55f371ff
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Comment modifier ou personnaliser une étiquette existante pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection en les configurant dans la stratégie Azure Information Protection.

Par exemple, vous pouvez modifier un nom d’étiquette ou de sous-étiquette, une info-bulle, la couleur, le tri, l’application ou non de marquages visuels (pied de page ou un filigrane), et l’application ou non à Azure Rights Management protection, ainsi que la classification recommandée ou automatique.

Procédez comme suit pour modifier une étiquette.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Pour changer une étiquette de la stratégie globale afin qu’elle s’applique à tous les utilisateurs, sélectionnez l’étiquette à changer dans le panneau **Azure Information Protection : Stratégie globale** ainsi que tous les panneaux suivants si nécessaire. Pour changer une étiquette d’une [stratégie délimitée](configure-policy-scope.md) pour qu’elle s’applique uniquement aux utilisateurs sélectionnés, sélectionnez d’abord **Stratégies délimitées** dans la sélection de menu **STRATÉGIES**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

    Il existe une exception si vous voulez réorganiser une étiquette, ce que vous faites dans le panneau de la stratégie globale ou de votre stratégie délimitée sélectionnée : cliquez avec le bouton droit sur l’étiquette ou sélectionnez le menu contextuel de l’étiquette, puis sélectionnez les options **Déplacer vers le haut** ou **Déplacer vers le bas**.

3. Chaque fois que vous apportez des modifications dans un panneau, cliquez sur **Enregistrer** dans ce panneau si vous souhaitez conserver vos modifications.

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

5. Si vous avez modifié le nom d’étiquette ou la description et que vous les avez configurés pour des langues supplémentaires, vous devez exporter de nouveau votre stratégie Azure Information Protection, fournir une nouvelle traduction et importer les modifications. Pour plus d’informations, consultez [Guide pratique pour configurer les étiquettes pour des langues différentes](configure-policy-languages.md).

> [!TIP]
>Si vous souhaitez réinitialiser l’une des étiquettes par défaut sur ses valeurs par défaut, utilisez les informations de la [stratégie Information Protection par défaut](configure-policy-default.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration des options disponibles pour une étiquette et d’autres paramètres de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


