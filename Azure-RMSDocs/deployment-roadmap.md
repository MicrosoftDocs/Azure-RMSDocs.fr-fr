---
title: Feuille de route pour le déploiement d’Azure Information Protection
description: Utilisez ces étapes pour préparer, implémenter et gérer Azure Information Protection pour votre organisation.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 251b193012dc32518a0a236cf1ee751545d4391e
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382392"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Feuille de route pour le déploiement d’Azure Information Protection

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

> [!TIP]
> Vous pouvez également Rechercher l’un des articles suivants :
> - [Guides de procédures pour les scénarios courants utilisant Azure Information Protection](how-to-guides.md)
>- [Feuille de route Azure Information Protection Release](information-support.md#information-about-new-releases-and-updates)

Utilisez les étapes décrites dans les pages de feuille de route suivantes comme recommandations pour vous aider à préparer, implémenter et gérer les Azure Information Protection pour votre organisation.

## <a name="identify-your-deployment-roadmap"></a>Identifier la feuille de route de votre déploiement

Avant de déployer AIP, passez en revue la [Configuration requise pour le système AIP](./requirements.md).

Ensuite, choisissez l’une des feuilles de route suivantes, en fonction des besoins et de l' [abonnement](https://azure.microsoft.com/pricing/details/information-protection/)de votre organisation :

- **Utiliser la classification, l’étiquetage et la protection**:

    Recommandé pour tous les clients disposant d’un abonnement. Les fonctionnalités supplémentaires incluent la découverte des informations sensibles et l’étiquetage des documents et des e-mails pour la classification. 

    Les étiquettes peuvent également appliquer une protection, ce qui simplifie cette étape pour vos utilisateurs. 

    Cette feuille de route est prise en charge pour les étiquettes AIP créées avec le client classique et les étiquettes de sensibilité qui utilisent la [plateforme d’étiquetage unifiée](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

    Pour plus d’informations, consultez [la feuille de route AIP pour classifier, étiqueter et protéger vos données](deployment-roadmap-classify-label-protect.md).

- **Utiliser uniquement la protection**: 

    Recommandé pour les clients disposant d’un abonnement qui ne prend pas en charge la classification et les étiquettes, mais qui prend en charge la protection sans étiquette. Le client Classic doit être installé.

    Pour plus d’informations, consultez la feuille [de route AIP pour la protection des données uniquement](deployment-roadmap-protect-only.md).

## <a name="next-steps"></a>Étapes suivantes

Lorsque vous déployez Azure Information Protection, il peut s’avérer utile de consulter les [questions fréquemment posées](faqs.md), ainsi que la page [informations et support](information-support.md) pour obtenir des ressources supplémentaires.