---
title: "Préparer l’environnement pour Azure RMS et AD RMS"
description: "Conseils si vous avez Azure Rights Management avec AD RMS déployé."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 577f91958c4b54c4fb023d973475c917b28f72b3
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2017
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Préparation de l’environnement pour Azure Rights Management quand vous avez également Active Directory Rights Management Services (AD RMS)

>*S’applique à : Azure Information Protection, Office 365*

Conseils importants si vous utilisez déjà Active Directory Rights Management Services (AD RMS) et que le scénario suivant s’applique :

## <a name="you-see-an-option-to-activate-azure-rms-when-you-configure-azure-information-protection"></a>Vous voyez une option pour activer Azure RMS quand vous configurez Azure Information Protection

Le panneau **Azure Information Protection - Paramètres RMS (préversion)** comporte une option pour activer le service Azure Rights Management (Azure RMS). 

Si vous utilisez également d’Active Directory Rights Management Services (AD RMS), ne sélectionnez pas l’option **Activer**. L’activation d’Azure Rights Management quand vous avez également AD RS n’est pas une combinaison compatible. Ce scénario n’est pas pris en charge et provoque des résultats imprévisibles. Il est donc important de ne pas activer Azure Rights Management à ce stade. 

Quand vous êtes prêt à migrer les ordinateurs d’AD RMS vers le service Azure Rights Management, vous pouvez démarrer un processus de migration. L’une des étapes de la migration consiste à activer le service, mais cette opération s’effectue une fois que vous avez exporté les informations de configuration d’AD RMS vers le service Azure Rights Management. Ce processus permet de s’assurer que les documents et e-mails qui étaient protégés par AD RMS peuvent toujours être ouverts.

Quand le service Azure Rights Management n’est pas activé, vous pouvez toujours utiliser Azure Information Protection pour les étiquettes qui appliquent uniquement la classification. Une stratégie par défaut spéciale est créée pour vous. Elle n’inclut pas la protection des données, et les options de configuration restent indisponibles jusqu’à ce que le service Azure Rights Management soit activé.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Étape 1 : Configurer votre stratégie Azure Information Protection pour la classification et l’étiquetage, sans protection

À partir du panneau **Azure Information Protection** initial, sélectionnez **Stratégie globale** pour afficher et configurer votre stratégie par défaut qui n’inclut pas d’options de protection des données. Pour en savoir plus, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Étape 2 : Commencer la planification de la migration

Suivez les instructions de migration : [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-start-to-configure-labels-for-protection"></a>Étape 3 : Commencer à configurer les étiquettes pour la protection

Une fois que vous avez activé le service Azure Rights Management dans le cadre du processus de migration, vous pouvez configurer des étiquettes pour la protection des données. Toutefois, si vous migrez des utilisateurs par lots, vérifiez que les étiquettes qui appliquent la protection [ont pour portée uniquement les utilisateurs migrés](configure-policy-scope.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


