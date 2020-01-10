---
title: Modifier une étiquette Azure Information Protection – AIP
description: Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection en les configurant dans la stratégie Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 4530f365f63756c61a7ad97936cffb64cc22d1b8
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75742856"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Comment modifier ou personnaliser une étiquette existante pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Azure information protection client pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection ou à partir du bouton **Protéger** du ruban Office en les configurant dans le portail Azure.

Par exemple, vous pouvez changer le nom d’une étiquette ou sous-étiquette, l’info-bulle, la couleur et l’ordre. Vous pouvez choisir si l’étiquette applique des marquages visuels comme un pied de page ou un filigrane. Vous pouvez aussi choisir si l’étiquette applique une protection, ainsi qu’une classification recommandée ou automatique.

Pour modifier une étiquette, utilisez les instructions suivantes :

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche pour ressources, services et docs : commencez à taper les **informations** et sélectionnez **Azure information protection**.

2. À partir de l’option de menu **classifications** > **étiquettes** : dans le volet **Azure information protection-étiquettes** , sélectionnez l’étiquette que vous souhaitez modifier.

    Vous devez procéder différemment si vous souhaitez réorganiser une étiquette : au lieu de sélectionner l’étiquette, cliquez dessus avec le bouton droit ou sélectionnez le menu contextuel associé à l’étiquette. Ensuite, sélectionnez les options **Déplacer vers le haut** ou **Déplacer vers le bas**.

3. Chaque fois que vous apportez des modifications dans un nouveau volet, cliquez sur **Enregistrer** dans ce volet si vous souhaitez conserver vos modifications.
    
    Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

4. Si vous avez changé le nom d’étiquette ou la description et que vous les avez configurés pour des langues supplémentaires : réexportez votre stratégie Azure Information Protection, fournissez de nouvelles traductions et importer les modifications. Pour plus d’informations, consultez [Guide pratique pour configurer les étiquettes pour des langues différentes](configure-policy-languages.md).

> [!TIP]
>Si vous souhaitez réinitialiser l’une des étiquettes par défaut sur ses valeurs par défaut, utilisez les informations de la [stratégie Information Protection par défaut](configure-policy-default.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration des options disponibles pour une étiquette et d’autres paramètres de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).



