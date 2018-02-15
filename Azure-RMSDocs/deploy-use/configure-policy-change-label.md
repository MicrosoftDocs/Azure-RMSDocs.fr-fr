---
title: "Modifier une étiquette Azure Information Protection"
description: "Vous pouvez modifier ou affiner les étiquettes vues par les utilisateurs sur la barre Information Protection, en les configurant dans la stratégie Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: f1ffd4c459f2fa194372450f5713c920422f744d
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Comment modifier ou personnaliser une étiquette existante pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Vous pouvez modifier ou affiner les étiquettes vues par les utilisateurs sur la barre Information Protection, en les configurant dans la stratégie Azure Information Protection.

Par exemple, vous pouvez modifier le nom d’étiquette ou de sous-étiquette, l’info-bulle, la couleur et l’ordre. Vous pouvez modifier les marquages visuels tels qu’un pied de page et un filigrane. Vous pouvez également choisir la protection et la classification automatique ou recommandée de l’étiquette.

Pour modifier une étiquette, suivez les instructions suivantes :

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [Portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Davantage de services** et commencez à écrire **informations** dans la zone de filtre. Sélectionnez **Azure Information Protection**.

2. Pour modifier une étiquette de la stratégie globale afin qu’elle s’applique à tous les utilisateurs, sélectionnez l’étiquette à modifier à partir du panneau **Azure Information Protection - Stratégie globale** et de tous les panneaux suivants si nécessaires. Pour modifier une étiquette d’une [stratégie étendue](configure-policy-scope.md) afin qu’elle s’applique uniquement aux utilisateurs sélectionnés, sélectionnez d’abord **Stratégies étendues** à partir de la sélection du menu **STRATÉGIES**. Sélectionnez ensuite votre stratégie étendue à partir du panneau **Azure Information Protection - Stratégies étendues**.

    Il existe une exception dans le cas où vous voudriez réorganiser une étiquette. Dans le panneau de stratégie à partir de la stratégie globale ou de votre stratégie étendue : faites un clic droit sur l’étiquette ou bien sélectionnez son menu contextuel. Ensuite, sélectionnez les options **Monter** ou **Descendre**.

3. Chaque fois que vous apportez des modifications dans un panneau, cliquez sur **Enregistrer** dans ce panneau si vous souhaitez conserver vos modifications.

4. Pour rendre vos modifications disponibles aux utilisateurs, cliquez sur **Publier** sur le panneau **Azure Information Protection**.

5. Si vous avez modifié le nom d’affichage ou la description de l’étiquette et que vous les avez configurés pour des langues supplémentaires : exportez de nouveau votre stratégie Azure Information Protection, fournissez les nouvelles traductions et importer les modifications. Pour plus d’informations, consultez [Comment configurer les étiquettes pour différentes langues](configure-policy-languages.md).

> [!TIP]
>Si vous souhaitez réinitialiser les valeurs par défaut de l’une des étiquettes par défaut, utilisez les informations contenues dans l’article [Stratégie Information Protection par défaut](configure-policy-default.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration des options que vous pouvez effectuer pour une étiquette et d’autres paramètres pour votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


