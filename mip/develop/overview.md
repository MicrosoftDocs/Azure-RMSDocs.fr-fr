---
title: Vue d’ensemble – Kit SDK Microsoft Information Protection
description: Microsoft Information Protection (MIP) réunit les services de classification, d’étiquetage et de protection de Microsoft dans un kit SDK assurant une expérience d’administration unique.
author: BryanLa
ms.service: information-protection
ms.topic: overview
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: bryanla
ms.openlocfilehash: 656f4af77ce3e26515c5e54103e8d3b341439271
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56250740"
---
# <a name="overview"></a>Vue d'ensemble

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) est l’unification de la classification de Microsoft, l’étiquetage et les services de protection :

- L’administration unifiée recouvre Office 365, Azure Information Protection, Windows Information Protection et d’autres services Microsoft. 
- Des tiers peuvent utiliser le SDK MIP pour intégrer des applications à l’aide d’un étiquetage service schéma et la protection de données standard et cohérentes.

* [Qu’est-ce que le Centre de sécurité et conformité Office 365 ?](https://docs.microsoft.com/office365/securitycompliance/)
* [Qu’est-ce qu’Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection)
* [Comment la protection fonctionne-t-elle dans Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Kit SDK Microsoft Information Protection

Le SDK MIP expose les services de l’étiquetage et la protection à partir d’Office 365 centre de sécurité et conformité, aux services et applications de fournisseurs tiers. Les développeurs peuvent utiliser le kit SDK pour générer une prise en charge native afin d’appliquer des étiquettes et une protection aux fichiers. Les développeurs peuvent réfléchir aux actions à entreprendre lorsque des étiquettes spécifiques sont détectées et penser aux informations chiffrées par MIP. 

La protection et les étiquettes appliquées aux informations sur la suite de services de Microsoft sont **cohérentes**. La cohérence permet aux applications et aux services qui prennent en charge MIP de lire et d’écrire les étiquettes d’une manière prévisible et commune.

Cas d’utilisation généraux du kit SDK MIP :

* Application métier qui applique des étiquettes de classification aux fichiers lors de l’exportation.
* Application d’une conception CAO/FAO qui assure une prise en charge native de l’étiquetage Microsoft Information Protection.
* Répartiteur de sécurité d’accès cloud (CASB) ou solution de protection contre la perte de données sécurité qui réfléchit aux données chiffrées avec Azure Information Protection.

Pour obtenir une liste plus complète, consultez [Concepts liés aux API](concept-apis-use-cases.md).

## <a name="next-steps"></a>Étapes suivantes

Vous êtes maintenant prêt à commencer avec le kit SDK. La première chose que vous devrez faire est [effectuer les étapes d’installation et la configuration du SDK MIP](setup-configure-mip.md). Ces étapes garantissent que votre abonnement Office 365 et l’ordinateur client sont définies correctement.

