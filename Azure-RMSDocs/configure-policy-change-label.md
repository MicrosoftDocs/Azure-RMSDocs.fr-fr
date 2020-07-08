---
title: Modifier une étiquette Azure Information Protection – AIP
description: Vous pouvez modifier ou affiner les étiquettes vues par les utilisateurs sur la barre Information Protection, en les configurant dans la stratégie Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e62a8086197a7e6fcd5715b9dc15e42cda72d4c9
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047743"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Comment modifier ou personnaliser une étiquette existante pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Vous pouvez modifier ou optimiser les étiquettes que les utilisateurs voient dans la barre Information Protection ou à partir du bouton **Protéger** du ruban Office en les configurant dans le portail Azure.

Par exemple, vous pouvez modifier le nom d’étiquette ou de sous-étiquette, l’info-bulle, la couleur et l’ordre. Vous pouvez modifier les marquages visuels tels qu’un pied de page et un filigrane. Vous pouvez également choisir la protection et la classification automatique ou recommandée de l’étiquette.

Pour modifier une étiquette, suivez les instructions suivantes :

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **classifications**  >  **étiquettes** : dans le volet **Azure information protection-étiquettes** , sélectionnez l’étiquette que vous souhaitez modifier.

    Vous devez procéder différemment si vous souhaitez réorganiser une étiquette : au lieu de sélectionner l’étiquette, cliquez dessus avec le bouton droit ou sélectionnez le menu contextuel associé à l’étiquette. Ensuite, sélectionnez les options **Monter** ou **Descendre**.

3. Chaque fois que vous apportez des modifications dans un nouveau volet, cliquez sur **Enregistrer** dans ce volet si vous souhaitez conserver vos modifications.
    
    Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

4. Si vous avez modifié le nom d’affichage ou la description de l’étiquette et que vous les avez configurés pour des langues supplémentaires : exportez de nouveau votre stratégie Azure Information Protection, fournissez les nouvelles traductions et importer les modifications. Pour plus d’informations, consultez [Comment configurer les étiquettes pour différentes langues](configure-policy-languages.md).

> [!TIP]
>Si vous souhaitez réinitialiser les valeurs par défaut de l’une des étiquettes par défaut, utilisez les informations contenues dans l’article [Stratégie Information Protection par défaut](configure-policy-default.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration des options que vous pouvez effectuer pour une étiquette et d’autres paramètres pour votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).



