---
title: Votre clé de locataire Azure Information Protection
description: Au lieu que Microsoft gère la clé racine pour Azure Information Protection, vous souhaiterez peut-être créer et gérer cette clé (appelée « apporter votre propre clé » ou BYOK) pour votre locataire, pour se conformer à des réglementations spécifiques.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 35c898ded852970e380c8061ba8f97d040860017
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386387"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Planification et implémentation de la clé de locataire Azure Information Protection

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

La clé de locataire Azure Information Protection est une clé racine pour votre organisation. D’autres clés peuvent être dérivées de cette clé racine, y compris les clés utilisateur, les clés d’ordinateur ou les clés de chiffrement de document. Chaque fois que Azure Information Protection utilise ces clés pour votre organisation, elles sont chaînées par chiffrement à votre clé de locataire racine Azure Information Protection.

En plus de votre clé racine de locataire, votre organisation peut nécessiter une sécurité locale pour des documents spécifiques. La protection de clé locale est généralement requise uniquement pour une petite quantité de contenu et, par conséquent, est configurée avec une clé racine de locataire.

## <a name="azure-information-protection-key-types"></a>Types de clés de Azure Information Protection

La clé racine de votre locataire peut être :

- [Généré par Microsoft](#tenant-root-keys-generated-by-microsoft)
- Généré par les clients ayant une protection [Bring Your Own Key (BYOK)](#bring-your-own-key-byok-protection) .

Si vous disposez d’un contenu hautement sensible nécessitant une protection supplémentaire locale, nous vous recommandons d’utiliser le [chiffrement à clé double (DKE)](#double-key-encryption-dke).

> [!TIP]
> Si vous utilisez le client classique et que vous avez besoin d’une protection locale supplémentaire, utilisez à la place [votre propre clé (hyok)](#hold-your-own-key-hyok) .
>

## <a name="tenant-root-keys-generated-by-microsoft"></a>Clés racines de locataire générées par Microsoft

La clé par défaut, générée automatiquement par Microsoft, est la clé par défaut utilisée exclusivement par Azure Information Protection pour gérer la plupart des aspects du cycle de vie de votre clé de locataire.

Continuez à utiliser la clé Microsoft par défaut lorsque vous souhaitez déployer Azure Information Protection rapidement et sans un matériel, un logiciel ou un abonnement Azure. Les exemples incluent des environnements de test ou des organisations sans exigences réglementaires pour la gestion des clés.

Pour la clé par défaut, aucune autre étape n’est requise et vous pouvez accéder directement à la prise en main de [la clé racine de votre locataire](get-started-tenant-root-keys.md).

> [!NOTE]
> La clé par défaut générée par Microsoft est l’option la plus simple avec les principaux frais d’administration.
>
> Dans la plupart des cas, vous ne savez peut-être pas que vous disposez d’une clé de locataire, car vous pouvez vous inscrire à Azure Information Protection et le reste du processus de gestion de clés est géré par Microsoft.

## <a name="bring-your-own-key-byok-protection"></a>Protection Bring Your Own Key (BYOK)

BYOK-protection utilise des clés qui sont créées par les clients, soit au Azure Key Vault soit localement dans l’organisation du client. Ces clés sont ensuite transférées vers Azure Key Vault pour une meilleure gestion.

Utilisez BYOK lorsque votre organisation a des réglementations de conformité pour la génération de clés, notamment le contrôle de toutes les opérations de cycle de vie. Par exemple, lorsque votre clé doit être protégée par un module de sécurité matériel.

Pour plus d’informations, consultez [configurer la protection BYOK](byok-price-restrictions.md). 

Une fois configuré, poursuivez la prise en main de [votre clé racine de locataire](get-started-tenant-root-keys.md) pour plus d’informations sur l’utilisation et la gestion de votre clé.

## <a name="double-key-encryption-dke"></a>Chiffrement à clé double (DKE)

**Concerne**: client d’étiquetage unifié AIP uniquement

La protection DKE fournit une sécurité supplémentaire pour votre contenu à l’aide de deux clés : une créée et détenue par Microsoft dans Azure, et une autre créée et conservée localement par le client.

DKE requiert les deux clés pour accéder au contenu protégé, garantissant que Microsoft et d’autres tiers n’ont jamais accès aux données protégées.

Les DKE peuvent être déployés dans le Cloud ou localement, ce qui offre une flexibilité totale pour les emplacements de stockage.

Utilisez DKE lorsque votre organisation :

- Veut s’assurer qu’il ne peut jamais déchiffrer le contenu protégé, dans toutes les circonstances.
- Vous ne souhaitez pas que Microsoft ait le même accès aux données protégées.
- A des exigences réglementaires pour conserver les clés dans une limite géographique. Avec DKE, les clés détenues par le client sont conservées dans le centre de données client.

> [!NOTE]
> DKE est similaire à une zone de dépôt de sécurité qui nécessite une clé de banque et une clé de client pour accéder.
> DKE-protection nécessite à la fois la clé détenue par Microsoft et la clé détenue par le client pour déchiffrer le contenu protégé.

Pour plus d’informations, consultez [chiffrement à clé double](/microsoft-365/compliance/double-key-encryption) dans la documentation Microsoft 365.

## <a name="hold-your-own-key-hyok"></a>Conserver votre propre clé (HYOK)

**Concerne**: client classique AIP uniquement

HYOK-protection utilise une clé qui est créée et conservée par les clients, à un emplacement isolé du Cloud. Étant donné que HYOK-protection autorise uniquement l’accès aux données pour les applications et les services locaux, les clients qui utilisent HYOK ont également une clé Cloud pour les documents Cloud.

Utilisez HYOK pour les documents qui sont :

- Limité à quelques personnes
- Non partagé en dehors de l’Organisation
- Sont consommés uniquement sur le réseau interne.

Ces documents ont généralement la classification la plus élevée au sein de votre organisation, en tant que « top secret ».

Le contenu peut être chiffré à l’aide de la protection HYOK uniquement si vous disposez du client Classic. Toutefois, si vous avez un contenu protégé par HYOK, il peut être affiché à la fois dans le client d’étiquetage classique et le client d’étiquetage unifié.  

Pour plus d’informations, voir [les détails de la conservation de votre propre clé (hyok)](configure-adrms-restrictions.md).

