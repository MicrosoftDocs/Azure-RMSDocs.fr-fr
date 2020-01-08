---
title: Vue d’ensemble – Kit SDK Microsoft Information Protection
description: Microsoft Information Protection (MIP) réunit les services de classification, d’étiquetage et de protection de Microsoft dans un kit SDK assurant une expérience d’administration unique.
author: msmbaldwin
ms.service: information-protection
ms.topic: overview
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: 45d2e4fb96bb81d8eb7bb982502693e9d5ebf981
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556059"
---
# <a name="overview"></a>Vue d’ensemble

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) réunit les services de classification, d’étiquetage et de protection de Microsoft :

- L’administration unifiée recouvre Office 365, Azure Information Protection, Windows Information Protection et d’autres services Microsoft. 
- Des tiers peuvent utiliser ce SDK MIP pour intégrer des applications à l’aide d’un service standard et complet de protection et de schéma d’étiquetage des données.

* [Qu’est-ce que le Centre de sécurité et conformité Office 365 ?](https://docs.microsoft.com/office365/securitycompliance/)
* [Qu’est-ce qu’Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection)
* [Comment la protection fonctionne-t-elle dans Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Kit SDK Microsoft Information Protection

Le kit SDK MIP expose les services de protection et d’étiquetage du Centre de sécurité et conformité Office 365 à des applications et services tiers. Les développeurs peuvent utiliser le kit SDK pour générer une prise en charge native afin d’appliquer des étiquettes et une protection aux fichiers. Les développeurs peuvent réfléchir aux actions à entreprendre lorsque des étiquettes spécifiques sont détectées et penser aux informations chiffrées par MIP. 

La protection et les étiquettes appliquées aux informations sur la suite de services de Microsoft sont **cohérentes**. La cohérence permet aux applications et aux services qui prennent en charge MIP de lire et d’écrire les étiquettes d’une manière prévisible et commune.

Cas d’utilisation généraux du kit SDK MIP :

* Application métier qui applique des étiquettes de classification aux fichiers lors de l’exportation.
* Application d’une conception CAO/FAO qui assure une prise en charge native de l’étiquetage Microsoft Information Protection.
* Répartiteur de sécurité d’accès cloud (CASB) ou solution de protection contre la perte de données sécurité qui réfléchit aux données chiffrées avec Azure Information Protection.

Pour obtenir une liste plus complète, consultez [Concepts liés aux API](concept-apis-use-cases.md).

Le kit SDK MIP est pris en charge sur les plateformes suivantes :

[!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous êtes maintenant prêt à commencer avec le kit SDK. Avant toute chose, [effectuez les étapes d’installation et de configuration du SDK MIP](setup-configure-mip.md). En suivant ces étapes, vous êtes sûr que votre machine cliente et votre abonnement Office 365 seront correctement configurés.

