---
title: Vue d’ensemble – Kit SDK Microsoft Information Protection
description: Microsoft Information Protection (MIP) réunit les services de classification, d’étiquetage et de protection de Microsoft dans un kit SDK assurant une expérience d’administration unique.
author: BryanLa
ms.service: information-protection
ms.topic: overview
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 775ae3d524947c8300de0e011b92c2cad106905a
ms.sourcegitcommit: d677088db8588fb2cc4a5d7dd296e76d0d9a2e9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251724"
---
# <a name="overview"></a>Vue d’ensemble

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) réunit les services de classification, d’étiquetage et de protection de Microsoft dans un kit SDK assurant une expérience d’administration unique. L’administration unifiée recouvre Office 365, Azure Information Protection, Windows Information Protection et d’autres services Microsoft. Des tiers peuvent utiliser ce kit SDK pour intégrer des applications à l’aide d’un service standard et complet de protection et de schéma d’étiquetage de données.

* [Qu’est-ce que le Centre de sécurité et conformité Office 365 ?](https://docs.microsoft.com/office365/securitycompliance/)
* [Qu’est-ce qu’Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection)
* [Comment la protection fonctionne-t-elle dans Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Kit SDK Microsoft Information Protection

Le kit SDK MIP expose les services de protection et d’étiquetage du Centre de sécurité et conformité Office 365 à des applications et des services tiers. Les développeurs peuvent utiliser le kit SDK pour générer une prise en charge native afin d’appliquer des étiquettes et une protection aux fichiers. Les développeurs peuvent réfléchir aux actions à entreprendre lorsque des étiquettes spécifiques sont détectées et penser aux informations chiffrées par MIP. 

La protection et les étiquettes appliquées aux informations sur la suite de services de Microsoft sont **cohérentes**. La cohérence permet aux applications et aux services qui prennent en charge MIP de lire et d’écrire les étiquettes d’une manière prévisible et commune.

Cas d’utilisation généraux du kit SDK MIP :

* Application métier qui applique des étiquettes de classification aux fichiers lors de l’exportation.
* Application d’une conception CAO/FAO qui assure une prise en charge native de l’étiquetage Microsoft Information Protection.
* Répartiteur de sécurité d’accès cloud (CASB) ou solution de protection contre la perte de données sécurité qui réfléchit aux données chiffrées avec Azure Information Protection.

Pour obtenir une liste plus complète, consultez [Concepts liés aux API](concept-apis-use-cases.md).

## <a name="next-steps"></a>Étapes suivantes

Vous êtes maintenant prêt à commencer avec le kit SDK. La première chose que vous devez faire est de suivre les [étapes d’installation et de configuration du kit SDK MIP](setup-configure-mip.md), pour vérifier que votre machine cliente et votre abonnement Office 365 sont correctement configurés.

