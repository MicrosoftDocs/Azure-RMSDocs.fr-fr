---
title: Présentation de la stratégie Azure Information Protection
description: Comprendre les étiquettes et les paramètres dans une stratégie de Azure Information Protection qui est téléchargée sur le client Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 21efcc84720849b6164a7754cf82c786a7559192
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386421"
---
# <a name="overview-of-the-azure-information-protection-policies"></a>Vue d’ensemble des stratégies de Azure Information Protection

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) dans la documentation de Microsoft 365. *

> [!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>

Une stratégie Azure Information Protection contient les éléments suivants que vous pouvez configurer :
    
- Les étiquettes incluses permettant aux administrateurs et aux utilisateurs de classer (et éventuellement protéger) les documents et les e-mails.

- Le titre et l’info-bulle de la barre Information Protection, que les utilisateurs voient dans leurs applications Office.

- L’option permettant de définir une étiquette par défaut comme point de départ de la classification de documents et d’e-mails.

- L’option permettant d’appliquer la classification lorsque des utilisateurs enregistrent des documents et envoient des e-mails.

- L’option invitant les utilisateurs à fournir une raison lorsqu’ils sélectionnent une étiquette qui a une sensibilité inférieure à l’étiquette originale.

- L’option d’étiqueter automatiquement un e-mail en fonction de ses pièces jointes.

- L’option permettant de contrôler si la barre Information Protection est affichée dans les applications Office.

- L’option permettant de contrôler si le bouton Ne pas transférer s’affiche dans Outlook.

- L’option permettant aux utilisateurs de spécifier leurs propres autorisations pour les documents.

- L’option permettant de fournir un lien d’aide personnalisé aux utilisateurs.

Azure Information Protection est livré avec une [stratégie par défaut](configure-policy-default.md), qui contient cinq étiquettes principales. Deux de ces étiquettes contiennent des sous-étiquettes pour fournir des sous-catégories, si nécessaire. 

Quand une étiquette est configurée pour des sous-étiquettes, les utilisateurs ne peuvent pas sélectionner l’étiquette principale, mais doivent sélectionner une des sous-étiquettes. Dans ce scénario, l’étiquette principale est prise en charge comme conteneur d’affichage uniquement pour le nom et la couleur.

Les étiquettes Azure Information Protection peuvent être utilisées avec la gamme complète des données généralement créées et stockées par une organisation, de la classification la plus basse des données personnelles à la classification la plus élevée des données hautement confidentielles. 

Vous pouvez utiliser les étiquettes par défaut sans les modifier, vous pouvez les personnaliser, ou encore les supprimer et créer de nouvelles étiquettes. Pour obtenir des instructions complètes, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des exemples montrant comment personnaliser la stratégie Azure Information Protection et voir le comportement qui en résulte pour les utilisateurs, suivez les didacticiels ci-dessous :

- [Modifier la stratégie Azure Information Protection et créer une nouvelle étiquette](infoprotect-quick-start-tutorial.md)

- [Configurer les paramètres de stratégie Azure Information Protection qui interagissent](infoprotect-settings-tutorial.md)